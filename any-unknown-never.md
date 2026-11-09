Introduction
In TypeScript, there are special types that sit at the very top and very bottom of the type system. Understanding any, unknown, and never helps you figure out how TypeScript checks your code for safety.

The Core Concepts
1. unknown
unknown is the top type. This means any value can be put into an unknown variable. However, before you can actually use that value, TypeScript forces you to prove what type it is (called "narrowing").

TypeScript
let u: unknown = "text";

(must check the type first)
if (typeof u === "string") {
  u.toUpperCase();   (TypeScript now knows it's a string)
}
2. any
any completely turns off TypeScript's type checking. You can do anything with it, but if you make a mistake, TypeScript won't warn you—it might crash your app when it actually runs.

TypeScript
let a: any = "text";
a.toFixed();        
(Compiles fine, but crashes at runtime because strings don't have toFixed()!)


3. never 
never is the bottom type. It represents something that should never happen. It is mostly used for functions that throw an error or loop forever (meaning they never return a value), or for checking that you handled every possible option in a list.

TypeScript
function fail(message: string): never {
  throw new Error(message);     
  (This function never successfully finishes and returns.)
  
}
Why Use unknown Instead of any?
any is dangerous because it lets bugs hide. If you make a typo, any won't warn you, and the error will only show up when your user runs the app.

unknown keeps you safe. It says, "I don't know what this data is yet, but TypeScript, please make sure I check it before I use it."

Which One Should Use?
Avoid any as much as possible, unless you are dealing with messy legacy code or migrating old JavaScript.
Use unknown when you genuinely don't know what type a value will be (like data coming from an API or user input).

Use never for extreme edge cases, like functions that throw errors or ensuring your switch statements handle every single possibility.

Conclusion
Whenever you aren't sure what type something is, prefer unknown to keep your code safe, and reserve never strictly for impossible states.