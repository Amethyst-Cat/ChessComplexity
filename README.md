About
====
In this project we build off of the work of [Goldammer](https://github.com/cgoldammer/chess-analysis/blob/master/position_sharpness.ipynb) and confirm that neural networks can estimate position complexity to a high degree of accuracy. We suggest that complexity should be measured as both the probability of making a mistake and the magnitude of a mistake, which provides a less-biased and more comprehensive insight into a position's complexity.

This page explains the impact of a complexity metric on chess. 

To view the technical analysis behind this project, go to the [Wiki Analysis Page](https://github.com/Amethyst-Cat/ChessComplexity/wiki/Analysis). 

Accessing the Software
----
We have also created a software demonstrating one application of a complexity measure, specifically generating puzzles from any game that go beyond tactics.

- To find more information about the software, including download instructions, go to the [Wiki Software Page](https://github.com/Amethyst-Cat/ChessComplexity/wiki/Software).

- To download the chess training software, go to the [Releases Page](https://github.com/Amethyst-Cat/ChessComplexity/releases) and download the ChessOracle1.2 zip file under Assets.

A Second Chess Revolution
====
The First Chess Revolution: How good is the position?
----
Modern-day chess engines provide objective evaluations and effectively answer the question, "how good or bad is the position?" 

The answer to this question has augmented our knowledge of chess by opening up a world of positions ranked highly by engines that were not previously considered by human players. Engines generate free online tactics, allow us to explore and learn from new positions (changing every part of the game from openings to endgames), and identify mistakes in games instantly. Engines have allowed us to gain deeper insights into positions, and the answer to this first question has undoubtedly changed chess forever.

The Second Chess Revolution: How complicated is the position?
----
We now have the answer to the second revolutionary question, "how complicated is the position?" Modern chess engines cannot reason like humans, and the evaluations they create are generated in a vacuum without humans. We posit that a second, more human metric to evaluate positions will produce another revolution in the way we understand chess. While position evaluation, the first metric, allowed to gain insights into a position, this second metric will allow us to gain insights into ourselves.

From an objective metric of a position's complexity or difficulty, we can determine what types of positions are difficult for lower rated players that are considered easier by higher level players, which would give all chess players a clear idea of how to improve their chess. We can determine chess personalities from analyzing players who prefer complex positions and players who prefer simpler positions, and we can use these personalities to build computers who play chess like humans. We can use our algorithm to suggest difficult and complicated training puzzles from any game, which would explode the range of free online chess puzzles beyond tactics. Our algorithm would further revolutionize openings as players would steer positions to be as complicated or simple as they like. 

In short, a metric of human difficulty would have applications in every area of chess and add another dimension of understanding to chess, similar to the revolution from the metric of position evaluation.

Chess.com and Lichess: Drivers of the Revolution
====
The primary factor in the power of machine learning algorithms is the amount of data used. With 200 games, a computer can distinguish between complicated phases of a game and less complicated phases, albeit with mediocre precision. With 25,000 games, we get results like these:

![](https://github.com/Amethyst-Cat/ChessComplexity/blob/master/images/hardeasypositions.png)
Our neural network ranking 1000 random positions from the World Cup 2019 by their complexity. Simple positions at the top, complex positions at the bottom.

Websites like lichess and chess.com have [**over a billion games**](https://database.lichess.org/) in their databases, a significant portion of which are already computer analyzed by their users. We need to call upon these websites to use their vast amounts of data to create an objective metric of complexity and drive the second chess revolution.

From How to Why: Limitations and the Need for Humans
====
Any chess player knows that there is very little to be learned in staring at Stockfish (a modern-day engine) evaluations. Perfect engines tempt us into believing we can imitate them and reach perfect play, but Stockfish doesn't think like a human. Stockfish knows a move is good because it looked at every combination of moves within a 20 move radius and found the path to the best position. In short, Stockfish justifies a good move with more moves. Stockfish cannot explain why a move a good, and neither can any other engine. Neither can a neural network explain why a position is complicated, it just knows that the position is complicated.

Even if we have perfect answers to "how good is a position" and "how complicated is a position", these questions by themselves have no value. Where we want to end up is answering the questions "why is a position good" and "why is a position complicated", and these questions can only be answered by humans. 

Modern chess engines have massive potential to advance chess theory, yet I suspect that the greatest advancements computers have provided to chess is in opening theory. With computers, we now have massively complex opening files and books but very few new patterns. We find it difficult to justify why a position is good or bad without resorting to long lines of moves or the computer centipawn evaluation. One cannot acknowledge the benefits of chess computers without acknowledging how they have allowed us to substitute memorization for logic. Beginning chess players learn very quickly when they learn logical patterns like pins, forks, and doubled pawns, but do not progress much when they learn the first 15 moves of the Fried Liver.

We do not need more memorization. These programs have given us rulers and scales, and we must use them to determine the laws of the chess world. Chess players must use these tools to augment their understanding, to find positions commonly misevaluated and to understand why we misevaluate them. We need more theory, more answers to "why" than "how", and more patterns to explain positions. My hope is that a more human metric of complexity will supplement modern-day engines and allow us to better understand chess and the humans that play chess.
