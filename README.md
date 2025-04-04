# Renton Technical College CSI-246

<div align="center">  
    <img src="logo.jpg" alt="Logo">
    <h3 align="center">Guided Activity 1</h3>
</div>

This repository is a part of CSI-246 at Renton Technical College.

## Part 1: Setting Up Your TypeScript Environment

### What is TypeScript?
TypeScript is a superset of JavaScript that adds static typing to the language. This means:
- All JavaScript code is valid TypeScript code
- TypeScript adds additional features like type checking
- TypeScript code must be compiled into JavaScript to run

1. Clone the repository to your local machine.
2. Make note of the folder where you cloned the repository.
3. Open the local repository folder in VS code and follow the instructions to complete the assignment.

### Installing Required Tools

Before we begin working with TypeScript, we need to make sure we have the necessary tools installed:

1. Verify Node.js installation:
```bash
node --version
```

2. Install TypeScript globally:
```bash
npm install -g typescript
```

3. Verify TypeScript installation:
```bash
tsc --version
```

### Creating a TypeScript Project

1. Navigate to your repository folder using the terminal or PowerShell.

2. Initialize a new Node.js project:
```bash
npm init -y
```

3. Install TypeScript as a development dependency:
```bash
npm install --save-dev typescript @types/node
```

4. Create a TypeScript configuration file:
```bash
tsc --init
```

### Understanding tsconfig.json

The `tsconfig.json` file controls how TypeScript compiles your code. Let's look at some important options:

```json
{
    "compilerOptions": {
        // Specifies which version of JavaScript to compile to
        "target": "es2016",
        
        // Determines how modules are handled
        "module": "commonjs",
        
        // Enables all strict type checking options
        "strict": true,
        
        // Allows default imports from modules with no default export
        "esModuleInterop": true,

        // Whether to allow JS files to be compiled
        "allowJs": true
    }
}
```

## Part 2: Your First TypeScript Program

Let's write and run your first TypeScript program.

1. Create a new file called `hello.ts`
2. Copy the following code into `hello.ts`:


```typescript
// ==========================================
// Basic Types and Type Checking Example
// ==========================================

// TypeScript enforces type checking at compile time
// Let's see some examples of type checking in action

// 1. Basic type annotations
let studentName: string = "John";
let studentAge: number = 20;
let isEnrolled: boolean = true;

// This will work fine
studentName = "Jane";

// This will cause a compile error - uncomment to see:
// studentName = 42;  // Error: Type 'number' is not assignable to type 'string'
// studentAge = "twenty";  // Error: Type 'string' is not assignable to type 'number'

// 2. The 'any' type - turns off type checking
// WARNING: Use sparingly! It defeats the purpose of TypeScript
let flexibleVar: any = 4;
flexibleVar = "Now I'm a string";  // This works
flexibleVar = true;                // This also works

// 3. Type inference
// TypeScript can guess types based on the initial value
let inferredString = "This is a string";  // TypeScript knows this is a string
// Uncomment to see the error:
// inferredString = 42;  // Error: Type 'number' is not assignable to type 'string'

// 4. Functions with type annotations
function calculateGrade(score: number, bonus: number): string {
    const totalScore = score + bonus;
    
    if (totalScore >= 90) return "A";
    if (totalScore >= 80) return "B";
    if (totalScore >= 70) return "C";
    return "F";
}

// This works:
console.log(calculateGrade(85, 5));  // "B"

// Uncomment these to see the errors:
// console.log(calculateGrade("85", 5));  // Error: Argument of type 'string' not assignable to type 'number'
// console.log(calculateGrade(85));       // Error: Expected 2 arguments, but got 1

// 5. Union Types - allowing multiple types
let studentId: string | number = "A123";  // Can be string
studentId = 123;                          // Or number
// studentId = true;                      // Error: Type 'boolean' not assignable to type 'string | number'

```

Now let's compile and test your code:

1. First, compile the TypeScript file:
```bash
tsc hello.ts
```

2. Run the compiled JavaScript:
```bash
node hello.js
```

3. You should see the grade "B" printed to the console.

4. Now, let's see TypeScript's error checking in action. Uncomment these lines in hello.ts:
```typescript
// console.log(calculateGrade("85", 5));
// console.log(calculateGrade(85));
```

