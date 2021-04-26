---
layout: post
title:  "LeetCode: Delete Node in a Linked List"
category: leetcode
---

In preparation for interviews, I've been making my way through coding challenges on LeetCode.

This is one of my favorite questions that I've solved so far.

# The Question

> ## Delete Node in a Linked List
>
> Write a function to **delete a node** in a singly-linked list. You will **not** be given access to the `head` of the list, instead you will be given access to the node to be deleted directly.
>
> It is guaranteed that **the node to be deleted** is not a tail node in the list.

This question is simple and it's mostly easy to understand what is being asked.

The only point of clarification I wanted to know when reading it was, will the node to be deleted be the head? If I was working with an interviewer on this question, that would be something I would ask for clarification about. Perhaps this is implied in the prompt when it states:
> You will **not** be given access to the `head` of the list

but this was not 100% clear to me. One more sentence at the end would do the trick:
> It is also guaranteed that **the node to be deleted** is not the head node in the list.

The reason this is important is because our work is much easier if we don't have to worry about the head and tail nodes of the list. There's less that needs to be done.

So now the question becomes: if we don't have access to the head of the list, and the list is singly-linked, how can we delete the node in question?

# Approaching a Solution

If you've done any work with Linked Lists, you'll know that the way to delete a node is to change the previous node's next pointer to the node-to-be-deleted's next node pointer. Since the pointers link the list, if we alter the ones linking to and from the node-to-be-deleted, we effectively "cut" the node-to-be-deleted out of the linked list.

In a singly-linked list, if we need to find a specific value and we don't know where it is, we need to start at the head node.

If we know the head node, we traverse the list until we find the value of the node-to-be-deleted (as the question states that each of the values in the list are unique). We could keep track of the next pointer, until it's pointing at the node with the value we need to delete, and then simply change that pointer to the node-to-be-deleted's next node pointer.

Another method we could use, if this was a doubly-linked list, is a previous node pointer, since doubly-linked list nodes have both next and previous node pointers. This would make our job very easy, since we're given the node to be deleted and we'd instantly have the information about the previous and next node pointers we'd need to change to delete the node-to-be-deleted.

Unforutnately, this is not a doubly-linked list.

Here's what we've got: a value, a pointer to the next node, and a setter method.

    /**
    * Definition for singly-linked list.
    * public class ListNode {
    *     int val;
    *     ListNode next;
    *     ListNode(int x) { val = x; }
    * }
    */


# The Solution

The reason I liked this question was because it got me thinking differently. It challenged the patterns I use when I approach coding questions. I think the best coding questions are the ones that are challenging yet simple to understand, offer satisfaction upon reaching a solution, and give you the confidence to keep going.

While thinking about this question, I took a good amount of time trying to figure out how I could figure out what the previous node was. And then I looked at what information I had access to, rather than what information I didn't.

    node.val
    node.next
    //the rest of the list
The big realization was this: I don't know what the previous node is but I do know that it is pointing to the node-to-be-deleted. That's only a dead-end if I want to try and change that to the node after the node-to-be-deleted. So what can be done if that can't be changed?

Perhaps the title, "Overwrite Node in a Linked List" for the question would make more sense.

Given that we can't change the previous node's next pointer, the node-to-be-deleted is not the one that can be deleted. It would be more accurate to refer to the node-to-be-deleted as the node-to-be-overwritten, while the node *after* the node-to-be-overwritten is actually the node-to-be-deleted.

Perhaps this is best illustrated with a look at the solution:

    class Solution {
        public void deleteNode(ListNode node) {
            node.val = node.next.val; //overwrite the nodes value with the next node's value
            node.next = node.next.next; //change the pointer of the node to the next node's next pointer, deleting the next node that was just effectively "copied"
        }
    }

Arriving at this solution taught me that sometimes, I approach these questions too literally. I realize this may be a simple question, but I found the experience of working on it to be invaluable.

Thanks for reading and happy coding!




