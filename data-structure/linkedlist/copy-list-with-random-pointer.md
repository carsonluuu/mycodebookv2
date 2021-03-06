# Copy List with Random Pointer

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

## Note

```
第一遍扫的时候巧妙运用next指针， 开始数组是1->2->3->4。
然后扫描过程中 先建立copy节点 1->1`->2->2`->3->3`->4->4`,
然后第二遍copy的时候去建立边的copy， 拆分节点, 一边扫描一边拆成两个链表，
这里用到两个dummy node。第一个链表变回 1->2->3 , 然后第二变成 1`->2`->3`
```

`iter.next.random = iter.random.next`

I believe now points to the "newly" created node, i.e. the copy, not the original node, which is later removed.

Need deep copy, which means a new node to be created.

## Code

```java
private void copyNext(RandomListNode head) {
    while (head != null) {
        RandomListNode newNode = new RandomListNode(head.label);
        newNode.next = head.next;
        newNode.random = head.random;
        head.next = newNode;
        head = head.next.next;   
    }
}

private void copyRandom(RandomListNode head) {
    while (head != null) {
        if (head.next.random != null) {
            head.next.random = head.random.next;
        }
        head = head.next.next;
    }
}

private RandomListNode splitList(RandomListNode head) {
    RandomListNode newHead = head.next;
    while (head != null) {
        RandomListNode temp = head.next;
        head.next = temp.next;
        if (temp.next != null) {
            temp.next = temp.next.next;
        }
        head = head.next;
    }

    return newHead;
}

public RandomListNode copyRandomList(RandomListNode head) {
    if (head == null) {
        return head;
    }

    copyNext(head);
    copyRandom(head);

    return splitList(head);
}
```
