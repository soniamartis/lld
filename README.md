# Resources and high level topics to cover


## High level topics
- Gaming
- Booking systems
- Machines
- Ride hailing apps
- Chat and Video systems
- data structure designs

 ## Resources
 - https://github.com/ashishps1/awesome-low-level-design/tree/main/problems


 ### Gaming Patterns
 - Some common features of these games are : board, gameLoop, players, player objects
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

### Reservation systems observations
- Requires user, entity to be booked and a class to link user to entity
- In reality a user can book several entities, eg user books n rooms, or user books n seats in movie/ flight booking
- Payment systems are always provided with diff modes of payment like cash/ credit card
- Booking and payment are separate, we can create a booking first with status as created and on payment, we can update status of that booking. On failure , we retry n times and then release the booking
- It will be nice to use some state machine here for transitioning states of the booking, so that it doesnt go into an inconsistent state
- Define some admin methods as well like adding entities, regisering users etc
- Bookings/ reservations require some uniqueid generations, where we can use several methods like UUID.randomUUID() or prefix + Intant.now() + atomicInteger.incrementAndGet()


### Ride hailing / food delivery apps observations
- Create location class with x and y axis
- Distance between 2 points : sqrt((x1-x2)^2 + (y1-y2)^2)
- Payment modes
- 


### Machines (state design pattern)
- Sample problems
  - Elevator
  - ATM
  - Vending machine
  - traffic signal
 
### Observer pattern
- Pub sub

### Chain of responsibility
- Logging framework

### Social networking
- linkedIn
- FB

### Online shopping


### Financial
- splitwise
- stock broker
  

  

### Important questions
- SSE imp questions
- Splitwise; Concurrent logger system; Battleship game; multi-directory file system with read-write permissions; circuit breaker; Task Scheduler; Concurrent LRU Cache and some more.
