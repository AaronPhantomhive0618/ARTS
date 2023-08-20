# ARTS Week 1

## Algorithm

```java
/**
Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays.

The overall run time complexity should be O(log (m+n)).

Example 1:
Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: merged array = [1,2,3] and median is 2.

Example 2:
Input: nums1 = [1,2], nums2 = [3,4]
Output: 2.50000
Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
*/

// Runtime: 2 ms, faster than 44.57% of Java online submissions for Median of Two Sorted Arrays.
// Memory Usage: 42.44 MB, less than 62.56% of Java online submissions for Median of Two Sorted Arrays.

class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int[] combineArray = Arrays.copyOf(nums1, nums1.length + nums2.length);
        System.arraycopy(nums2, 0, combineArray, nums1.length, nums2.length);

        Arrays.sort(combineArray);

        if (combineArray.length % 2 == 1) {
            return combineArray[combineArray.length / 2];
        } else {
            double result1 = combineArray[combineArray.length / 2];
            double result2 = combineArray[combineArray.length / 2 - 1];
            return (result1 + result2) / 2;
        }
    }
}
```



## Review

https://aws.amazon.com/cn/blogs/architecture/lets-architect-security-in-software-architectures/

亚马逊提供了几个解决架构软件时的安全问题的解决方案。其中包括：

- 深入探讨 AWS 当前的安全威胁形势
- 零信任构建更好的安全性
- 深入探讨 AWS 上的容器安全性
- 将您的密钥迁移到 AWS Secrets Manager



## Technique/Tips

### git生成ssh密钥

```
ssh-keygen -t rsa -C "xxxxxx@xxx.com"
```

之后可以直接三次回车，

然后在`C:/Users/xxx/.ssh/id_rsa.pub`文本编译器打开。



## Share

耗子叔的课程中讲到的如何处理错误的最佳方法。最近在做相关业务，非常实用，对我也很有启发。

#### 统一分类的错误字典

无论是使用错误码还是异常捕捉，都需要认真并统一地做好错误的分类。最好是在一个地方定义相关的错误。比如，HTTP 的 4XX 表示客户端有问题，5XX 则表示服务端有问题。也就是说，要建立一个错误字典。

#### 同类错误的定义最好是可以扩展的

这一点非常重要，而对于这一点，通过面向对象的继承或是像 Go 语言那样的接口多态可以很好地做到。这样可以方便地重用已有的代码。

#### 定义错误的严重程度

比如，Fatal 表示重大错误，Error 表示资源或需求得不到满足，Warning 表示并不一定是个错误但还是需要引起注意，Info 表示不是错误只是一个信息，Debug 表示这是给内部开发人员用于调试程序的。

#### 错误日志的输出最好使用错误码，而不是错误信息

打印错误日志的时候，应该使用统一的格式。但最好不要用错误信息，而应使用相应的错误码，错误码不一定是数字，也可以是一个能从错误字典里找到的一个唯一的可以让人读懂的关键字。这样，会非常有利于日志分析软件进行自动化监控，而不是要从错误信息中做语义分析。比如：HTTP 的日志中就会有 HTTP 的返回码，如：404。但我更推荐使用像PageNotFound这样的标识，这样人和机器都很容易处理。

#### 忽略错误最好有日志

不然会给维护带来很大的麻烦。

#### 对于同一个地方不停的报错，最好不要都打到日志里

不然这样会导致其它日志被淹没了，也会导致日志文件太大。最好的实践是，打出一个错误以及出现的次数。

#### 不要用错误处理逻辑来处理业务逻辑

也就是说，不要使用异常捕捉这样的方式来处理业务逻辑，而是应该用条件判断。如果一个逻辑控制可以用 if - else 清楚地表达，那就不建议使用异常方式处理。异常捕捉是用来处理不期望发生的事情，而错误码则用来处理可能会发生的事。

#### 对于同类的错误处理，用一样的模式

比如，对于null对象的错误，要么都用返回 null，加上条件检查的模式，要么都用抛 NullPointerException 的方式处理。不要混用，这样有助于代码规范。

#### 尽可能在错误发生的地方处理错误

因为这样会让调用者变得更简单。

#### 处理错误时，总是要清理已分配的资源

这点非常关键，使用 RAII 技术，或是try-catch-finally，或是 Go 的 defer 都可以容易地做到。

#### 不推荐在循环体里处理错误

这里说的是try-catch，绝大多数的情况你不需要这样做。最好把整个循环体外放在 try 语句块内，而在外面做 catch。

#### 不要把大量的代码都放在一个 try 语句块内

一个 try 语句块内的语句应该是完成一个简单单一的事情。

#### 为你的错误定义提供清楚的文档以及每种错误的代码示例

如果做 RESTful API 方面的，使用 Swagger 会很容易搞定这个事。

#### 对于异步的方式，推荐使用 Promise 模式处理错误

对于这一点，JavaScript 中有很好的实践。

#### 对于分布式的系统，推荐使用 APM 相关的软件

尤其是使用 Zipkin 这样的服务调用跟踪的分析来关联错误。
