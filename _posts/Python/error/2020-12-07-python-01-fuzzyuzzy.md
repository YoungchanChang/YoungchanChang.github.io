---
layout: post
title: 파이썬 fuzzyuzzy에러
category: python
tags: [python, program]
comments: true
---

# 에러 코드

- TypeError: expected string or bytes-like object

- 뜻 : "형"과 관련된 에러. 문자열이나 bytes형식의 객체를 기대했다.

# 에러 발생 상황

- `process.extractOne(args1, args2, scorer=fuzz.partial_ratio)`메소드를 수행했을 때 에러

# 에러 발생 원인

- args1은 문자열, args2는 배열을 넣었어야 하는데,  parse_"string"이 아니라 배열을 넣었었다.

- 문자열 대신에 nan을 넣은 경우 위와 같은 현상 발생

# fuzzywuzzy에러코드

```console
  File "E:\1thefull\work\bokji_qa\bokji-qa-elasticsearch\lib\site-packages\fuzzywuzzy\utils.py", line 95, in full_process
    string_out = StringProcessor.replace_non_letters_non_numbers_with_whitespace(s)
  File "E:\1thefull\work\bokji_qa\bokji-qa-elasticsearch\lib\site-packages\fuzzywuzzy\string_processing.py", line 26, in replace_non_letters_non_numbers_with_whitespace
    return cls.regex.sub(" ", a_string)
TypeError: expected string or bytes-like object
```

> [참조](https://www.python2.net/questions-16237.htm)
