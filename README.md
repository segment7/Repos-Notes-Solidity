# 30 Days of Solidity — MY NOTES

Welcome to my learning feedback repos for 30 Days of Solidity!

Every day in june 2025.

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
✔️构造函数用于初始化合约设定`constructor() {}`  
✔️`external`函数允许外部合约交互  
✔️`require(bool, string memory message)`设置函数前提与错误返回消息  
✔️所有合约的 Storage（状态变量）都是“零初始化”的  

![image](https://github.com/user-attachments/assets/262f6586-76ea-49f3-b608-e3d866085172)


## DAY 5
📑Day {05} in becoming a Solidity developer  
✔️
✔️
✔️


## DAY 6
📑Day {06} in becoming a Solidity developer  
✔️
✔️ 
✔️
