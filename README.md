# Project-README-with-Demo
I built this using a Binary Search Tree (BST). This gives us some cool advantages, like being able to traverse the queue in perfect order and handling duplicate priorities in a really unique way.

Standard priority queues are great, but sometimes you need to see what's going on inside. Because this is built on a BST, the data is always sorted internally. I've also added a special twist to handle duplicates: instead of making the tree deeper and slower when priorities match, I chain them together. This keeps the tree balanced and operations fast!

Key Features

Smart Duplicate Handling: If two items have the same priority, they don't clutter the tree structure. They get linked together in a mini-chain right at that node.

I've implemented the "Rule of Three" (Destructor, Copy Constructor, Assignment Operator) to ensure deep copies work perfectly and there are no memory leaks.

You can iterate through the entire queue from start to finish without removing items, using the begin() and next() helper functions.

It's a BST, but with a slight modification to the Nodes.

Every NODE has the usual left, right, and parent pointers, but also a link pointer.

Unique Priority: Goes into the tree normally (left for smaller, right for larger).

Duplicate Priority: If I try to add a priority that already exists, I just attach it to the link of the existing node.

This keeps the tree height (H) minimal, which is crucial for keeping search times fast.

Getting Started

1. Installation

Just include prqueue.h into your project folder and include it.

#include "prqueue.h"


2. Basic Usage

Here is a quick example of how to set up a queue of names. Note that in this implementation, lower numbers = higher priority (processed first).

#include <iostream>
#include <string>
#include "prqueue.h"

using namespace std;

int main() {
    // Create a queue to store names
    prqueue<string> tasks;

    cout << "Adding tasks..." << endl;

    // Format: enqueue(Value, Priority)
    tasks.enqueue("Fix critical bug", 1);   // Priority 1 (Highest)
    tasks.enqueue("Write documentation", 2);
    tasks.enqueue("Get coffee", 1);         // Duplicate priority!

    // Let's see who is up first
    // This should be one of the Priority 1 items (usually FIFO for duplicates)
    cout << "Next task: " << tasks.peek() << endl; 

    // Process the queue
    while(tasks.size() > 0) {
        cout << "Doing: " << tasks.dequeue() << endl;
    }

    return 0;
}


3. Iterating without Dequeuing

Want to print the whole list without destroying the queue? You can do that too:

tasks.begin(); // Rewind to the start
string taskName;
int priority;

// Loop through everything
while (tasks.next(taskName, priority)) {
    cout << "[" << priority << "] " << taskName << endl;
}
