---
layout: post
title: 웹스크래핑15. FileDownlaod
category: webscraping
tags: [python, webscraping]
comments: python
---

# 파일 다운받기

- csv파일로 다운로드 받게 처리한다. 해당 부분을 모듈로 만든다.

```python
import csv


def save_to_file(jobs):
    file = open("jobs.csv", mode="w")
    writer = csv.writer(file)
    writer.writerow({"title", "company", "location"})

    for job in jobs:
        print(job)
        print(list(job.values()))
        writer.writerow(list(job.values()))
```

- 서버 내부에서 인자가 들어왔을 때 해당 모듈을 실행시킨다.
    - 모듈을 import해야한다.
    - send_file메소드도 flaks에서 import한다.

```python
from flask import Flask, render_template, request, redirect, send_file
from exporter import save_to_file

@app.route("/export")
def export():
    try:
        word = request.args.get('word')
        if not word:
            raise Exception()
        word = word.lower()
        jobs = db.get(word)
        if not jobs:
            raise Exception()
        save_to_file(jobs)
        return send_file("jobs.csv")

```