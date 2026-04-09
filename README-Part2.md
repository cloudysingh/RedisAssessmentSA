\# Redis Solution Architect Assignment — Part 2



\## 🎯 Objective



Design and implement a real-time leaderboard system using Redis that supports:



\* Real-time score updates

\* Top-N player retrieval

\* Player rank lookup



\---



\## 🏗️ Architecture



!\[Architecture Diagram](./images/app-diagram.png)



\---



\## 🧠 Design Overview



The leaderboard is implemented using a \*\*Redis Sorted Set (ZSET)\*\*.



\* Each player is stored as a \*\*member\*\*

\* Score is used as the \*\*sorting value\*\*

\* Redis maintains ordering automatically



\---



\## 🗂️ Data Model



\*\*Key:\*\*



```bash

leaderboard:global

```



\*\*Structure:\*\*



```text

ZSET → (player\_id → score)

```



\---



\## ⚙️ Core Operations



| Requirement        | Redis Command |

| ------------------ | ------------- |

| Add / Update Score | ZADD          |

| Get Top N Players  | ZREVRANGE     |

| Get Player Rank    | ZREVRANK      |

| Get Player Score   | ZSCORE        |



\---



\## 💻 Implementation



\### 🔹 API Layer (Flask — app.py)



Endpoints implemented:



\* `POST /score` → Add/update player score

\* `GET /top/<n>` → Retrieve top N players

\* `GET /rank/<player\_id>` → Retrieve rank and score



\---



\### 🔹 UI Layer (Flask — ui\_app.py)



\* Built as a separate service

\* Consumes API endpoints

\* Features:



&#x20; \* Live leaderboard display

&#x20; \* Score update form

&#x20; \* Auto-refresh with controlled behavior



\---



\## 🔄 System Flow



```text

User (Browser)

&#x20;  ↓

Flask UI (Port 5001)

&#x20;  ↓

Flask API (Port 5000)

&#x20;  ↓

Redis OSS (ZSET Leaderboard)

&#x20;  ↓

Replication to Redis Enterprise

```



\---



\## 🧪 Validation



\### ➕ Add Score



!\[Add Score](./screenshots/13-add-score.png)



```bash

curl -X POST http://127.0.0.1:5000/score \\

\-H "Content-Type: application/json" \\

\-d '{"player\_id": "player1", "score": 100}'

```



\---



\### 🏆 Get Top Players



!\[Top Players](./screenshots/14-get-top-players.png)



```bash

curl http://127.0.0.1:5000/top/10

```



\---



\### 🎯 Get Player Rank



!\[Player Rank](./screenshots/15-get-player-rank.png)



```bash

curl http://127.0.0.1:5000/rank/player1

```



\---



\## 🎤 Demo Steps



1\. Start Redis (Port 6380)

2\. Start API (`app.py`)

3\. Start UI (`ui\_app.py`)

4\. Open UI in browser

5\. Add/update scores

6\. Observe leaderboard updates



\---



\## 🎯 Conclusion



This solution demonstrates how Redis Sorted Sets can be used to efficiently build a real-time leaderboard system with fast updates, accurate ranking, and clean architectural separation.



