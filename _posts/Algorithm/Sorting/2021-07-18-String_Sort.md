---
title:  "문자열의 정렬법"
excerpt: "문자열은 사전순 정렬"
categories:
  - AL_Sorting
tags:
  - 1
last_modified_at: 2021-07-18

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# String 내에 접두어가 있는지 체크

| phone_book                        | return |
| --------------------------------- | ------ |
| ["119", "97674223", "1195524421"] | false  |
| ["123","456","789"]               | true   |
| ["12","123","1235","567","88"]    | false  |

```python
def solution(phone_book):
    lst = sorted(phone_book) 
    l = len(lst) 
    for i in range(l-1): 
        length = len(lst[i])
        if lst[i] == lst[i+1][:length]:
            return False
    else : 
        return True
```

- 위와 같이, element 가 '수' 가 아니라, 문자열일떄에는 정렬이 사전순으로 일어납니다.
- ["119", "97", "11955"]   -> ["119", "11955", "97",]  
- 즉 정렬 후에, 앞의 원소가 뒤에 포함되는지만 검사하면 되는것입니다! 

```python
# 몰론 위를 해시를 이용해 풀수도 있습니다.
def solution(phone_book):
    answer = True
    hash_map = {}
    for phone_number in phone_book:
        hash_map[phone_number] = 1
    for phone_number in phone_book:
        temp = ""
        for number in phone_number:
            temp += number
            if temp in hash_map and temp != phone_number:
                answer = False
    return answer
```

- 해시에서 key search 가 매우 빠르다는것을 이용한 좋은 풀이입니다.
