# 二叉树遍历

##  前序遍历：
    
    递归法：
        
        1. 将当前节点的值加入到结果集中
        2. 递归调用当前节点的左子树
        3. 递归调用当前节点的右字树

        如果是空节点就终止递归
    
    实现：
        
        def FindTreeQx(node, res):
    
            if node is None:
                return
        
            res.append(node.val)
            FindTreeQx(node.left, res)
            FindTreeQx(node.right, res)
            
        def Traversal(node):
        
            res = []
        
            if node:
        
                FindTreeQx(node, res)
        
            return res
            
##  中序遍历：

    递归法：
        
        1. 递归调用当前节点的左子树
        2. 将当前节点的值加入到结果集中
        3. 递归调用当前节点的右字树
    
        如果是空节点就终止递归
        
    实现：

        def FindTreeZx(node, res):
        
            if node is None:
                return
        
            FindTreeZx(node.left, res)
            res.append(node.val)
            FindTreeZx(node.right, res)
            
        def Traversal(node):
        
            res = []
        
            if node:
        
                FindTreeZx(node, res)
        
            return res 
            
## 后序遍历：
     
     递归法：
        1. 递归调用当前节点的左子树
        2. 递归调用当前节点的右字树
        3. 将当前节点的值加入到结果集中

        如果是空节点就终止递归
            
     实现：
     
        def FindTreeHx(node, res):
        
            if node is None:
                return
        
            FindTreeHx(node.left, res)
            FindTreeHx(node.right, res)
            res.append(node.val)
        
        
        def Traversal(node):
        
            res = []
        
            if node:
        
                FindTreeHx(node, res)
        
            return res
            
    
# 链表

## 操作倒数第N个节点：

     遍历链表，得其长度为L, 待操作的节点为：L-N+1
    
### 只遍历一次，获取倒数第N个节点的值

    tot：双指针

        1. 定义指针1和指针2，均指向头节点位置
        2. 指针1遍历链表，遍历到第N个节点时，指针2开始后移, 链表遍历结束，指针2所指位置即待取的数据

        def FindNode( head: ListNode, n: int):

            # 前后指针分别指向pre,然后间隔n
            before, after = head, head

            # after向前走n步
            while n > 0:
                after = after.next
                n -= 1

            # 当after走到头时，before刚好处于倒数第N个节点
            while after.next:
                before = before.next
                after = after.next

### 删除倒数第N个节点数据

    tot1：单指针, 多次遍历

        1. 对链表进行一次遍历，得到链表的长度 L， 第L-N+1个节点即要删除的节点
        2. 遍历到第L-N个节点时，修改其next指向为L-N+1节点的next指向
            cur.next = cur.next.next

    tot2：双指针，单次遍历

          1. 设置虚拟节点 dummyHead 指向 head (不需要对头节点进行特殊的判断)
          2. 设定双指针 p 和 q，初始都指向虚拟节点 dummyHead
          3. 指针p移动N个节点，指针q开始移动，直到指针p遍历结束
          4. 此时指针q指向倒数第N-1个节点
          5. 删除节点  cur.next = cur.next.next

    code:

        def remove_node(head: ListNode, n: int):

            def get_length(head: ListNode):

                length = 0

                while head:

                    length += 1

                    head = head.next

                return length

            length = get_length(head)

            cur = head

            for i in range(1, length - n + 1):

                cur = cur.next

            cur.next = cur.next.next

            return head

## 翻转链表
### 翻转单链表

    tot1:
    
        先对原链表做头部删操作，再对新链表做头部插入操作；

            1. 取出旧链表中头结点的元素, 新建链表

            2. 将旧链表中头结点的next作为新链表的头节点

            3. 执行旧链表中头结点的下一个元素， 重复执行

    tot2:

        把每个节点的 next 指向它的前驱节点即可

        三个指针：p（当前节点），当前节点的后继节点， q（前驱节点）

        先找到 temp，然后 p.next 再指向 q，最后 q，p 同时右移

    code:

        def ReverseList(head: ListNode):

            # 初始化记录当前节点 p 和前驱节点 q
            p = head
            q = None

            while p:

                temp = p.next
                p.next = q
                q = p
                p = temp

            return q

