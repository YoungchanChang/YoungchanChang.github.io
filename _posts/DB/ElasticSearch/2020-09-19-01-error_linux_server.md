---
layout: post
title: 엘라스틱서치 csv를 JSON파일로 바꾸기
category: elasticsearch
tags: [elasticsearch]
comments: true
---


# 에러상황과 해결책


### 메모리 에러

- 에러코드 : Native controller process has stopped - no new native processes can be started
이렇게 하고 start 하면 vm.max_map_count [65530] is too low 오류 발생

- 메모리 설정해줘야함

### 외부접속 허용

- IP원격접속이 안 됨

- vi /etc/elasticsearch/elasticsearch.yml에서 설정파일바꿔야함

- networkhost: 0.0.0.0허용

- cluster.initial_master_nodes: ["node-1", "node-2"]까지 해줘야함

# 참조

[메모리 에러](https://para-selene.tistory.com/52)

[외부접속 허용](https://msyu1207.tistory.com/entry/Elasticsearch-%EC%84%A4%EC%B9%98-%EB%B0%8F-%EC%99%B8%EB%B6%80-%ED%97%88%EC%9A%A9)