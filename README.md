Download Link: https://assignmentchef.com/product/solved-ece448-assignment-2-planning-games
<br>
<h2>Part 1: Constraint Satisfaction Problem</h2>

<a name="part1"></a>Your code will require the Numpy libary.

<a name="part1"></a>Many are familiar with the problem of <a href="https://urldefense.proofpoint.com/v2/url?u=https-3A__en.wikipedia.org_wiki_Pentomino&amp;d=DwMGAg&amp;c=OCIEmEwdEq_aNlsP4fF3gFqSN-E3mlr2t9JcDdfOZag&amp;r=XHR4f_YuIFlVBwMQ5kVUO5pXtzWXJdRnmBhkLaDfxcI&amp;m=j3CfAd57FF50wSZoXxEXaCV0MymZm_STzmGcJZ9kpkw&amp;s=308B2JxVhYb38ZvPeE4JpBWarenhRw3ReqNAX0tzCKk&amp;e=">pentomino tiling</a>. The problem statement is as follows: You are given a set of shapes each made up of 5 connected squares and a board of 0s and 1s. You are required to place the pentominos on the board such that

<ul>

 <li>Pentominos may be flipped or rotated</li>

 <li>No pentominos overlap</li>

 <li>All pentominos lie completely on the board</li>

 <li>All 1s on the board are covered by a pentomino</li>

 <li>No 0s are covered by a pentomino</li>

</ul>

You will be tasked to solve this problem. To provide easier cases, you will also be tasked with tiling a board of the same size using dominos and triominos (shapes made of 2 and 3 squares respectively). The function you implement in solve.py will need to be able to tile a given board using a given set of tiles. That means that the function should work for arbitrary input tiles and boards. You may assume any instance we test on your code will have a solution. The interface of the solve function you will need to implement is described in the docstring in solve.py.

<h2>Part 2: Game of Ultimate Tic-Tac-Toe</h2>

<a name="part2"></a>For this part of the assignment, you will implement the game ultimate tic-tac-toe with minimax and alpha-beta pruning algorithms.

<h3>Rules</h3>

<a name="part2"></a>The rules of ultimate tic-tac-toe can be found on the <a href="https://urldefense.proofpoint.com/v2/url?u=https-3A__en.wikipedia.org_wiki_Ultimate-5Ftic-2Dtac-2Dtoe&amp;d=DwMGAg&amp;c=OCIEmEwdEq_aNlsP4fF3gFqSN-E3mlr2t9JcDdfOZag&amp;r=XHR4f_YuIFlVBwMQ5kVUO5pXtzWXJdRnmBhkLaDfxcI&amp;m=j3CfAd57FF50wSZoXxEXaCV0MymZm_STzmGcJZ9kpkw&amp;s=9jUjv8ycGFVKJDjTbGbEpq-irXgllaxMM08VQPj6i2Q&amp;e=">wiki page</a>. ultimate tic-tac-toe is a board game composed of nine tic-tac-toe boards arranged in a 3-by-3 grid. Each smaller 3×3 grid is referred to as a local board, and the 9×9 grid is referred to as the global board. The player starting the game can place their move on any empty spot. After the first move, the opposing player must play in the board corresponding to the square where the first player played, as shown below:

<img decoding="async" width="300" data-src="./CS440_ECE448 Assignment 2_files/Ultimate_tic-tac-toe_forced_move.png" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="./CS440_ECE448 Assignment 2_files/Ultimate_tic-tac-toe_forced_move.png" width="300">

 </noscript>

In the above image, at starting of the game, since player “X” played at the top right corner at the central local board, player “O” is sent to the top right local board and only allowed to play there. O’s next move determines the board in which X must next play, and so on.

The rules for the local board are the same as regular 3×3 tic-tac-toe. Ultimate tic-tac-toe has many variations of rules; for this part of the assignment, the winner will be the one who wins the first local board.