### 反转从位置 left 到位置 right 的链表节点

    tot:
    
        在需要反转的区间里，每遍历到一个节点，让这个新节点来到反转部分的起始位置
    
        三个指针变量: pre（curr的前节点）、curr（反转起始节点）、next（curr的后节点）
    
        1. 先将 curr 的下一个节点记录为 next；
    
        2. 把 curr 的下一个节点指向 next 的下一个节点；
    
        3. 把 next 的下一个节点指向 pre 的下一个节点；
    
        4. 把 pre 的下一个节点指向 next
    
    code:
    
        def ReverseBetween(head: ListNode, left: int, right: int):
    
            # 设置虚拟节点
            dummy_node = ListNode(-1)
            dummy_node.next = head
    
            pre = dummy_node
    
            for _ in range(left - 1):
                pre = pre.next
    
            cur = pre.next
    
            for _ in range(right - left):
    
                next = cur.next
                cur.next = next.next
                next.next = pre.next
                pre.next = next
    
            return dummy_node.next
            
##  将两个升序链表合并为一个新的升序链表并返回

    tot:
        使用迭代的方法：
       
           1. 设立虚拟头节点prehead，prev节点初始指向prehead，
           
           2. 循环两个链表，两个链表中小的节点接在prev的后面, 节点小的链表往后移一位
           
           3. 不断移动prev，最后返回prehead.next
       
    code:   
        class Solution:
            
            def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
                
                prehead = ListNode(-1)
        
                prev = prehead
                
                while l1 and l2:
                    if l1.val <= l2.val:
                        prev.next = l1
                        l1 = l1.next
                    else:
                        prev.next = l2
                        l2 = l2.next            
                    
                    prev = prev.next
        
                # 合并后 l1 和 l2 最多只有一个还未被合并完，我们直接将链表末尾指向未合并完的链表即可
                prev.next = l1 if l1 is not None else l2
        
                return prehead.next
                
   ## 判断链表中是否有环

        tot1：哈希表

            每次遍历到一个节点时，判断该节点此前是否被访问过

            1. 定义一张哈希表来存储所有已经访问过的节点。

            2. 每到达一个节点，如果该节点已经存在于哈希表中，则说明该链表是环形链表，否则就将该节点加入哈希表中


            code:
                class Solution:

                    def HasCycle(self, head: ListNode):

                        seen = []

                        # 入环点和环的长度

                        pos, length = None, None

                        while head:

                            if head in seen:

                                pos = seen.index(head)

                                length = len(seen) - pos

                                return True

                            seen.append(head)

                            head = head.next

                        return False

        tot2: 快慢指针

            是否为环形：

                1. 定义两个指针，一快一满。慢指针每次只移动一步, 而快指针每次移动两步

                2. 初始时，慢指针在位置 head，而快指针在位置 head.next

                3. 在移动的过程中，快指针反过来追上慢指针，就说明该链表为环形链表

                4. 否则快指针将到达链表尾部，该链表不为环形链表

            找出入环节点？

                当slow与fast 相遇时，再额外使用一个指针 ptr, 它指向链表头部；
                随后，它和slow 每次向后移动一个位置。最终，它们会在入环点相遇。

            环的长度是多少？

                从入口点遍历，到下次入口点遍历，得到长度


            code：

                    class Solution:

                        def HasCycle(self, head: ListNode):

                            if not head or not head.next:

                                return False

                            slow = head
                            fast = head
                            ptr = head

                            while slow != fast:

                                if not fast or not fast.next:

                                    return False

                                slow = slow.next
                                fast = fast.next.next

                            # ptr从头开始往后走，和slow相遇点就是入环点

                            while ptr != slow:
                                slow = slow.next
                                ptr = ptr.next

                            # 计算长度

                            length = 1

                            while ptr.next != slow:

                                length += 1

                                ptr = ptr.next

                            return True

