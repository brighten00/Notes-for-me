# [演算法解題思路](https://www.ptt.cc/man/Grad-ProbAsk/D1FC/M.1245522773.A.A29.html)

```json
{
  "圖論": "大多需要藉由性質來解決，比較沒有辦法分析",
  "非圖論": {
    "最佳化型": [
      "求最大、最長、最小、最短之類的",
      "動態規劃Dynamic Programming",
      "貪婪演算法Greedy"
    ],
    "非最佳化型": {
      "時間複雜度有 logN 的，像是 O() == NlogN || O() == (N^2)logN": [
        "排序",
        "2元搜索",
        "2元樹",
        "Heap堆積",
        "分治法 Divide & Conquer(最後嘗試)"
      ],
      "時間複雜度是n的非整數次方，這種問題多半是": [
        "分治法 Divide & Conquer(最後嘗試)",
        "Master Theorem"
      ],
      "線性複雜度，能夠維持線性的複雜度": ["字串比對", "Prune & Search"],
      "剩下的複雜度，或是只限制小於某個複雜度，甚至是根本沒限制複雜度的就很麻煩，只能憑真本事了。": ""
    }
  },
  "演算法": {
    "遞增法Incremental Method": "一次只做一個動作，完成了一件事才做下一件事。當一個問題太大太多時，化整為零、一個一個解決吧！",
    "記憶法Memoization": "只要將計算過的數值，儲存於記憶體，往後就能直接使用記憶體儲存的資料，不必再浪費時間重複計算一遍",
    "枚舉法Enumeration": "找到不確定的變數，枚舉所有可能性，逐一判斷正確性",
    "遞推法,疊代法Iterative Method": "不斷利用目前求得的數值，再求得新數值 , 針對已知，逐步累積，直至周全",
    "遞迴法Recursive Method": "重複運用相同手法，縮減問題範圍，直到釐清細節 , 針對未知，反覆拆解，直至精確",
    "分治法Divide and Conquer": "將一個大問題，分割成許多小問題",
    "貪心法Greedy Method": {
      "遞推法(填答案),遞增法(改答案)": [
        "一、觀察問題特徵，擬定一個填答案、改答案的原則。",
        "二、隨便挑幾個特例，手算一下。如果答案都對，就大膽假設此原則是正確的。（也可以嘗試證明此原則必定正確。）",
        "三、實作程式碼，把答案算出來。"
      ],
      "遞增法Incremental Method": "一次只做一個動作，完成了一件事才做下一件事。當一個問題太大太多時，化整為零、一個一個解決吧！",
      "遞推法,疊代法Iterative Method": "不斷利用目前求得的數值，再求得新數值 , 針對已知，逐步累積，直至周全",
      "選最極端的,但是只能短線觀察": "",
      "規約法Reduction": "把a問題轉成b問題的特例,在套用b的解決辦法, NP-Complete",
      "Scaling Algorithm": "",
      "Fixed Parameter Algorithm 固定參數演算法": "",
      "External Memory Algorithm": "當問題太過困難，就增加限制，將部分變數改成常數。"
    },
    "背包問題 Knapsack Problem": {}
  }
}
```

