# ARTS Week 3

## Algorithm

```java
/*
Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

Example 1:

Input: 121
Output: true
Example 2:

Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
Example 3:

Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
*/

class Solution {
    public boolean isPalindrome(int num) {
        int res = 0;
        int num1 = num;
        while (num > 0) {
            res = res * 10 + (num % 10);
            num = num / 10;
        }
        return num1 == res;s
    }
}
```

```python
// 很有意思的一个Python解法：
return str(x) == str(x)[::-1]
```

## Review

我们可能正在目睹 Google 宇宙的终结。

Facebook和Instagram等大型封闭算法社交网络的兴起开始吞噬网络，最近人们转向了像TikTok这样的基于娱乐的视频源，它现在正被新一代互联网用户用作主要搜索引擎。

愈来愈多的人抱怨 Google 的搜索不再像以前那样精确。

我们周围都有迹象表明，“peak Google”时代正在结束，或者可能已经结束。

https://www.theverge.com/23846048/google-search-memes-images-pagerank-altavista-seo-keywords

## Technique/Tips

推荐三个基本功博客和网站

https://www.r2coding.com/#/README

https://github.com/jwasham/coding-interview-university/blob/main/translations/README-cn.md

https://csdiy.wiki/

## Share

#### 架构设计的原则

- N+1设计。系统中的每个组件都应做到没有单点故障；
- 回滚设计。确保系统可以向前兼容，在系统升级时应能有办法回滚版本；
- 禁⽤设计。应该提供控制具体功能是否可⽤的配置，在系统出现故障时能够快速下线功能；
- 监控设计。在设计阶段就要考虑监控的⼿段；
- 多活数据中心设计。若系统需要极⾼的⾼可⽤，应考虑在多地实施数据中⼼进⾏多活，⾄少在⼀个机房断电的情况下系统依然可⽤；
- 采⽤成熟的技术。刚开发的或开源的技术往往存在很多隐藏的bug，出了问题没有商业⽀持可能会是⼀个灾难；
- 资源隔离设计。应避免单⼀业务占⽤全部资源；
- 架构应能⽔平扩展。系统只有做到能⽔平扩展，才能有效避免瓶颈问题；
- ⾮核⼼则购买。⾮核⼼功能若需要占⽤⼤量的研发资源才能解决，则考虑购买成熟的产品；
- 使⽤商⽤硬件。商⽤硬件能有效降低硬件故障的机率；
- 快速迭代。系统应该快速开发⼩功能模块，尽快上线进⾏验证，早⽇发现问题⼤⼤降低系统交付的⻛险；
- ⽆状态设计。服务接⼝应该做成⽆状态的，当前接⼝的访问不依赖于接⼝上次访问的状态。
