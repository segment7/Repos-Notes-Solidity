# 30 Days of Solidity — MY NOTES

Welcome to my learning feedback repo for 30 Days of Solidity!

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

> #### address payable
e.g.   `payable(msg.sender)`   
`address payable xxx`    
> #### nested mapping logic
```solidity
mapping(address => mapping(address => uint256)) public debts

debts[debtor][creditor] = amount;

//EXAMPLE
debts[0xA][0xB] = 1.5 ether;
//A owes B 1.5 ETH

```


## DAY 8
📑Day {08} in becoming a Solidity developer  
✔️constructor里面可以使用后面定义的函数   
✔️查重字符串数组(因为 Solidity 不允许直接用 `==` 比较两个串，所以用哈希值代替)    
✔️`public string[]`初始长度为0    
✔️换算 1 ETH = 10^18 wei    


## DAY 9
📑Day {09} in becoming a Solidity developer  
①纯血计算方程我用pure从小用到大   
②牛顿算法估计平方根  
③build two smart contracts that work together:  high-level function call(address casting)/ [low-level call](https://builder-hub.notion.site/Smart-Calculator-1d05720a23ef803a86e3e16d534b51ab)(Encode and Decode bytes )  
```sol
import "./ScientificCalculator.sol";//importing its source code
ScientificCalculator sci = ScientificCalculator(scientificCalculatorAddress);
uint256 result = sci.power(base, exponent);
```

#### What is ABI?

ABI stands for **Application Binary Interface**. Think of it as a contract’s "communication protocol" — it defines how data must be structured when one contract calls another.  

When using high-level function calls (like `otherContract.someFunction()`), Solidity handles ABI encoding for you. But with low-level calls, **you must do it manually**.  

## DAY 10
📑Day {10} in becoming a Solidity developer  
① `struct xxx {}`  
② Declare and emit Events  
③ `indexed` parameter makes it searchable in frontend(`indexed` <=3 per `event`)  
④ creating a `storage` reference within a func  


## DAY 11
📑Day {11} in becoming a Solidity developer  
① contract inheritance and use OpenZeppelin    
② ` address(this).balance`查询合约余额  
③ npm-style package system  


## DAY 12
📑Day {12} in becoming a Solidity developer  
① ERC-20: the 20th proposal in the Ethereum Request for Comments series    
② 使用套娃方程，separation of logic    


## DAY 13
📑Day {13} in becoming a Solidity developer  
① `virtual`makes function overridable by child contract  
② use` if () { require(false, ""); }` to deliberately set revert condition  
③ after LOGICALLY-Changed ` override()`, fall back to the original function using `return super.funcName();`  
④ UX-friendly `receive() external payable {function();}` automatically calls func within  


## DAY 15
📑Day {15} **Advanced**  
① An `interface xxx {}` in Solidity is basically a contract with only function definitions — no logic, no storage, no state variables.  
② We use `abstract contract xxx {}` as foundations — they are not meant to be deployed directly.  
③ state variable `private` means only functions **within this contract** can read or modify it.  
④ Array.pop() to remove the last item,  
> #### 🤔 Interface Casting(address)  
#### 函数内使用`storage`
storage作为mapping默认存储位置，函数内使用`storage`可以作用于直接修改storage里的东西  
在函数内部`address[] storage boxlist = userDepositBoxes[msg.sender];`  
boxlist只是指向userDepositBoxes这个mapping的函数局部别名（alias）函数执行完毕后就消失，不会影响变量本名  

#### 换尾删（swap-and-pop）
```solidity
for (uint i = 0; i < boxlist.length; i++) {

    if (boxlist[i] == boxAddress) {
        boxlist[i] = boxlist[boxlist.length - 1];//用结尾的值覆盖
        boxlist.pop();//删结尾的值
        break;
    }

}
```


## DAY 16
📑Day {16} **Advanced**  