It’s recommended that students use <a href="https://urldefense.proofpoint.com/v2/url?u=http-3A__ultimatetictactoe.creativitygames.net_&amp;d=DwMGAg&amp;c=OCIEmEwdEq_aNlsP4fF3gFqSN-E3mlr2t9JcDdfOZag&amp;r=XHR4f_YuIFlVBwMQ5kVUO5pXtzWXJdRnmBhkLaDfxcI&amp;m=j3CfAd57FF50wSZoXxEXaCV0MymZm_STzmGcJZ9kpkw&amp;s=tMmpx9gg0PcPtXdQT3AkQPnQPIWHI3yS5sRAuowiF8k&amp;e=">the online tool</a> to play the game to fully understand the rules. For this online tool, remember to select “First Tile Wins” at top left corner from the dropdown list.

<h3>Requirements</h3>

The global game board has 9 local boards with 81 available spots. The coordinate of each empty spot is the row and the column number starting with 0. Each local board has an index starting at 0. The first row of local boards has index from 0 to 2, the second row of local boards have index from 3-5, and so on.

For this part of the assignment, you will first implement the predefined offensive agent and the predefined defensive agent to play against each other. In the provided skeleton code, the maxPlayer is the offensive agent, and the minPlayer is the defensive agent. The game always starts at the central local board (index 4). The evaluation function for each predefined agent is prioritized to three levels. If the higher level of evaluation rules is applied, then the lower level of evaluation rules won’t be used. For example, if the second rule is applicable, then the third rule won’t be used. Minimax or alpha-beta search always search the local board row by row from top left corner to bottom right corner. The search depth has maximum three levels, including current player, opposing player, and current player again. Then evaluate the resulting board position after the third level search. If the evaluation function returns two terminal states with the same value, choose whichever of the two moves comes first in this raster search order.

Predefined offensive agent:

<ul>

 <li>First rule: If the offensive agent wins (form three-in-a-row), set the utility score to be 10000.</li>

 <li>Second rule: For each local board, count the number of two-in-a-row without the third spot taken by the opposing player (unblocked two-in-a-row). For each unblocked two-in-a-row, increment the utility score by 500. For each local board, count the number of places in which you have prevented the opponent player forming two-in-a-row (two-in-a-row of opponent player but with the third spot taken by offensive agent). For each prevention, increment the utility score by 100.</li>

 <li>Third rule: For each corner taken by the offensive agent, increment the utility score by 30.</li>

</ul>

Predefined defensive agent:

<ul>

 <li>First rule: If the defensive agent wins (forms three-in-a-row), set the utility score to be -10000.</li>

 <li>Second rule: For each local board, count the number of two-in-a-row without the third spot taken by the opponent player. For each two-in-a-row, decrement the utility score by 100. For each local board, count the number of prevention of opponent player forming two-in-a-row (two-in-a-row of opponent player but with the third spot taken by defensive agent). For each prevention, decrement the utility score by 500.</li>

 <li>Third rule: For each corner taken by defensive agent, decrement the utility score by 30.</li>

</ul>

You tasks are the following:

<ul>

 <li>First implement the predefined offensive and defensive agents to play against each other for four games: offensive(minimax) vs defensive(minimax), offensive(minimax) vs defensive(alpha-beta), offensive(alpha-beta) vs defensive(minimax), and offensive(alpha-beta) vs defensive(alpha-beta). In the first two games, maxPlayer goes first, while in the rest of the games, minPlayer goes first. Report the final game board positions, number of expanded nodes, and the final winner for each game.</li>

 <li>Then come up with a smarter evaluation function to beat the offensive agent at least 80% of the time. Play the game with alpha-beta pruning for both agents for at least 20 times, with both the starting local board index and the starting player set randomly. In your report, explain your formulation, and the advantages of your evaluation function. Report the percentage of winning time and number of expanded nodes for each game. Report 3-5 representative final game boards that show the advantage of your evaluation function vs predefined offensive evaluation function.</li>

 <li>Let a human play with your own defined evaluation function for at least 10 games. Report 3-5 representative final game boards that show the advantages or disadvantages of your evaluation function. Discuss the results and findings. Do human always win over the agent? If so, what does the evaluation function fails to do?</li>

</ul>

<h2>Tips</h2>

<ul>

 <li>Use the online tool to farmilarize yourself with the rules of the game, meanwhile gain some intuition of designing a good evaluation function.</li>

 <li>Make sure the predifined agents are implemented as described. Your implementation will be graded on percentage of correctness.</li>

 <li>Determine critical steps for coming up good evaluation function and transform your thoughts to math equations.</li>

</ul>