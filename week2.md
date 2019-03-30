## 20190325~20190331
## Algorithm
### Two Sum
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
### 解答
```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode l3 = new ListNode(0);
        int i = 0;
        while(null != l1){
            ListNode n = new ListNode(0);
            n.val = l1.val + i;
            l1 = l1.next;
            if(null != l2){
                n.val = n.val + l2.val;
                l2 = l2.next;
            }
            if(n.val>=10){
                n.val = n.val -10;
                i = 1;
            }else{
                i = 0;
            }
            
            insert(l3, n);           
        }
        while(null != l2){
            ListNode n = new ListNode(0);
            n.val = l2.val + i;
            l2 = l2.next;
            
            if(n.val>=10){
                n.val = n.val -10;
                i = 1;
            }else{
                i = 0;
            }
            
            insert(l3, n);      
        }
        
        if(i==1){
            ListNode n = new ListNode(0);
            n.val = i;
            insert(l3, n);     
        }
        l3 = l3.next;
        return l3;
    }
    
    public void insert(ListNode l, ListNode n){
        ListNode p = l;
        while(p.next != null){
            p = p.next;
        }
        p.next = n;
    }
}
```
## Review
### [从亚马逊的实践，谈分布式系统的难点](https://time.geekbang.org/column/article/1505)
1. 架构：高并发、异地多活、容器化、微服务、高可用、弹性化架构等
2. 管理型技术方法：DevOps、应用监控、自动化运维、SOA服务治理、去IOE
3. 分布式系统的发展：
   * SOA-基于服务的架构：过于笨重
      * 可重用、粒度适合、模块化
      * 符合开放标准
      * 服务的识别和分类，监控和跟踪
   * SOAP、WSDL、XML
   * RESTful、JSON
   * 微服务
      * 微服务平台PaaS，比如Spring Cloud
4. 分布式系统的难点
   * 需要有分布式的团队架构
   * 分布式服务查错不容易
   * 自动化运维难度高
   * 监控复杂
5. 分布式系统需要注意的问题
   * 异构系统的不标准问题
      * 软件和应用不标准
      * 通讯协议不标准
      * 数据格式不标准
      * 开发和运维的过程和方法不标准
   * 系统架构中的服务依赖性问题
      * Swagger
   * 故障发生的概率更大
      * 故障影响面、影响时长
   * 多层架构的运维复杂度更大
      * 基础层：机器、网络和存储设备
      * 平台层：中间件层（Tomcat、Mysql、Redis、Kafka之类的）
      * 应用层：业务软件
      * 接入层：接入用户请求的网关、负载均衡或是CDN、DNS等
## Tip/Techni
### 用IDea开发Restful应用时，可以安装一个插件 ***RestfulToolkit*** ，本地快速调试Restful接口：
![RestfulToolkit工具截图](/static/3.png)
## Share
### 继续分享Awk One-Liners的内容
1. 将文件中的行距扩大一倍
```
    awk '1;{print ""}' file
```
   * 每个awk命令包含：pattern {action statement}。在命令中，pattern或者action可以缺失。如果pattern缺失的话，action就作用于每一行；如果action缺失的话，等同于{print}。所以上面的命令等同于：   
   ```
   awk '1 {print};{print ""}' file
   ```
   * 由于1表示永远为真，所以第一个命令相当于作用于每一行
   ```
   awk '{print}; {print ""}' file
   ```
   * 由于awk没打印一行会默认以ORS结束（换行符），第一个命令相当于打印print $0。因此上面的命令能够实现打印一行后，空格一行再打印。