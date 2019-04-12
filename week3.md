## 20190408~20190414
## Algorithm
Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

Example 1:

Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
Example 2:

Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.
### 解答
```
class Solution {
    public int removeDuplicates(int[] nums) {
        if(nums.length == 0){
            return 0;
        }
        int cur = nums[0];
        int duplicates = 0;
        for(int i=1; i<nums.length; i++){
            if(nums[i] == cur){
                duplicates ++;
            }else{
                cur = nums[i];
                nums[i-duplicates] = cur;
            }
        }
        return nums.length-duplicates;
    }
}
```
## Review
### [关于单点登录的原理](https://www.cnblogs.com/ywlaker/p/6113927.html)
1. 单点登录全称Single Sign On（以下简称SSO），是指在多系统应用群中登录一个系统，便可在其他所有系统中得到授权而无需再次登录，包括单点登录与单点注销两部分。
2. 登录
   * sso需要一个独立的认证中心，只有认证中心能接受用户的用户名密码等安全信息，其他系统不提供登录入口，只接受认证中心的间接授权。间接授权通过令牌实现，sso认证中心验证用户的用户名密码没问题，创建授权令牌，在接下来的跳转过程中，授权令牌作为参数发送给各个子系统，子系统拿到令牌，即得到了授权，可以借此创建局部会话，局部会话登录方式与单系统的登录方式相同。这个过程，也就是单点登录的原理，用下图说明
![注销流程](/static/7.png)
3. 注销
   * 单点登录自然也要单点注销，在一个子系统中注销，所有子系统的会话都将被销毁，用下面的图来说明
![注销流程](/static/8.png)
## Tip/Techni
### VSCode 安装Go插件
* 安装过程中会出现很多失败
```
Installing github.com/derekparker/delve/cmd/dlv FAILED
Installing github.com/stamblerre/gocode FAILED
Installing github.com/ianthehat/godef FAILED
Installing github.com/sqs/goreturns FAILED
```
* 手动安装：clone项目到本地，在进行打包放置$GOPATH\bin路径下 
   * 浏览器访问：[github.com/sqs/goreturns](https://github.com/sqs/goreturns)
   * 在$GOPATH\src路径下建立文件夹github.com，进入github.com后，执行命令git clone git@github.com:sqs/goreturns.git
   * 进入$GOPATH\bin，执行go install ..\src\github.com\sqs\goreturn，就能自动打包成goreturns.exe文件了
* Go插件修改配置参数 
   * 点击下图的Settings  
![设置](/static/4.png)
   * 找到Go Configuration，点击Edit in settings.json
![Configuration](/static/5.png)
   * 下图是增加go test 命令参数 -v，使得单元测试能够打印出详细信息
![testFlags](/static/6.png)
## Share
### 继续分享Awk One-Liners的内容
#### ***打印文件中每行的行号***
```
 awk '{print FNR "\t" $0}'
```
* FNR-File Line Number 若有多个文件，每个文件的行号都是重新开始编号的
```
awk '{print NR "\t" $0}'
```
* NR-Line Number 若有多个文件，显示的行数是依次递增的，不会重新编号