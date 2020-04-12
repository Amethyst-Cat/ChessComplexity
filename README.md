About
=====

Supervised learning to estimate the complexity of chess positions.

This project is based off of these resources:

1) [Learning to Evaluate Chess Positions with Deep Neural Networks and Limited Lookahead](https://www.ai.rug.nl/~mwiering/GROUP/ARTICLES/ICPRAM_CHESS_DNN_2018.pdf) showing dense neural networks can approximate the Stockfish evaluation function.
2) cgoldammer's work using dense networks to evaluate chess position complexity. [https://github.com/cgoldammer/chess-analysis/blob/master/position_sharpness.ipynb](https://github.com/cgoldammer/chess-analysis/blob/master/position_sharpness.ipynb)

Overview
-----
Chess engines are known to easily defeat even the best chess players, but they do not provide reasoning for their evaluations. Thus, they are not very useful as training partners, despite their ability to accurately evaluate positions and suggest perfect moves. Similar to the previous work of cgoldammer, this project seeks to create more "human" engines that can predict how complex or difficult positions are for human chessplayers.

-picture of chess engine evaluation

Methodology
=====
We take [25,000 games evaluated by Stockfish (1sec/move)](https://www.kaggle.com/c/finding-elo/data) on Kaggle and process them into training examples mapping the position (1x769 a binary vector with the locations of the pieces and whose turn it is) to the error of the move (calculated by the evaluation before the move minus the evaluation after the move). Similar to past work, we omit positions where the evaluation exceeds 300 centipawns (indicating a winning position), positions before move 12 (indicating opening theory), and scale errors so they do not exceed 100 centipawns. In addition, we also round errors below 30 centipawns to 0, as Stockfish at 1 second per move can sometimes indicate small errors even with perfect moves.

A Two-Headed Approach
-----
Unlike previous work, which mapped a position to an expected centipawn error using one dense network, we use two networks, one predicting whether or not the user made an error (the classification network) and one predicting how large an error would be if it were made (the regression network). Due to the massive amount of training examples with 0 error, we chose this approach to give our regression network more flexibility and prevent it from constantly outputting low error values to minimize mean-squared loss.

Because there are significantly more positions with no error than error, we also trained with a subset of the positions with no error to remove bias from the training set. This prevents the classification network from predicting each position will have no error to minimize categorical loss.

-picture of the training examples by error

Network Architecture
-----
We split the Kaggle game data into 5 rating categories (<1600, 1600-1900, 1900-2200, 2200-2500, 2500+) and trained five regression models and five classification models. The <1600 elo regression model trained on less data, so it is a 100-5-1 dense model with relu activation and a 20% dropout in each layer except the output, and the classification model is a similar 100-5-2 model but with softmax for the output layer. For the other rating categories, the regression model if a 1048-500-50-1 dense model with relu activation and 20% for all layers except the output, and the classification model is a similar 1048-500-50-2 with a softmax activation in the last layer. The classification models were trained on a dataset of 50% error positions and 50% non-error positions, and the regression models were trained on the error amounts in positions where the error exceeded 0. All models were trained with a learning rate of 0.001.

Results
=====
Almost all models achieved a 65% classification accuracy on the validation set (around 0.63 categorical cross-entropy loss) and a mean-squared error loss of around 0.06 (about a 0.2 mean absolute error). The models are pretty successful in seperating complex positions from non-complex positions. Complexity is approximated by the probability of an error given by the classification model multiplied by the mean value of the error given by the regression model. However, this is a relative measurement of complexity, not a measure of expected centipawn loss. Below are five of the most complex positions (deemed by the 1900-2200 model, which trained on the most amount of data - roughly 100k positions) along with 5 of the simplest positions chosen out of 1000 random positions from the 2015 World Cup.

-picture of positions

Comparison to Previous Results
-----
