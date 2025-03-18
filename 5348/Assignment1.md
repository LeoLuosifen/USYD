# Question1

### (1)

- Resource state:
  - Task Description
  - Task Progress
  - Task Due
  - Task Status
- Session state:
  - User Login Status
  - View Preference



### (2)

- System setting:
  - In the front end, to develop a page of task list that support agents can check all the tasks assigned to them; in addition, add the function of filtering and sorting that agents can check by task status, due or overdue state.
  - In the back end, to design the APIs dealing with the task query requests that return a list of tasks by user Id or other conditions; filtering the data by using SQL statements that can check the state or due.
  - About the UI, there is a dashboard to show the number of overdue tasks or tasks that are coming due, and allowing supports agents to get a quick overview of tasks.



# Question2

### (1)

Task of type A: 9 x 10 ^ 10, 4GB, 100000 IOs

Task of type B: 6 x 10 ^ 11, 12GB, 20000 IOs



Price List:

| Instance | vCPU | RAM   | Temporary storage | Cost        | IOPS |
| -------- | ---- | ----- | ----------------- | ----------- | ---- |
| D2 v3    | 2    | 8 GB  | 50 GB             | $0.188/hour | 200  |
| D4 v3    | 4    | 16 GB | 100 GB            | $0.376/hour | 400  |
| D8 v3    | 8    | 32 GB | 200 GB            | $0.752/hour | 800  |
| D16 v3   | 16   | 64 GB | 400 GB            | $1.504/hour | 1600 |



**For the task of Type A**：

- Each task of Type A is 4 GB, D2 v3 has 8 GB -> Each D2 v3 instance contains 8 / 4 = 2 Type A Task 
- Each D2 v3 instance can execute 2 x 10 ^ 9 / s instructions, each task can get 1 x 10 ^ 9 instructions, each A task requires 9 x 10 ^ 10 instructions.

- Instruction Time:
  - 9 x 10 ^ 10 / 1 x 10 ^ 9 = 90s

- IO Time:
  - Each D2 v3 can provide 200 IOPS (Each task needs 100000 IOPS) -> Each task can get 100 IOPS
  - Time: 100000 / 100 = 1000s ≈ 0.278 hour

The demand of D2 v3 instance
$$
Instances = \frac{\text{Total Type A tasks}}{\text{Tasks per instance}} = \frac{40}{2} = 20
$$
**For the task of Type B**：

- Each task of Type B is 12 GB, D16 v3 has 64 GB -> Each D16 v3 instance contains 64 / 12 = 5 Type B Task 
- Each D2 v16 instance can execute 16 x 2 x 10 ^ 9 / s instructions, each task can get 32 x 10 ^ 9 / 5 = 6.4 x 10 ^ 9 instructions, each A task requires 6 x 10 ^ 11 instructions.
- Instruction Time:
  - 6 x 10 ^ 11 / 6.4 x 10 ^ 9 = 93.75s
- IO Time:
  - Each D2 v16 can provide 1600 IOPS (Each task needs 100000 IOPS) -> Each task can get 1600 / 5 = 320 IOPS
  - Time: 20000 / 320 = 62.5s
- Because Instruction Time > IO Time; the final time is 93.75s ≈ 0.026 hour

The demand of D16 v3 instance:
$$
Instances = \frac{\text{Total Type B tasks}}{\text{Tasks per instance}} = \frac{80}{5} = 16
$$
**Total Cost**:

- Total cost of D2 v3: 

$$
\text{Total cost} = 20 \times $0.188 \times 0.278  = $1.05/hour
$$

- Total cost of D16 v3:

$$
\text{Total cost} = 16 \times $1.504 \times 0.026= $0.63/hour
$$

- Total cost:

$$
\text{Total hourly cost} = 1.05 \text{ + } 0.63 = $1.68/hour
$$

### (2) 

Try to allocate Type A tasks to other types of instances and allocate Type B tasks to a difference instance configuration, then calculate the cost. Repeating the above calculation steps for each configuration to find the total cost, finally, comparing the costs of all configurations and find which configuration provides the lowest total cost.

For example, for Type A task, trying to allocate it to other different instances

**To D4 v3**:

- Each task of Type A is 4 GB, D4 v3 has 16 GB -> Each D4 v3 instance contains 16 / 4 = 4 Type A Task 
- Each D2 v3 instance can execute 4 x 2 x 10 ^ 9 / s instructions, each task can get 4 x 2 x 10 ^ 9 / 4 = 2 x 10 ^ 9 instructions, each A task requires 9 x 10 ^ 10 instructions.

- Instruction Time:
  - 9 x 10 ^ 10 /  2 x 10 ^ 9 = 45s
