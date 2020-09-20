---
layout: post
title: 엘라스틱서치 csv를 JSON파일로 바꾸기
category: python
tags: [python, 쓰기]
comments: true
---


# 에러상황과 해결책

### illegal multibyte sequence

- 에러코드 : UnicodeEncodeError: 'cp949' codec can't encode character '\u2027' in position 321: illegal multibyte sequence

- 원인 : 파일을 읽을 때 코드가 잘못되었다.

- 해결책 : utf8로 읽어야 한다.

- open('파일경로.txt', 'rt', encoding='UTF8')

### bulk request must be terminated

- 에러코드 : The bulk request must be terminated by a newline [\\n]

- 원인 : bulk요청을 할 시에 마지막은 엔터가 들어가 있어야 한다.

- 해결책 : JSON끝에 엔터를 넣는다.

###  Unexpected character (''' (code 39))

- 에러코드 : Unexpected character (''' (code 39)): was expecting double-quote to start field name\n at : 

- 원인 : python은 객체의 key값을 ''(싱글쿼트)로 감싸지만, json은 ""(더블쿼트)로 감싼다.

- 해결책: json.dump()로 객체를 감싼다.


# 참조

[illegal multibyte sequence](https://airpage.org/xe/language_data/20205)

[Unexpected character]((https://stackoverflow.com/questions/18283725/how-to-create-a-python-dictionary-with-double-quotes-as-default-quote-format/18283909))

