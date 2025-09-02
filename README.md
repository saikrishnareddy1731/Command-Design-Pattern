# Command Design Pattern in Java

## Overview

The **Command Pattern** is a **behavioral design pattern** that turns a request into a standalone object containing all the information about the request.  
This allows you to parameterize methods with different requests, delay execution, queue requests, or support undoable operations.

---

## Key Points

- Encapsulates a **request as an object**.
- Decouples the **sender (Invoker)** from the **receiver**.
- Useful for implementing **undo/redo**, **logging**, and **transactional behavior**.

---

## Real-world Example

Imagine a **text editor** where you want to:

- **Open a file**
- **Save a file**

Each action is represented as a **command object**.  
The client sends commands to the **Invoker** (`TextFileOperationExecutor`), which executes them on the **Receiver** (`TextFile`).  

---

## Components

1. **Command Interface** → Declares the `execute()` method.  
   Example: `TextFileOperation`

2. **Concrete Commands** → Implement command actions.  
   Examples: `OpenTextFileOperation`, `SaveTextFileOperation`

3. **Receiver** → The actual object performing the work.  
   Example: `TextFile`

4. **Invoker** → Executes commands and may keep history.  
   Example: `TextFileOperationExecutor`

5. **Client** → Creates and sends commands.  
   Example: `Main`

---

## UML Diagram

```mermaid
classDiagram
    direction LR

    TextFileOperation <|.. OpenTextFileOperation
    TextFileOperation <|.. SaveTextFileOperation
    TextFileOperationExecutor --> TextFileOperation : executes
    OpenTextFileOperation --> TextFile : calls
    SaveTextFileOperation --> TextFile : calls
    Main --> TextFileOperationExecutor : uses

    class TextFileOperation {
        <<interface>>
        +execute() String
    }

    class OpenTextFileOperation {
        -textFile: TextFile
        +execute() String
    }

    class SaveTextFileOperation {
        -textFile: TextFile
        +execute() String
    }

    class TextFile {
        -name: String
        +open() String
        +save() String
    }

    class TextFileOperationExecutor {
        -textFileOperations: List~TextFileOperation~
        +executeOperation(op: TextFileOperation) String
    }

    class Main {
        +main()
    }
