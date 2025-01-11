# codepratice-day4
代码随想录第四天
交换链表节点、删除链表倒数第N个节点、链表相交、环形链表Ⅱ
需要熟练链表操作。

今天时间不够，也没有细看文章和视频，周日补上。

[两两交换链表中的节点](https://leetcode.cn/problems/swap-nodes-in-pairs/description/)
这个答案是我这周1在leetcode官方题解看的，感觉是比代码随想录的答案好一点。
周日再细看代码随想录的答案，琢磨琢磨，这题我不熟。（好像我也没有熟的题目，md！！）
```CPP
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode* dummyhead=new ListNode(0);
        dummyhead->next=head;
        ListNode* tmp=dummyhead;
        while(tmp->next!=nullptr&&tmp->next->next!=nullptr)
        {
            ListNode* node1=tmp->next;
            ListNode* node2=tmp->next->next;
            tmp->next=node2;
            node1->next=node2->next;
            node2->next=node1;
            tmp=node1;
        }
        ListNode* ans=dummyhead->next;
        delete dummyhead;
        return ans;
    }
};
```

[删除链表的倒数第N个节点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/description/)
重点在于双指针操作，让快指针比漫指针先走n个，这样两个指针之后同步走， 到最后fast指向空，slow指向倒N的前一个，就能删倒N。
这些题都需要背啊，最少也刷个十来次，能记住才行。
还有就是我还是要考CSP的，所以ACM模式下的这些内容，也要会。
```CPP
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* dummyhead=new ListNode(0);
        dummyhead->next=head;
        ListNode* slow=dummyhead;
        ListNode* fast=dummyhead;
        while(n--&&fast!=nullptr)
        {
            fast=fast->next;
        }
        fast=fast->next;
        while(fast!=nullptr)
        {
            fast=fast->next;
            slow=slow->next;
        }

        ListNode* tmp=slow->next;

        slow->next=slow->next->next;

        slow->next=tmp->next;
        delete tmp;
        
        return dummyhead->next;
    }
};
```


[链表相交](https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/)
将两个链表从尾部对齐，操作是先统计两个链表长度，再从短链表的位置开始遍历，第一个值相等的是我们要的节点。
```CPP
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode* cura=headA;
        ListNode* curb=headB;
        int lena=0,lenb=0;
        while(cura!=nullptr)
        {
            lena++;
            cura=cura->next;
        }
        while(curb!=nullptr)
        {
            lenb++;
            curb=curb->next;
        }

        cura=headA;
        curb=headB;
        if(lenb>lena)
        {
            swap(lena,lenb);
            swap(cura,curb);
        }

        int gap=lena-lenb;

        while(gap--)
        {
            cura=cura->next;
        }
        
        while(cura!=nullptr)
        {
            if(cura==curb)
            {
                return cura;
            }
            cura=cura->next;
            curb=curb->next;
        }
        return nullptr;
    }
};
```

[环形链表II](https://leetcode.cn/problems/linked-list-cycle-ii/)
这题之前写过，有快慢指针的印象，但是没记住。
这次写也没有细看推到过程，周日看，看完再回来写体会。
```CPP
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* fast=head;
        ListNode* slow=head;
        while(fast!=nullptr&&fast->next!=nullptr)
        {
            slow=slow->next;
            fast=fast->next->next;
            if(slow==fast)
            {
                ListNode* index1=fast;
                ListNode* index2=head;
                while(index1!=index2)
                {
                    index1=index1->next;
                    index2=index2->next;
                }
                return index2;//返回环的入口
            }
        }
        return nullptr;
    }
};
```