- [2018 出到爛的](https://www.youtube.com/watch?v=yRpp-D7NlOQ)
- [leet 起來](https://leetcode.com/problemset/all/)
- lcm 最小公倍 gcd 最大公因

# 人話

- O(logN) == 每次刪去一半的可能性，所以如果總節點有 N 個的話。

![](https://github.com/zero85258/MyNOTE/blob/master/img/BFS-and-DFS.png)

# 五大常用演算法總結

### 窮舉法 Enumeration(一個一個檢查)

```
窮舉法簡單粗暴，沒有什麼問題是搞不定的，只要你肯花時間。
同時對於小資料量，窮舉法就是最優秀的演算法。
就像太祖長拳，簡單，人人都能會，能解決問題，但是與真正的高手過招，就頹了。
```

### 貪婪法 Greedy(每次都選奶大的)

```
短線
貪婪演算法可以獲取到問題的區域性最優解，不一定能獲取到全域性最優解，同時獲取最優解的好壞要看貪婪策略的選擇。
特點就是簡單，能獲取到區域性最優解。就像打狗棍法，同一套棍法，洪七公和魯有腳的水平就差太多了，
因此同樣是貪婪演算法，不同的貪婪策略會導致得到差異非常大的結果。
```

### 動態規劃法 Dynamic Programming

- DP(n) is 算過了嗎 ? 取快取 : DP(讓 n 收斂)

```
長線
當最優化問題具有重複子問題和最優子結構的時候，就是動態規劃出場的時候了。
動態規劃演算法的核心就是提供了一個memory來快取重複子問題的結果，避免了遞迴的過程中的大量的重複計算。
動態規劃演算法的難點在於怎麼將問題轉化為能夠利用動態規劃演算法來解決。
當重複子問題的數目比較小時，動態規劃的效果也會很差。
如果問題存在大量的重複子問題的話，那麼動態規劃對於效率的提高是非常恐怖的。
```

### 分治法 Divide&Conquer

- 切割問題

### 回溯法 Backtracking

- 窮舉(可能是樹狀), 正確 Backtracking(n+1), 錯誤 Backtracking(n-1)

```
回溯演算法是`DFS深度優先`策略的典型應用，回溯演算法就是沿著一條路向下走，
如果此路不同了，則回溯到上一個分岔路，在選一條路走，一直這樣遞迴下去，直到遍歷萬所有的路徑。
八皇后,迷宮 都是回溯演算法的一個經典問題
```

### [分支限界法](https://zhuanlan.zhihu.com/p/36800491)

```
是`BFS廣度優先`的一個經典的例子。
回溯法一般來說是遍歷整個解空間，獲取問題的所有解，
而分支限界法則是獲取一個解（一般來說要獲取最優解
```

# 硬肛 obj 走訪(js)

```js
function iterate(obj, stack) {
  for (var property in obj) {
    if (obj.hasOwnProperty(property)) {
      if (typeof obj[property] == "object") {
        iterate(obj[property], stack + "." + property);
      } else {
        console.log(property + " " + obj[property]);
        $("#output").append($("<div/>").text(stack + "." + property));
      }
    }
  }
}

iterate(object, "");
```

# 遞迴專家

```sh
# Linear recursion (線性遞迴)
當一個 function 在每一輪都呼叫自己一次, 就稱為 linear recursion
當我們將大問題一步步的分解成小問題, 朝終點前進的這段過程, 又稱為 Winding (纏繞),
而從終點處一路 return 回來, 這段又稱為 Unwinding (解纏繞)

# Binary recursion (二元遞迴)
每一輪的結果來自多個不同的 recursion 計算後而得之

# Mutual recursion
簡單來說, 就是交替式的呼叫兩個不同的 recursion method, 比方說,
這一輪呼叫 function B, 下一輪又呼叫 function A, 下一輪又回到 function B, 依序輪流的呼叫直到終點

# Tail recursion
簡單來說,
就是當 recursion 跑到終點時, 不需要將終點得到的結果再反向的一路計算回來,
例如我們之前介紹過的 GCD Tail recursion 也是 linear recursion 的一種

# Nested recursion
當一個 recursion function 呼叫了它自己, 並且 recursion function 的 args 之一也是這個 recursion function
```

# HashTable

- 001 TwoSum
- 242 ValidAnagram

# BinarySearch

- 035 SearchInsertPosition
- 278 FirstBadVersion

# LinkedList

- 083 RemoveDuplicates
- 021 MergeTwoSortedLists

# BinaryTree

- 100 TwoSum
- 110 BalancedBinaryTree

# Recursive/Iterative

- 101 SymmetricTree
- 617 MergeTwoBinaryTrees

# Dp

- 062 UniquePaths
- 063 UniquePaths II
- 198 HouseRobber
- 213 HouseRobber II

# Traversal

- 094 BinaryTreeInorder
- 102 BinaryTreeLevelOrderTraversal

# BST

- 700 SearchInABinary
- 098 ValidateBinarySearchTree

# BitwiseOperation

- 136 SingleNumber
- 693 BinaryNumberWithAlternatingBits

# 解

```java
// 001 TwoSum
public class Solution {
public int[] twoSum(int[] numbers, int target) {
HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
int[] result = new int[2];
for (int i = 0; i < numbers.length; i++) {
if (map.containsKey(numbers[i])) {
int index = map.get(numbers[i]);
result[0] = index ;
result[1] = i;
return result;
} else {
map.put(target - numbers[i], i);
}
}
return result;
}
}

```

```java
// 035 SearchInsertPosition
class Solution {
public int searchInsert(int[] nums, int target) {
if (nums == null || nums.length == 0) return 0;

int i = 0, j = nums.length - 1;
int index = -1;
while(i <= j) {
index = (i + j) / 2;
if(nums[index] == target)
return index;
if(nums[index] >= target)
j = index - 1;
else
i = index + 1;
}
return i;
}
}
```

```java
// 101 SymmetricTree
class Solution {
public boolean isSymmetric(TreeNode root) {
if (root == null) return true;
LinkedList<TreeNode> q = new LinkedList<>(Arrays.asList(root.left, root.right));
while (!q.isEmpty()) {
TreeNode left = q.poll(), right = q.poll();
if (left == null && right == null) continue;
if (left == null || right == null || left.val != right.val) return false;
q.addAll(Arrays.asList(left.left, right.right, left.right, right.left));
}
return true;
}
}
```

```java
// 062 UniquePaths
class Solution {
private int[][] dp;

public int uniquePaths(int m, int n) {
// setState
this.dp = new int[m + 3][n + 3];

// start
return rec(m, n);
}

public int rec(int m, int n) {
System.out.println(m + " " + n + " " + this.dp[m][n]);
if(this.dp[m][n] != 0) return this.dp[m][n];

if (m == 0 || n == 0) {
this.dp[m][n] = 0;
return 0;
} else if(m == 1 || n == 1){
this.dp[m][n] = 1;
return 1;
} else {
this.dp[m][n] = rec(m - 1, n) + rec(m, n - 1);
return this.dp[m][n];
}
}
}
```

```java
// 目前是c須改寫java
// 198 HouseRobber
class Solution {
public int houseRobber(vector<int>& nums) {
if(nums.size() == 0) return 0;
if(nums.size() == 1) return nums[0];

int *dp = new int[nums.size()];
dp[0] = nums[0];
dp[1] = max(nums[0], nums[1]);

for(int i = 2; i < nums.size(); i++){
dp[i] = max(dp[i - 2] + nums[i], dp[i - 1]);
}

// getLast
return dp[nums.size() - 1];
}
}

// 遞迴法改寫中
class Solution {
private ArrayList<Integer> dp = new ArrayList<Integer>();

public int rob(int[] nums) {
List<Integer> nums2 = Arrays.stream(nums).boxed().collect(Collectors.toList());
dp.add(0, nums2.get(0) );
dp.add(1, Math.max(nums2.get(0), nums2.get(1)) );

return rec(new ArrayList<Integer>(nums2.remove(1)));
}

public int rec(ArrayList<Integer> nums) {
if(nums.size() == 0) return 0;
if(nums.size() == 1) return nums.get(0);

int i = nums.size() - 1;
return Math.max(
rec(new ArrayList<Integer>(nums.remove(2))) + nums.get(i-1),
rec(new ArrayList<Integer>(nums.remove(1)))
);
}
}
```

```java
// 700 SearchInABinary
class Solution {
public TreeNode searchBST(TreeNode root, int val) {
if (root == null || val == root.val) return root;

return val < root.val ? searchBST(root.left, val) : searchBST(root.right, val);
}
}
```

```java
// 098 ValidateBinarySearchTree
class Solution {
public boolean isValidBST(TreeNode root) {
if (root == null) return true;
if (!isValidBST(root.left)) return false;
if (last != null && root.val <= last.val) return false;
last = root;
return isValidBST(root.right);
}
}
```

```java
// 094 BinaryTreeInorder
class Solution {
public List<Integer> inorderTraversal(TreeNode root) {
List<Integer> res = new ArrayList<>();
inorder(root, res);
return res;
}

public void inorder(TreeNode root, List<Integer> res) {
if (root == null) return;
inorder(root.left, res);
res.add(root.val);
inorder(root.right, res);
}
}
```