- IO Time:
  - Each D4 v3 can provide 400 IOPS (Each task needs 100000 IOPS) -> Each task can get 400  / 4 = 100 IOPS
  - Time: 100000 / 100 = 1000s ≈ 0.278 hour

The demand of D4 v3 instance:
$$
Instances = \frac{40}{4} = 10
$$
**To D8 v3**:

- Each task of Type A is 4 GB, D4 v3 has 32 GB -> Each D8 v3 instance contains 32 / 4 = 8 Type A Task 
- Each D8 v3 instance can execute 8 x 2 x 10 ^ 9 / s instructions, each task can get 8 x 2 x 10 ^ 9 / 16 = 1 x 10 ^ 9 instructions, each A task requires 9 x 10 ^ 10 instructions.

- Instruction Time:
  - 9 x 10 ^ 10 /  1 x 10 ^ 9 = 90s
- IO Time:
  - Each D48 v3 can provide 800 IOPS (Each task needs 100000 IOPS) -> Each task can get 800  / 8 = 100 IOPS
  - Time: 100000 / 100 = 1000s ≈ 0.278 hour

The demand of D8 v3 instance:
$$
Instances = \frac{40}{8} = 5
$$
**Total Cost**:

- For D4 v3: Total cost = 10 x $0.376 x 0.278 = **$1.05/hour** -> Equals D2 total cost
- For D8 v3: Total cost = 5 x $0.752 x 0.278 = **$1.05/hour** -> Equals D2 total cost

Above all, the total cost doesn't change even the task A changes the instances.



For Type B task, trying to allocate it to other different instances

**To D4 v3**:

- Each task of Type B is 12 GB, D4 v3 has 16 GB -> Each D4 v3 instance contains 16 / 12 = 1 Type B Task 
- Each D4 v3 instance can execute 4 x 2 x 10 ^ 9 / s instructions, each task can get 4 x 2 x 10 ^ 9 / 1 = 4 x 2 x 10 ^ 9 instructions, each B task requires 6 x 10 ^ 11 instructions.

- Instruction Time:
  - 6 x 10 ^ 11 /  8 x 10 ^ 9 = 75s
- IO Time:
  - Each D4 v3 can provide 400 IOPS (Each task needs 20000 IOPS) -> Each task can get 400  / 1 = 400 IOPS
  - Time: 20000 / 400 = 50s
- Because Instruction Time > IO Time; the final time is 75s ≈ 0.021 hour

The demand of D4 v3 instance:
$$
Instances = \frac{80}{1} = 80
$$
**To D8 v3**:

- Each task of Type B is 12 GB, D8 v3 has 32 GB -> Each D8 v3 instance contains 32 / 12 = 2 Type B Task 
- Each D8 v3 instance can execute 8 x 2 x 10 ^ 9 / s instructions, each task can get 8 x 2 x 10 ^ 9 / 2 = 8 x 10 ^ 9 instructions, each B task requires 6 x 10 ^ 11 instructions.

- Instruction Time:
  - 6 x 10 ^ 11 /  8 x 10 ^ 9 = 75s
- IO Time:
  - Each D8 v3 can provide 800 IOPS (Each task needs 20000 IOPS) -> Each task can get 800  / 2 = 400 IOPS
  - Time: 20000 / 400 = 50s
- Because Instruction Time > IO Time; the final time is 75s ≈ 0.021 hour

The demand of D8 v3 instance:
$$
Instances = \frac{80}{2} = 40
$$


**Total Cost**:

- For D4 v3: Total cost = 80 x $0.376 x 0.021 = **$0.63/hour** -> Equals D16 total cost
- For D8 v3: Total cost = 40 x $0.752 x 0.021 = **$0.63/hour** -> Equals D16 total cost

Above all, the total cost doesn't change even the task B changes the instances.

Above of the data, no matter task A and task B assign instance configurations (expect task B can not assign to the D2 v3), the total cost is maintained at $1.68/hour, so the above plan is the best choice.



# Question 3



Your point is great, Fred. But it has some limitation, because it does not consider for other types of complicity issues. First of all, we need to consider the issue of **Read and Write Conflict**, which is when one activity is reading data, if another activity updates the same data at the same time, the read operation might get partly updated data, leading in data inconsistency. In addition, we need to make sure that **Integrity and Consistency** in the data, which is the core requirement to any system, as you said, there is a problem where only one activity could modify data, failure to handle concurrency might result in data damage or loss of consistency. So, to prevent concurrency problems, especially Read and Write Conflicts, we need to implement concurrency control methods, such as ,in the design of the database, try to design with locks and use transaction isolation.