5. Try compiling again:
```bash
tsc hello.ts
```

6. You should see error messages about type mismatches. This is TypeScript helping you catch errors before they happen at runtime!

7. Comment out the error lines again before moving on.


## Part 3: Working with Interfaces

Now that you understand basic types, let's explore interfaces.

1. Create a new file called `interfaces.ts`
2. Copy the following code into `interfaces.ts`:

```typescript
// ==========================================
// Interfaces Example
// ==========================================

// Interfaces define the shape that our objects must have
// Think of them as contracts that objects must follow

// 1. Basic Interface
interface Student {
    name: string;
    age: number;
    courses: string[];
    graduationYear?: number;  // Optional property (notice the ?)
}

// This works - has all required properties
const goodStudent: Student = {
    name: "John",
    age: 20,
    courses: ["TypeScript", "JavaScript"]
    // graduationYear is optional, so we can omit it
};

// Uncomment to see errors:
// Missing required properties
// const badStudent: Student = {
//     name: "Jane"
//     // Error: Missing properties 'age' and 'courses'
// };

// Wrong type for a property
// const wrongStudent: Student = {
//     name: "Bob",
//     age: "twenty",  // Error: Type 'string' not assignable to type 'number'
//     courses: ["TypeScript"]
// };

// 2. Interface with Methods
interface Calculator {
    add(x: number, y: number): number;
    subtract(x: number, y: number): number;
}

// Implementing an interface
class BasicCalculator implements Calculator {
    add(x: number, y: number): number {
        return x + y;
    }
    
    subtract(x: number, y: number): number {
        return x - y;
    }
}

// Using the calculator
const calc = new BasicCalculator();
console.log(calc.add(5, 3));      // 8
console.log(calc.subtract(5, 3));  // 2

// 3. Extending Interfaces
interface Animal {
    name: string;
    makeSound(): void;
}

interface Dog extends Animal {
    breed: string;
}

// This must implement all properties from both interfaces
const myDog: Dog = {
    name: "Rex",
    breed: "German Shepherd",
    makeSound(): void {
        console.log("Woof!");
    }
};

```

Let's test the interfaces code:

1. Compile the TypeScript file:
```bash
tsc interfaces.ts
```

2. Run the compiled JavaScript:
```bash
node interfaces.js
```

3. You should see the calculator results (8 and 2) and a "Woof!" in the console.

4. Now let's see what happens when we break the interface contracts. Uncomment these sections in interfaces.ts:

```typescript
// Uncomment these lines to see the errors:
const badStudent: Student = {
    name: "Jane"
    // Error: Missing properties 'age' and 'courses'
};

// Uncomment these lines to see more errors:
const wrongStudent: Student = {
    name: "Bob",
    age: "twenty",  // Error: Type 'string' not assignable to type 'number'
    courses: ["TypeScript"]
};
```

5. After uncommenting these sections, try to compile the TypeScript file:
```bash
tsc interfaces.ts
```

6. You should see error messages like:
   - Property 'age' is missing in type '{ name: string; }' but required in type 'Student'
   - Property 'courses' is missing in type '{ name: string; }' but required in type 'Student'
   - Type 'string' is not assignable to type 'number'

7. These errors demonstrate TypeScript's static type checking, which catches these issues before runtime.

8. To see the working code again, comment out the error examples and run:
```bash
tsc interfaces.ts
node interfaces.js
```

This exercise helps you understand how TypeScript enforces the contracts defined by interfaces, preventing common programming errors that would otherwise only be caught at runtime.

