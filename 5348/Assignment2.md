# Assignment 2

### Question 1

Traditional design

- submitAttempt
- fetchAssignmentAttempts
- markAttempt
- fetchUnmarkedAssignmentAttempts
- fetchStudentUnattemptedAssignments

Restful api design:

#### Submit attempt

- URI: `/student/{studentId}/assignment/{assignmentId}/attempts`
- Method: `POST`
- Requirements: Students submit the attempt via upload resources

#### Fetch assignment attempts

- URI: `/student/{studentId}/assignment/{assignmentId}/attempts`
- Method: `GET`
- Requirements: Get all submission attempts for a certain assignment for a student

#### Mark attempt

- URI: `/student/{studentId}/assignment/{assignmentId}/attempts/{attemptId}/mark`
- Method: `PUT`
- Requirements: Mark the certain submission attempts

#### Fetch unmarked assignment attempts

- URI: `assignment/{assignmentId}/attempts/unmark`
- Method: `GET`
- Requirements: To get all unmarked attempts of the certain assignment

#### Fetch student unattempted assignments

- URI: `/student/{studentId}/assignment/{assignmentId}/attempts/unattempted`
- Method: `GET`
- Requirements: To get a student all unattempted attempts of the certain assignment 



### Question 2

Pre-condition:

Update transactions:

- CPU processing: 0.3ms
- Disk reading: 1 block
- Sending time: 30ms

Query transactions:

- CPU processing: 35ms
- Disk reading: 230 blocks (each block occupies 4KB)
- Disk capacity: 100 MB/s

Proportion of transactions from client:

- Update transactions: 25%
- Query transactions: 75%



#### (a) 

**Time of Query transactions**: (230 * 4KB) ÷ 100MB/s = 0.0092 = 9.2ms

**Total query time** = 35ms + 9.2ms = 44.2ms



**Time of Update transactions**: 4KB ÷ 100MB/s = 0.00004 = 0.04ms

**Total update time** = 0.3ms + 30ms + 0.04ms = 30.34ms



**Average transactions time** = 44.2 x 75% + 30.34 x 25% = 40.735ms



**Throughput of each client**: 1 / 40.735 x 1000ms/s ≈ 24.55 t/s

**The total Throughput for three clients** = 24.55 x 3 = 73.65 t/s



- Throughput = 73.65 t/s
- Latency = 40.735ms



#### (b)

The largest number of clients in 2s:

**The largest number of transactions** = 2000ms ÷ 40.735ms ≈ 49.1t

**The largest number of clients** = 49.1 / 24.55 = 2

So the largest number of clients is **2** with an average response time will be below 2s



### Question 3

Pre-condition

- Component A has MTTF of 3 months and MTTR of 2 days
- Component B has MTTF of 1 year and MTTR of 4 days
- Component C has MTTF of 1 month and MTTR of 6 days



#### 1. MTTF

$$
\frac{1}{MTTF} = \frac{1}{MTTF_A} + \frac{1}{MTTF_B} + \frac{1}{MTTF_C}
$$

$$
\frac{1}{MTTF} = \frac{1}{3 * 30} + \frac{1}{365} + \frac{1}{30} = 0.0471
$$

So the MTTF of WebSys = 1 / 0.0471≈ 21.23 days



#### 2. MTTR

For the pre-condition, we can know MTTR of A has 2 days, MTTR of B has 4 days and MTTR of C has 6 days
$$
MTTR = MTTR_A + MTTR_B + MTTR_C = 2 + 4 + 6 = 12 days
$$




#### 3. Availability

$$
Availability = \frac{MTTF}{MTTF + MTTR}
$$

So the availability of the whole system is:
$$
Availability = \frac{21.23}{21.23 + 12} ≈ 0.6389
$$
The availability is 63.89%
