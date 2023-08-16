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

---

# Challenge 5: Count the characters

- Difficulty: Easy
- Time: 4 min 34 sec
- 思路：for-in 遍歷所有 words ，如果符合就 +1，最後得出答案
- 另外思路：可以反向思考，移除 words 裡的 letter ，之後比較移除前後的數量

```swift =
func countOfChar(letter: Character ,in words: String) -> Int {
    
    var count = 0
    
    for word in words {
        if word == letter {
            count += 1
        }
    }
    return count
}
```
---

# Challenge 6: Remove duplicate letters from a string

- Difficulty: Easy
- Time: 8 min 45 sec
- 思路：for-in 遍歷所有 letter ，沒有重複就 append 進 outputs
- 另外思路：可以嘗試使用 Filter + Dictionary 篩選

```swift =
func challenge6(input: String) -> String {
    
    var outputs: [Character] = []
    
    for char in input {
        if !outputs.contains(char) {
            outputs.append(char)
        }
    }
    return String(outputs)
}
```

---

# Challenge 7: Condense whitespace

- Difficulty: Easy
- Time: 17 min 34 sec
- 思路：for-in 所有 character，不為 " " 就加入，為 " " 時，跟前者比較，相同就不加入 

```swift =
func removeMutiWhitespace(input: String) -> String {
    let inputs = Array(input)
    var outputs: Array<Character> = []
    
    for input in inputs {
        if outputs.isEmpty {
            outputs.append(input)
        } else if let last = outputs.last {
            if input != " " {
                outputs.append(input)
            } else if input != last {
                outputs.append(input)
            }
        }
    }
    return outputs.map { String($0) }.joined()
}
```
---

# Challenge 8: String is rotated
- Difficulty: Tricky
- Time: 22 min 27 sec
- 思路：先找出第一個 character，比較 character 在兩個 String 的位置，在依照順序開始比較(錯誤)
- 另外思路：rotated 只不過是把其中一段 String 改變位置，移到最前方來，因此只要把 string + string 就可以滿足所有情況

(錯誤) 有重複字的 string 會失敗
ex.
abacba
cbaaba
```swift =
func isRotated(string1: String, string2: String) -> Bool {
    
    if string1.count != string2.count { return false }
    if string1 == "" { return true }
    
    let array1 = Array(string1)
    let array2 = Array(string2)
    
    guard let index = array2.firstIndex(of: array1.first!) else { return false }
    
    var currentIndex = index
    for i in 1..<array1.count {
        if currentIndex+1 == array2.count { currentIndex = -1 }
        if array1[i] != array2[currentIndex+1] { return false }
        currentIndex += 1
    }
    return true
}
```

正確
```swift =
func isRotated(string1: String, string2: String) -> Bool {
    guard string1.count == string2.count else { return false }
    let allAnswer = string1 + string1
    return allAnswer.contains(string2)
}
```
