## 206. Reverse a linked List

still awful at manipulating given class/functions. This one recursively just sees if a node has a next, then passes along the "new_head" pointer down the list as well as changes the next values pointer to be the current node, reversing the list.

    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head:
            return None

        new_head = head

        if head.next:
            new_head = self.reverseList(head.next)
            head.next.next = head

        head.next = None

        return new_head


## 2095. Delete Middle Node of Linked List

we make a fast and a slow pointer.
while fast is not at the end( while fast.next) we jump the fast by 2 and the slow by 1. Once the fast is at the end the slow is at the middle and we just set slow.next = slow.next.next thus skipping the slow.next current value and "deleting" it.

    if not head.next:
        return None
    slow,fast = head,head.next.next
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    slow.next = slow.next.next
    return head

## 328. Odd Even Linked List

I was on the right track but was getting an infinite loop. In this problem we want to create even and odd, then leapfrog them until there is no more nodes. Then set the final odd.next to the even_head variable stored earlier.

    if not head or not head.next:
        return head

    odd_head, even_head = head, head.next
    odd = odd_head
    even = even_head

    while even and even.next:
        odd.next = even.next
        odd = odd.next
        even.next = odd.next
        even = even.next
    odd.next = even_head

    return odd_head

Note: I feel like this solution only works because there is always an odd number of nodes in the test lists even though that wasn't stated in the problem. Confirmed by doing a count and returning an obvious wrong value if count is even.


## 2130. Maximum Twin Sum of Linked List

I was trying to make a new linked list, instead we want to reverse the first half of the list while using a fast to traverse to the end, then we just iterate throught the last half and backwards through the first half, adding the values together and comparing to the max sum.

    def pairSum(self, head: Optional[ListNode]) -> int:
        slow, fast = head, head
        prev = None
        while fast and fast.next:
            fast = fast.next.next

            tmp = slow.next
            slow.next = prev
            prev = slow
            slow = tmp

        res = 0
        while slow:
            res = max(res, prev.val + slow.val)
            prev = prev.next
            slow = slow.next
        return res
