# Gaming LLD patterns


 - Some common classes in these games are : board, gameLoop, players, player objects
 - Board
   - initialise board with objects that should be present on the board. eg: for snakes and ladders board, the board contains list of snakes and ladders
   - add methods like making a move, check for winner, stalemate on board
 - Game loop
    - Just a while(true) loop to iterate over the players.
    - Will iterate over players and call board's makemove, will check for board's winner/ stalemate and continue with loop
    - Player selection in game loop -> add all players to list and index + 1 % listSize to get  next player
    - If only 2 players, then switch player with if currentplayer == player1 ? player2 : player1
 - Player
   - Pojo with a playerId and an object that defines the player in the grp, eg for X and Os, player is defined by the symbol X or 0 and in chess, player is identified by color     
 - Making moves
    - Use simple scanner operations
 - Sample Problems
   - Snake and Ladder
   - Battleship
   - Chess
   - tic-tac-toe
