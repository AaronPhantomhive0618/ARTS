# ARTS Week 2

## Algorithm

```java
/*
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.
You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.

Example 2:
Input: l1 = [0], l2 = [0]
Output: [0]

Example 3:
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
*/

class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        return helper(l1, l2, 0);
    }
    
    public ListNode helper(ListNode l1, ListNode l2, int carry) {
        if (l1 == null && l2 == null && carry == 0) {
            return null;
        }
        
        int sum = ((l1 == null) ? 0 : l1.val) + ((l2 == null) ? 0 : l2.val) + carry;
        ListNode head = new ListNode(sum % 10);
        
        head.next = helper((l1 == null) ? null : l1.next, (l2 == null) ? null : l2.next, sum / 10);
        
        return head;
    }
}

```

## Review

https://matt.might.net/articles/what-cs-majors-should-know/

计算机科学专业的学生应该了解的知识。

其中覆盖了应该怎么样才能找到好工作，怎么样才能维持终身就业，进入研究生学院应该知道什么，怎样才能造福社会。

从作品集，简历，技术核心，Unix哲学，系统管理，编程语言，离散数学，数据结构算法，体系结构，操作系统，网络，安全，密码学，测试，用户体验，可视化，并行，软件工程，图形学，机器人学习，人工智能，数据库等方面，推荐了很多有用的书籍以及链接。

## Technique/Tips

https://about.fb.com/news/2023/08/code-llama-ai-for-coding/

Meta 发布了它的代码生成 AI 模型 Code Llama。类似 GitHub Copilot 和 Amazon CodeWhisperer。

支持为 Pytho、C++、Java、 PHP、Typescript (Javascript)、C# 和 Bash 等编程语言补完代码和调试。

## Share

**google评分卡**

0 - you are unfamiliar with the subject area.

1 - you can read / understand the most fundamental aspects of the subject area.

2 - ability to implement small changes, understand basic principles and able to figure out additional details with minimal help.

3 - basic proficiency in a subject area without relying on help.

4 - you are comfortable with the subject area and all routine work on it: For software areas - ability to develop medium programs using all basic language features w/o book, awareness of more esoteric features (with book).For systems areas - understanding of many fundamentals of networking and systems administration, ability to run a small network of systems including recovery, debugging and nontrivial troubleshooting that relies on the knowledge of internals.

5 - an even lower degree of reliance on reference materials. Deeper skills in a field or specific technology in the subject area.

6 - ability to develop large programs and systems from scratch. Understanding of low level details and internals. Ability to design / deploy most large, distributed systems from scratch.

7 - you understand and make use of most lesser known language features, technologies, and associated internals. Ability to automate significant amounts of systems administration.

8 - deep understanding of corner cases, esoteric features, protocols and systems including “theory of operation”. Demonstrated ability to design, deploy and own very critical or large infrastructure, build accompanying automation.

9 - could have written the book about the subject area but didn’t; works with standards committees on defining new standards and methodologies.

10 - wrote the book on the subject area (there actually has to be a book). Recognized industry expert in the field, might have invented it.

