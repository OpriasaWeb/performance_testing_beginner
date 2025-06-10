# 🧪 Performance Testing with Apache JMeter

This repository contains my beginner journey in learning performance testing using [Apache JMeter](https://jmeter.apache.org/). It includes test plans, sample test cases, and notes on what I’ve learned.

--------------------------------------------

🧠 What is a Logic Controller?
A Logic Controller defines the flow or logic of your test execution within a Thread Group.

Think of it like programming control structures (if, loop, switch, etc.) — but in JMeter's drag-and-drop interface.

🧰 Types of Logic Controllers (with simple use cases)
| Logic Controller           | What it Does                                                         | Example Use Case                                       |
| -------------------------- | -------------------------------------------------------------------- | ------------------------------------------------------ |
| **Loop Controller**        | Repeats its child samplers a number of times                         | Repeat login request 5 times                           |
| **If Controller**          | Runs its child samplers **only if** a condition is true              | Run step only if user is admin                         |
| **While Controller**       | Runs its children **while a condition** is true                      | Keep polling API until status is "DONE"                |
| **Switch Controller**      | Runs **only one** child based on index or condition                  | Simulate different user flows                          |
| **Random Controller**      | Randomly picks one of its children to execute                        | Random page visits                                     |
| **Interleave Controller**  | Rotates through each child on each loop iteration                    | Alternate between login and search                     |
| **Once Only Controller**   | Runs its children **only once per thread**, even if loop count is >1 | Do login only once per virtual user                    |
| **Transaction Controller** | Groups requests and reports their combined time                      | Measure login + dashboard load time as one transaction |


✅ Where Do You Add Logic Controllers?
Inside a Thread Group:

Right-click on Thread Group → Add → Logic Controller → choose your controller

Then, place your HTTP Request samplers inside that logic controller.

📌 Example: Loop Controller inside a Thread Group
Thread Group
└── Loop Controller (Loops 3 times)
     └── HTTP Request (runs 3x for each thread)

🔁 Why Use Logic Controllers?
Simulate real user behavior

Control request order and conditions

Group requests to create logical transactions

Avoid repeating test setup in complicated ways

--------------------------------------------

In JMeter, timers are used in performance testing to simulate real-world user behavior by introducing delays between requests. By default, JMeter sends requests as fast as possible, which isn't realistic. Timers help you control the pace of your test by spacing out requests like actual users would.

🔧 What Timers Do in JMeter:
Add delays between requests or between samplers.

Simulate think time (time users take between actions).

Prevent overloading the server with continuous requests.

Enable realistic traffic patterns.

🕒 Common Types of Timers in JMeter:
Timer Type	Description
Constant Timer	Adds a fixed delay (e.g., 3000 ms = 3 seconds).
Gaussian Random Timer	Adds a delay with random variation using a normal (Gaussian) distribution.
Uniform Random Timer	Adds a random delay using a uniform distribution.
Constant Throughput Timer	Tries to achieve a specified throughput (e.g., 100 requests per minute).
Synchronizing Timer	Pauses threads until a specified number of threads have reached the point, then releases them all at once (for load spikes).
Poisson Random Timer	Adds delay based on a Poisson distribution (used in more advanced, statistically representative tests).

💡 Example Use Case:
Let’s say you’re testing a login and dashboard view:

User logs in.

User views dashboard after 5 seconds.

You can add a Constant Timer (5000 ms) before the dashboard request to simulate that delay.

⚠️ Tips:
Timers are scoped: they apply to all samplers under the same level in the test plan tree.

You can use multiple timers together, but the delays are additive.

Don't forget that real users don’t click instantly — timers are critical to mimic reality.

--------------------------------------------

🚀 Beginner JMeter Projects (with Ideas and Goals)
1. Static Website Load Test
Test URL: A GitHub Pages or personal website
Goal: Measure how fast static pages load under multiple users.

What You Learn:

Thread Groups

HTTP Requests

View Results Tree / Summary Report

2. Login Page Simulation (Dummy API or Local Server)
Test: Simulate a user logging in (POST request)
Goal: Test how login handles 10–100 users.

What You Learn:

HTTP POST with parameters

Assertion (e.g., successful login message)

HTTP Header Manager

3. REST API Load Test
Test API: Use a public API like https://jsonplaceholder.typicode.com
Goal: Simulate GET/POST/PUT/DELETE requests.

What You Learn:

RESTful testing

JSON extractor

Parameterization

4. E-commerce Workflow Simulation
Test Scenario: User browses → selects item → adds to cart → checkout (mock endpoints or dummy APIs)
Goal: Group multiple requests and measure end-to-end time.

What You Learn:

Transaction Controller

Think Time (Timers)

Logic Controllers (If, Loop)

5. File Download Test
Test: Download a PDF/image from a website
Goal: Measure download speed and time.

What You Learn:

HTTP GET with large payloads

Response Time vs Size Analysis

6. Database Performance (JDBC Test)
Test: Query a MySQL or SQLite database
Goal: Measure how fast queries are processed under load.

What You Learn:

JDBC Connection Configuration

SQL Query Sampler

Result Assertions

7. Login Test with CSV Data (Data-Driven Test)
Test: Use a CSV file with 10 different usernames/passwords
Goal: Test multiple user credentials.

What You Learn:

CSV Data Set Config

Parameterization

User simulation with different inputs

8. Website with Login Session (Cookie Handling)
Test: Login → visit dashboard → logout
Goal: Simulate real session-based navigation.

What You Learn:

Cookie Manager

HTTP Header Manager

Session Management

9. Performance Comparison (Single vs Multiple Users)
Test: Send requests with 1, 10, 50, 100 users
Goal: Observe how response time changes.

What You Learn:

Threads

Ramp-up time

Load behavior analysis

10. Performance Monitoring with Backend Listener (Grafana + InfluxDB)
Test: Hook JMeter to a monitoring dashboard
Goal: See live graphs of load, latency, etc.

What You Learn:

Backend Listener

Grafana/InfluxDB basics (optional for advanced beginner)