# Java Fundamentals Lists, Hashmaps and Generics Workshop

## Learning Objectives
- Use Lists to store and manipulate data
- Use generic typing to define the datatype of items stored in a List
- Use HashMaps to store and access key-value data pairs
- Use generic typing to define types contained in a HashMap

## ArrayLists

So far the only data structure we've really used has been the Array, these are useful as they are efficient both in terms of memory and access, but sometimes we need to use a more dynamic structure which we can define the size of as we go along. This is where the ArrayList comes in, it works similarly to an Array, but you don't have to specify how many items it will contain in advance.

Think back to the Chat-Bot we created previously. What if we could easily store all of the text entered by the user and the Chat-Bot responses into an ArrayList that we could then output, save or query at a later point in order to see what the conversation looked like.

Let's build that now.

```java
package com.booleanuk;

import java.util.ArrayList;
import java.util.Random;
import java.util.Scanner;

public class ChatBot {
    ArrayList<String> conversationLog = new ArrayList<>();
    Scanner input = new Scanner(System.in);
    String[] responses = {"That's interesting, please continue.", "Interesting, what makes you think that?",
                        "Please expand on that point?", "Why do you think that?", "Are there any other possibilities?"};
    Random randomiser = new Random();

    public void chat() {
        String userInput = "";
        String output = "";
        do {
            output = this.responses[randomiser.nextInt(this.responses.length)];
            System.out.println(output);
            this.conversationLog.add(output);
            userInput = this.input.nextLine();
            this.conversationLog.add(userInput);
        } while (!userInput.toLowerCase().equals("q"));
        this.conversationLog.remove(this.conversationLog.size()-1);

        
        System.out.println();
        System.out.println("Conversation as follows");
        System.out.println();
        for (String theOutput : this.conversationLog) {
            System.out.println(theOutput);
        }
    }
}
```


To access a value at a particular index we use `myArrayList.get(3)` to change that value we would use set `myArrayList.set(3, "Some Text")`.

We can add new items at the end of the ArrayList or add them at a given index. We can remove the first instance of an object, or we can remove an item at a given index.

[Java ArrayList Documentation](https://docs.oracle.com/en/java/javase/18/docs/api/java.base/java/util/ArrayList.html)

## Activity

Create a multiple choice quiz which asks the user how many maths questions they want to answer and then randomly generates multiplication questions for them to answer. It should create two ArrayLists - one for the actual answers and one for the answers given by the user. When the questions are complete the program will then iterate over the two lists comparing answers and awarding them points. It should then display a message which is different depending on what proportion of the questions the user got correct.

## HashMaps

HashMaps are a way of storing data in key-value pairs. The keys all need to be of the same data type and the data needs to be of the same data type (although the two can be different from each other). Keys have to be unique, but the data can include repetitions.

Let's build a simple program that stores user emails and their corresponding names into a HashMap.

```java
package com.booleanuk;

import java.util.HashMap;

public class EmailStore {
    HashMap<String, String> nameStore = new HashMap<>();

    public EmailStore() {
        this.nameStore.put("dave@example.com", "Dave");
        this.nameStore.put("ed@boolean", "Edward");
        this.nameStore.put("nigel@c-sharp.com", "Nigel");
    }
}
```

We can check for individual users or output the whole thing easily enough:

```java
package com.booleanuk;

public class Main {
    public static void main(String[] args) {
        EmailStore theStore = new EmailStore();
        System.out.println(theStore.nameStore.get("dave@example.com"));
        System.out.println(theStore.nameStore);
    }
}
```

## Activity

Use the reference at [HashMap Documentation](https://docs.oracle.com/en/java/javase/18/docs/api/java.base/java/util/HashMap.html) to help add in methods that will:

- Modify the user if their email address already exists.
- Create a new user if their email doesn't exist.
- Delete a given user.
- Add a new user.
- Add a new user interactively.
- Any other methods you can think of.


## Generics

Generics is the posh term we use to describe putting the data types into angle brackets when defining ArrayLists, HashMaps and similar data structures. In theory, you could implement your own data structures that take Generic classes and then be able to reuse them with multiple data types, that is beyond the scope of this course, however.

## Activity

Build Library and Book classes that uses an ArrayList of Books to hold the list of books in the library.

Have a menu that runs when you run the program and allows you to do various things, including add a new book to the library, where the new book is generated by getting appropriate inputs from the user to populate the book interactively. The program should let you search to see if a book is in the library and list books by certain authors or other criteria.
