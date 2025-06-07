# 30 Days of Solidity — MY NOTES

Welcome to my learning feedback repos for 30 Days of Solidity!

🥕Every day in june 2025.

#BuildinPublic  
#Solidity  
@HerstoryWeb3  
@0xbalala  
@0xqiuqiuu  
@audaciousSneha  

---

## DAY 1
📑Day {01} in becoming a Solidity developer   
✔️理解.sol合约结构  
✔️自定义类型为uint256的N*变量用于存储数字  
✔️调用click()公共函数用于计数  

😊使用remix 集成开发环境进行在线编译与部署合约的体验很好  


## DAY 2
📑Day {02} in becoming a Solidity developer  
✔️引用类型RT(e.g. string)不同于值类型VT，在使用时必须指定数据位置DL  
✔️函数的返回规则如图，搭配return关键词食用  
✔️view禁改，pure禁读禁改，也意味着更节油  
![image](https://github.com/user-attachments/assets/eb0850cd-992c-4b75-aa68-32347bed36fd)


## DAY 3
📑Day {03} in becoming a Solidity developer  
✔️类似于PY，Solidity使用Array和Mapping处理结构数据  
✔️declare Array `Type[size不填为dynamic] 变量名` P.S.多维数组必须同类型  
✔️append Array `.push(变量)` P.S.用`new T[](n)`重设memory数组大小  
✔️declare Mapping `mapping(KeyType KeyName*可选 => ValueType ValueName*可选) 变量名`   

🤔可以用for循环遍历mapping字典的value

```solidity
// ================================================
// 返回所有候选人的票数
// ================================================
function getAllVoteCounts() public view returns (uint256[] memory) {
    uint256 len = candidateNames.length;
    // 在内存中开一个与候选人数量相同长度的 uint256 数组
    uint256[] memory counts = new uint256[](len);

    // 逐个读取字典里的票数，填到 counts 里
    for (uint256 i = 0; i < len; i++) {
        string memory name = candidateNames[i];
        counts[i] = voteCount[name];
    }

    return counts;
}
```   

## DAY 4
📑Day {04} in becoming a Solidity developer  
✔️`constructor`函数用于初始化合约设定`constructor() {}`  
✔️`external`函数仅允许外部合约与地址交互  
✔️`require(bool, string memory message)`设置函数前提与错误返回消息  
✔️所有合约的 Storage（状态变量）都是“零初始化”的  

![image](https://github.com/user-attachments/assets/262f6586-76ea-49f3-b608-e3d866085172)


## DAY 5
📑Day {05} in becoming a Solidity developer  
✔️函数里`return;`可一键退出    
✔️自定义`modifier`作为函数通用修饰符    
✔️`constructor (){}`+`msg.sender`+`modifier xxx(){}`实现管理员权限功能   
```solidity
// Whoever deployed this contract becomes the owner
constructor() {
    owner = msg.sender; //a global variable that tells us who is calling the constructor function
}

// Modifier for owner-only functions
modifier onlyOwner() {
    require(msg.sender == owner, "Access denied: Only the owner can perform this action");
    _;//配了修饰符onlyOwner的函数将在这里执行

}
```

❓Logic advance: When approveWithdrawal, how make sure sum of withdrawalAllowances <= treasureAmount so that everyone can withdrawal at least what was allocated?  


## DAY 6
📑Day {06} in becoming a Solidity developer  
✔️`payable` allows function to receive Ether  
✔️`msg.value` holds the amount of Ether (in wei) that the user sent in  
✔️`mapping(address => bool)`实现账户注册  

🐞有一个BUG，视频代码里bankManager是没有注册的，应当在`constructor`里面声明  

```solidity
constructor(){
        ...
        registeredMembers[msg.sender] = true;//register bankManager
        ...
}
```


## DAY 7
📑Day {07} in becoming a Solidity developer  
✔️nested mapping logic  
✔️`transfer()` sytax and its gas limit on interacting with smart contracts  
`<address payable>.transfer(uint256 amount);  //send given amount of Wei to Address`  
✔️common requirements:` _amount > 0` `_adress!= address(0)`    
🤔`call()` syntax   
`  (bool success, ) = <address payable>.call{value: _amount}("");`  
⚠️[自动回滚错误的函数机制 Error handling: Assert, Require, Revert and Exceptions](https://docs.soliditylang.org/en/latest/control-structures.html#error-handling-assert-require-revert-and-exceptions)

### address payable
e.g.   `payable(msg.sender)`   
`address payable xxx`    
### nested mapping logic
```solidity
mapping(address => mapping(address => uint256)) public debts

debts[debtor][creditor] = amount;

//EXAMPLE
debts[0xA][0xB] = 1.5 ether;
//A owes B 1.5 ETH

```
