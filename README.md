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


You're on the right track — the problems I gave earlier **cover foundational patterns** and simulate **real-world use cases** that regularly appear in interviews. But to **prepare well for product-based and FAANG companies**, you should also practice a **specific set of LLD problems** known to be frequently asked.

Here’s an **expanded and enriched list of problems** from actual interviews at companies like **Amazon, Google, Facebook (Meta), Microsoft, Uber, Atlassian, Flipkart, etc.**, across **three difficulty tiers**, focusing on **OOP + Concurrency**, just like your goal.

---

## ✅ **Most Frequently Asked LLD Problems in Product/FAANG Companies**

### 🔹 EASY to MEDIUM

| # | Problem                                | Asked In             | Concepts                            |
| - | -------------------------------------- | -------------------- | ----------------------------------- |
| 1 | **Design a Logger Rate Limiter**       | Google, Uber         | Concurrency, Token bucket           |
| 2 | **Design a Tic-Tac-Toe Game**          | Microsoft, Atlassian | OOP, Game loop                      |
| 3 | **Design a Parking Lot**               | Amazon, Flipkart     | OOP, State transitions              |
| 4 | **Design an ATM Machine**              | Visa, JPMorgan       | OOP, State machine                  |
| 5 | **Design a Snake Game / Chess**        | Microsoft            | OOP, Game engine                    |
| 6 | **Design a Library Management System** | Adobe, Zoho          | OOP, Modeling                       |
| 7 | **Design a Splitwise App**             | Google, Uber         | Graph modeling, Debt simplification |

---

### 🔹 MEDIUM to HARD (Concurrency Emphasis)

| #  | Problem                                                | Asked In          | Concepts                                    |
| -- | ------------------------------------------------------ | ----------------- | ------------------------------------------- |
| 8  | **Thread-Safe In-Memory Cache (TTL support)**          | Amazon, Uber      | `ConcurrentHashMap`, background cleaner     |
| 9  | **Design a Food Delivery System**                      | Uber Eats         | Multi-threaded task queues                  |
| 10 | **Design a Rate Limiter for API Gateway**              | Google            | Fixed window / sliding window               |
| 11 | **Design Uber Cab Matching Service**                   | Uber              | Pub-sub, concurrent matching                |
| 12 | **Design a Distributed ID Generator (like Snowflake)** | Twitter           | Bitwise ops, concurrency, atomic counters   |
| 13 | **Design an Elevator System**                          | Amazon, Microsoft | Controller, concurrent requests             |
| 14 | **Design a ThreadPoolExecutor (from scratch)**         | Google            | BlockingQueue, producer-consumer            |
| 15 | **Design a Notification Service**                      | Meta              | Observer pattern, concurrency, backpressure |

---

### 🔹 HARD (System + Real-World + Deep OOP/Concurrency)

| #  | Problem                                                  | Asked In         | Concepts                                    |
| -- | -------------------------------------------------------- | ---------------- | ------------------------------------------- |
| 16 | **Design a Multiplayer Game Matchmaking Engine**         | Riot Games, Meta | Concurrency, Player Pools                   |
| 17 | **Design a Stock Exchange Matching Engine**              | Bloomberg        | Queues, locks, atomic ops                   |
| 18 | **Design a Scalable Order Management System (Flipkart)** | Flipkart, Amazon | Event-driven order pipeline                 |
| 19 | **Design a Real-Time Chat Application**                  | Meta, WhatsApp   | Thread-safe queues, connection management   |
| 20 | **Design a Scalable Notification System (Push + Poll)**  | Google, LinkedIn | Push vs Pull, pub-sub, rate control         |
| 21 | **Design Dropbox (File Storage System)**                 | Meta             | Thread-safe file operations, versioning     |
| 22 | **Design a Mini Twitter / News Feed System**             | Facebook         | Feed aggregation, eventual consistency      |
| 23 | **Design a Load Balancer**                               | Meta, Amazon     | Round-robin, sticky sessions, health checks |

---

## 📌 What Top Companies Test In LLD Interviews:

### 🔸 Object-Oriented Design (OOP)

* Class Hierarchy, SOLID Principles
* Composition vs Inheritance
* Design Patterns (Strategy, Observer, State, Singleton, etc.)

### 🔸 Concurrency & Thread Safety

* Thread Pools
* Blocking Queues, Semaphores, Atomic Classes
* Race condition prevention (Locks, CAS)

### 🔸 Scalability Awareness

* Stateless designs
* Interfaces for plugging distributed components (e.g., Redis for cache)
* Asynchronous communication (queues, callbacks)

---

## ✅ Ideal Preparation Plan for You:

Since you're aiming high, here’s how you should structure your LLD practice:

### Week 1–2: Master OOP

* Parking Lot
* Tic Tac Toe
* Library Management
* Vending Machine
* Elevator System

### Week 3–4: Dive into Concurrency

* Logger Rate Limiter
* In-Memory Cache (Redis-like)
* Food Delivery System
* Uber Cab Matching
* ThreadPoolExecutor

### Week 5–6: Combine Both — Real World + Concurrency

* Notification Service
* Multiplayer Matchmaking
* Stock Exchange
* Real-Time Chat
* Dropbox

---

## 🛠️ Bonus Tools & Practice Aids:

1. **UML Practice:** Use [PlantUML](https://plantuml.com/) to draw class diagrams.
2. **System Skeletons:** Implement classes + interfaces in Java (ask me for any boilerplate).
3. **Mock Interviews:** Try mock design interviews on platforms like:

   * [Excalidraw](https://excalidraw.com/)
   * [System Design Primer](https://github.com/donnemartin/system-design-primer)

---

Would you like:

* A **roadmap planner** with daily goals across 4–6 weeks?
* **Starter skeletons and UML diagrams** for any of the above problems?
* **Mock interview questions** to self-check your progress?

Let me know how you'd like to proceed!