## Part 4: Advanced Types
Create a file called `advanced.ts`:
```typescript
// ==========================================
// Advanced Types Example
// ==========================================
// 1. Enum Example
// Enums create a set of named constants
enum CourseStatus {
    Active = "ACTIVE",
    Completed = "COMPLETED",
    Withdrawn = "WITHDRAWN"
}
// Using the enum
let myStatus: CourseStatus = CourseStatus.Active;
console.log(myStatus);  // "ACTIVE"
// This will cause an error - uncomment to see:
// myStatus = "ACTIVE";  // Error: Type '"ACTIVE"' is not assignable to type 'CourseStatus'
// 2. Type Aliases and Union Types
// Creating a custom type that can be reused
type GradeInput = number | string;
function processGrade(grade: GradeInput): number {
    if (typeof grade === "string") {
        // Convert letter grade to number
        switch (grade.toUpperCase()) {
            case "A": return 4.0;
            case "B": return 3.0;
            case "C": return 2.0;
            default: return 0.0;
        }
    }
    return grade;
}
console.log(processGrade("A"));    // 4.0
console.log(processGrade(3.5));    // 3.5
// This will cause an error - uncomment to see:
// console.log(processGrade(true));  // Error: Argument of type 'boolean' not assignable
// 3. Intersection Types
// Combining multiple types into one
type Teacher = {
    name: string;
    subject: string;
};
type Employee = {
    id: number;
    department: string;
};
// Combining both types
type TeachingEmployee = Teacher & Employee;
const teacher: TeachingEmployee = {
    name: "Mr. Smith",
    subject: "TypeScript",
    id: 123,
    department: "Computer Science"
};
// This will cause an error - uncomment to see:
// const invalidTeacher: TeachingEmployee = {
//     name: "Mr. Jones",
//     subject: "JavaScript"
//     // Error: Missing properties from Employee type
// };
// Try compiling with: tsc advanced.ts
// Then uncomment the error examples to see type checking in action
```

### Union Types Explained

Union types, represented by the `|` symbol, allow a variable to hold values of multiple types. They're one of TypeScript's most powerful features for creating flexible yet type-safe code.

In the example above, `type GradeInput = number | string;` creates a type that can accept either numbers (like 3.5) or strings (like "A").

#### How Union Types Work:

1. **Declaration**: Use the pipe (`|`) symbol to combine types
   ```typescript
   let id: string | number;
   id = "abc123";  // Valid
   id = 456789;    // Also valid
   id = true;      // Error: Type 'boolean' not assignable
   ```

2. **Type Narrowing**: TypeScript automatically narrows the type within conditional blocks
   ```typescript
   function printId(id: string | number) {
     if (typeof id === "string") {
       // TypeScript knows id is a string here
       console.log(id.toUpperCase());
     } else {
       // TypeScript knows id is a number here
       console.log(id.toFixed(2));
     }
   }
   ```

3. **Type Guards**: Use checks like `typeof`, `instanceof`, or custom functions to determine types
   ```typescript
   function isString(x: any): x is string {
     return typeof x === "string";
   }
   ```

4. **Literal Type Unions**: You can create unions of specific values
   ```typescript
   type Direction = "north" | "south" | "east" | "west";
   let heading: Direction = "north";  // Valid
   heading = "northeast";  // Error: Type '"northeast"' not assignable
   ```

Union types are especially useful for:
- Functions that can handle multiple input types
- Variables that might hold different types of values
- Creating type-safe APIs with multiple valid options
- Error handling with discriminated unions

In the `processGrade` example, the function can process both numeric grades (directly) and letter grades (by converting them), making your code more flexible while maintaining type safety.
## Part 5: Understanding the TypeScript Compilation Process

When you run `tsc filename.ts`, TypeScript:

1. **Checks your code for errors:**
   - Type mismatches
   - Missing properties
   - Incorrect function calls
   - Syntax errors

2. **If it finds errors:**
   - Shows error messages
   - Won't generate JavaScript code until errors are fixed

3. **If no errors:**
   - Removes all TypeScript-specific code (types, interfaces, etc.)
   - Generates regular JavaScript that can run in any JavaScript environment

Try this process:
1. Run `tsc filename.ts` on the working examples
2. Uncomment some error examples
3. Run `tsc filename.ts` again to see the errors
4. Fix the errors and compile again

### Final Commit

1. Stage changes:
```bash
git add .
```

2. Create commit:
```bash
git commit -m "Guided Activity 1 Complete"
```

3. Push to GitHub:
```bash
git push
```

## Key Takeaways

1. TypeScript Advantages:
   - Catches errors before runtime
   - Makes code more self-documenting
   - Provides better development tools support

2. Core Concepts:
   - Type annotations prevent errors
   - Interfaces define object shapes
   - TypeScript compiles to regular JavaScript
   - Error messages help find problems quickly

3. Best Practices:
   - Use type annotations consistently
   - Avoid the 'any' type when possible
   - Let TypeScript infer types when obvious
   - Use interfaces for complex objects

If you have any questions about this assignment, please reach out to your instructor or TA for this course.
