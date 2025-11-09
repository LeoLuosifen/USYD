# Exercise 1. Mobile Computing

1、The most import stakeholder(s) in the mobile ecosystem is/are:

(A)	App Developers

(B)	Users

(C)	Mobile Operators

(D)	All of the above	✅

2、What does password primarily contribute to in the CIA triad?

(A)	Availability

(B)	Confidentiality	✅

(C)	Integrity

(D)	None of the above

- **C - Confidentiality**

- **I - Integrity**

- **A - Availability**

The primary function of a password is to prevent unauthorized individuals from accessing systems or information through an authentication mechanism, thereby safeguarding the confidentiality of information.

# Exercise 2. Designing Mobile Applications

3、The notifications should be designed carefully

(A)	to repeat as frequently as possible until the user pays attention

(B)	with actionable controls	✅

(C)	to get user attention at any time of the day

(D)	show as much as information as possible

***to repeat as frequently*** ❌,  ***at any time of the day*** ❌, ***as much as information*** ❌

4、McGurk effect is a good example of multimodal effects

(A)	Yes	✅

(B)	No

5、To manage attention, it is important to design interfaces that have

(A)	as much as possible spacing between elements

(B)	high colour contrast	✅

(C)	faster response time

(D)	the minimum amount of network data

***manage attention*** -> important information is **easily noticed**.

6、In *Norman’s conceptual framework* :

(A)	Designer’s Model should match User’s Model	✅

(B)	System Image should be minimized

(C)	Users are discouraged to create mental models

(D)	Designers are discouraged to create mental models

> Norman's Core Principles:
>
> “The **designer’s model** should be accurately communicated through the **system image**, so that the **user’s model** matches it.”

# Exercise 3. React Native - General

7、The Figure 3.1 shows an example how an app uses Context in React Native. **Context.Provider** indicates which component the context provider wraps. Please select the correct answer about which component can have access to the Shared Data Context.

![Figure_3.1](./Figure_3.1.png)

(A)	Neither Login or Profile components can have access

(B)	Only Profile component can have access

(C)	Only _Layout(user) has access

(D)	Can be access from Login component	✅

```scss
_Layout(app)
 ├── _Layout(user) ← Context.Provider here
 │    ├── Login
 │    └── Register
 └── _Layout(todos)
      ├── Add Todo
      ├── Todo
      └── Profile

```

# Exercise 4. React Native - Architecture

8、Shadow thread in React Native is responsible for:

(A)	Event Handling

(B)	Manage Layout	✅

(C)	Processing style changes

(D)	Rendering user interface



![Figure_4.1](./Figure_4.1.png)

9、All JS codes must run through:

(A) Call Stack	✅

(B) Task Queue

(C) MicroTask Queue

(D) None of the above

>Whether it's synchronous code or asynchronous callbacks, they must ultimately enter the call stack to be executed.

10、If all two queues and call stack has code to be executed, priority will be given to

(A) Call Stack

(B) Task Queue

(C) MicroTask Queue	✅

(D) None of the above

```html
Call Stack → MicroTask Queue → Task Queue
```

11、Task Queue will be used when:

(A) There is a call back function	✅

(B) Anything after an await

(C) Promise is returned

(D) None of the above

### 🔹 A typical scenario for the Task Queue:

- `setTimeout(callback, 0)`
- `setInterval(callback, n)`
- `setImmediate(callback)`（Node.js）
- `I/O callbacks`
- `UI rendering callbacks`



# Exercise 5. package.json

The code Listing-1 below shows an example package.json file of a project developed by a student. You can assume all the versions listed are accurate and all the necessary libraries are imported.

![Listing_1](./Listing_1.png)

12、Code Listing-1 has,

(A) Errors

(B) No errors	✅

13、The project that has Listing-1 can be started with the command

(A) npm start	✅

(B) npm run start

(C) npm run dependencies

(D) npm install

# Exercise 6. Using useState Hook