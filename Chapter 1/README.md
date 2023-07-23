# Challenge 1: Are the letters unique?

- Difficulty: Easy
- Time: 24 min
- 思路：尋找有沒有重複的

```swift =
func challenge1(input: String) -> Bool {
    var index = 0
    var inputArray: [Character] = []
    for char in input {
        inputArray.append(char)
    }
    
    while index < inputArray.count-1 {
        
        var index2 = index+1
        while index2 < inputArray.count {
            if inputArray[index] == inputArray[index2] {
                return false
            }
            index2 += 1
        }
        index += 1
    }
    
    return true
}
```
---

# Challenge 2: Is a string a palindrome?

- Difficulty: Easy
- Time: 8 min 40 sec
- 思路：比較前後是否相同，直到中心點

```swift =
// 1.
func challenge2(input: String) -> Bool {
    let lowercased = input.lowercased()
    return String(lowercased.reversed()) == lowercased
}

// 2.
func challenge2(input: String) -> Bool {
    let strArray = Array(input.lowercased())
    let middleIndex = strArray.count/2
    var index = 0
    while index != middleIndex {
        if strArray[index] != strArray[strArray.count-1 - index] {
            return false
        }
        index += 1
    }
    
    return true
}
```
---

# Challenge 3: Do two strings contain the same characters?

- Difficulty: Easy
- Time: 20 min 18 sec
- 思路：使用loop比較兩者，當有符合的letter時，從array2中刪除，直到array2.count = 0 return true 或者 有不相符的letter return false
- 優化思路：既然是比較相同，不管排序，那就自己排順序！比較是否相同即可

```swift =
func challenge3(string1: String, string2: String) -> Bool {
    var array2 = Array(string2)
    
    if array2.count != string1.count { return false }
    
    for element in string1 {
        var index = 0
        while index <= array2.count {
            if index == array2.count { return false }
            
            if array2[index] == element {
                array2.remove(at: index)
                break
            }
            index += 1
        }
    }
    return true
}
```

---

# Challenge 4: Does one string contain another?

- Difficulty: Easy
- Time: 10 min 10 sec
- 思路: 是否包含，重要的是順序及字母是否相同，藉由index迴圈判斷當index相同時加1，當index==words.count-1 時，代表完全吻合

```swift =
extension String {
    func fuzzyContains(_ word: String) -> Bool {
        let array = Array(self.lowercased())
        let words = Array(word.lowercased())
        
        var index = 0
        
        for char in array {
            
            if char == words[index] {
                
                if index == words.count-1 { return true }
                index += 1
                
            } else {
                index == 0
            }
        }
        return false
    }
}
```
