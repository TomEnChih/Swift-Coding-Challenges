# Challenge 1: Are the letters unique?

- Difficulty: Easy
- Time: 24 min

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
