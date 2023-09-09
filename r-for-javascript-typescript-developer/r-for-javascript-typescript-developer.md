# Introduction

Today's article is a gentle introduction to the powerful Rust programming language for Javascript/Typescript developers. We tried to leverage your knowledge of JS and its pattern to explain the equivalents in Rust.

Rust is a systems programming language that is highly optimized for safety, speed, and concurrency. It was designed to solve common problems in systems programming, such as memory safety and data races, while still being fast and low-level enough to be used for operating systems and other performance-critical tasks. This is in contrast to Javascript and Typescript which are high-level, dynamic language that are designed to be much more flexible which means compromising on things like sheer speed and safety.

## Index of Content

This remaining part of this article explores the following:

- Variable Declaration
- Functions
- Control Struuctures
- Structs & Enums vs Objects
- Traits
- Borrowing & Ownership
- Error Handling
- Tradeoffs between the languages
- Error Typing...

---


   - Memory Safety

     - Rust has an ownership and borrowing system which help ensures that memory is managed safely and efficiently, preventing common bugs like null pointers and dangling pointers. 
     
     Here is a quick example to illustrate this:

       ```rust
       fn main() {
           let x = String::from("hello");
           let y = x; // ownership of x is moved to y
           println!("{}",y); // prints "hello"
       }
       ```
    In this example, the variable `x` owns the reference to the value "hello". In the next line where the value is assigned to `y`, x loses this ownership. Trying to access the variable `x` later down in the code like this:
    ```rs
    println!("{}", y) // error: 
    ``` 
    will result in a error. To be able to do this, we are going to be  utilizing the borrow operator `&` to borrow the value temporarily to y.
    
    ```rs
    fn main() {
           let x = String::from("hello");
           let y = &x; // ownership of x is moved to y
           println!("{}",y); // prints "hello"
           println!("{}",x); // prints "hello"
       }

    ``` 

     - In JavaScript/TypeScript, memory management is handled by a garbage collector, which can lead to performance issues and memory leaks. Here's an example of a potential memory leak in JavaScript:

       ```javascript
       function createNode() {
         let node = document.createElement("div");
         document.body.appendChild(node);
         return node;
       }

       let node1 = createNode();
       let node2 = createNode();

       // Oops, forgot to remove node1!
       ```

   - Performance

     - Rust is designed to be fast and efficient, with low-level control over memory and hardware. Here's an example of a Rust program that sorts a large array of integers:

       ```rust
       fn main() {
           let mut data = [5, 3, 1, 4, 2];
           data.sort();
           println!("{:?}", data); // prints [1, 2, 3, 4, 5]
       }
       ```

     - JavaScript/TypeScript can be slower than Rust due to its dynamic nature, but it has improved significantly with the introduction of features like just-in-time (JIT) compilation. Here's an example of a JavaScript program that sorts an array:

       ```javascript
       let data = [5, 3, 1, 4, 2];
       data.sort();
       console.log(data); // prints [1, 2, 3, 4, 5]
       ```

   - Concurrency

     - Rust's ownership and borrowing system make it easy to write concurrent code that is safe and efficient. Here's an example of a Rust program that spawns multiple threads to calculate the sum of a large array:

       ```rust
       use std::thread;

       fn main() {
           let data = vec![1, 2, 3, 4, 5];
           let mut handles = vec![];

           for chunk in data.chunks(2) {
               let handle = thread::spawn(move || {
                   chunk.iter().sum::<i32>()
               });
               handles.push(handle);
           }

           let sum = handles.into_iter().map(|h| h.join().unwrap()).sum::<i32>();
           println!("{}", sum); // prints 15
       }
       ```

     - JavaScript/TypeScript also support concurrency through features like Web Workers and async/await. Here's an example of a TypeScript program that uses async/await to calculate the sum of a large array:

       ```typescript
       async function sum(data: number[]): Promise<number> {
         if (data.length <= 1000) {
           return data.reduce((acc, val) => acc + val, 0);
         }

         let mid = Math.floor(data.length / 2);
         let left = data.slice(0, mid);
         let right = data.slice(mid);

         let sumLeft = sum(left);
         let sumRight = sum(right);

         return sumLeft + sumRight;
       }

       let data = [1, 2, 3, 4, 5];
       sum(data).then((result) => console.log(result)); // prints 15
       ```

   - Error Handling

     - Rust's error handling system is based on the Result type, which allows for explicit handling of errors and prevents code from crashing at runtime. Here's an example of a Rust program that reads a file and handles errors:

       ```rust
       use std::fs::File;

       fn main() {
           let file = File::open("foo.txt");
           match file {
               Ok(f) => println!("File opened successfully"),
               Err(e) => println!("Error opening file: {}", e),
           }
       }
       ```

     - JavaScript/TypeScript also support error handling through try/catch blocks and promises. Here's an example of a TypeScript program that reads a file and handles errors:

       ```typescript
       import { promises as fs } from "fs";

       async function main() {
         try {
           let file = await fs.open("foo.txt");
           console.log("File opened successfully");
         } catch (e) {
           console.log(`Error opening file: ${e}`);
         }
       }

       main();
       ```

   - Type Safety

     - Rust is a statically typed language, which means that all types are known at compile time and checked for correctness before the program runs. This prevents many common bugs and makes it easier to reason about code. Here's an example of a Rust program that uses a struct to represent a user:

       ```rust
       struct User {
           name: String,
           age: u32,
       }

       fn main() {
           let user = User {
               name: String::from("Alice"),
               age: 30,
           };

           println!("{} is {} years old", user.name, user.age);
       }
       ```

     - TypeScript is also a statically typed language that adds optional type annotations to JavaScript. This allows for type checking at compile time and can help prevent errors. Here's an example of a TypeScript program that uses an interface to represent a user:

       ```typescript
       interface User {
         name: string;
         age: number;
       }

       let user: User = {
         name: "Alice",
         age: 30,
       };

       console.log(`${user.name} is ${user.age} years old`);
       ```

4. Tradeoffs between the languages

   - Rust's focus on safety and performance comes at a cost of increased complexity and a steeper learning curve. It is also less flexible than dynamic languages like JavaScript/TypeScript and may not be the best choice for all projects.
   - JavaScript/TypeScript areeasier to learn and use, and they have a larger ecosystem and community, making it easier to find libraries and resources. However, they may not be as performant or safe as Rust, and they can be more prone to errors and bugs.

5. Conclusion
   - In conclusion, Rust and TypeScript/JavaScript are two different languages with different strengths and weaknesses. Rust offers strong memory safety and performance guarantees, while TypeScript/JavaScript offer flexibility and ease of use. When deciding which language to use for a project, it's important to consider the specific needs and requirements of the project, as well as the skills and experience of the development team. In some cases, it may be beneficial to use both Rust and TypeScript/JavaScript together, for example by using Rust for performance-critical parts of a web application and TypeScript/JavaScript for the front-end.
