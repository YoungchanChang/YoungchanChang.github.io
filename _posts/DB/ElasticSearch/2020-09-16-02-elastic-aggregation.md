---
layout: post
title: 엘라스틱서치 aggregation
category: elasticsearch
tags: [elasticsearch]
comments: true
---

# aggreagtion

- 같고 있는 document에서 조합을 통해서 값을 도출할 때 쓰이는 방법

- Metric aggregation은 평균, 최솟값, 최댓값 구할 때 사용한다.

{
    "size" : 0,
    "aggs" : {
            "max_score" : {
                "max" : {
                    "field" : "points"
                }
            }
    }
}

- 평균, 최소, 최대를 전부 도출하려고 할 때 stats명령어를 사용하면 된다.
```
{
    "size" : 0,
    "aggs" : {
            "stats_score" : {
                "stats" : {
                    "field" : "points"
                }
            }
    }
}
```

- bucket aggregations는 group by로 사용한다. 팀별로 어떤 결과값을 도출하고 싶을 때 사용한다.

- document를 index에 삽입하기

- `curl -XPUT localhost:9200/basketball`

- `curl -XPUT localhost:9200/basketball/record/_maaping -d @basketball_mapping.json` record 타입에 매핑을 해준다.

- 도큐먼트에 값을 넣는다. `curl -XPOST localhost:9200/_bulk --data-binary @twoteam_basketball.json`

```
{ "index" : { "_index" : "basketball", "_type" : "record", "_id" : "1" } }
{"team" : "Chicago","name" : "Michael Jordan", "points" : 30,"rebounds" : 3,"assists" : 4, "blocks" : 3, "submit_date" : "1996-10-11"}
```

- aggreagtion 진행하기. size=0은 여러개 정보 대신 원하는 정보만 추출한다. aggs의 이름은 players, term aggre를 쓰고 team별로 묶는다.

- `curl -XGET localhost:9200/_search?pretty --data-binary @terms_aggs.json`

```
{
    "size" : 0,
    "aggs" : {
            "players" : {
                "terms" : {
                    "field" : "team"
                }
            }
    }
}
```

- 농구 통계자료가 주어졌을 때, 팀 분류를 한 다음에 각 팀별로 성적을 낸다. 팀별로 성적을 가져와라. 팀별 분류에서 점수들이 나오게 된다.

```
{
    "size" : 0,
    "aggs" : {
        "team_stats" : {
            "terms" : {
                "field" : "team"
            },
            "aggs" : {
                "stats_score" : {
                    "stats" : {
                        "field" : "points
                    }
                }
            }
        }
    }
}
```

# 참조

[ELK 스택](https://www.youtube.com/watch?v=ebXczuiMbEQ&list=PLVNY1HnUlO24LCsgOxR_eK2Yi4sOgH9Pg&index=13)