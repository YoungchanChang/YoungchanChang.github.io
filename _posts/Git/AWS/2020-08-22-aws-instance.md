---
layout: post
title:  AWS의 EC2서비스를 활용해 웹서비스를 구현하기
category: aws
tags: [aws, ec2, web]
comments: true
---

# EC2란?
- EC2(Elastic Copute Cloud)는 인터넷(Cloud)을 통해 외부 컴퓨터 자원(Compute)을 임대받아서 쓰는 서비스입니다. 필요에 따라서(Elastic) 컴퓨터 자원을 늘리거나 줄일 수 있습니다.

# AWS의 EC2서비스를 활용해 웹서비스를 구현하기
EC2인스턴스를 생성 -> 원격 접속(putty) -> 아파치 설치 후 웹 페이지 확인 -> VSCODE로 AWS의 EC2 인스턴스내의 파일 수정하기 순서로 진행하겠습니다.
- EC2인스턴스에서 Instance는 컴퓨터 한 대를 의미합니다.

### EC2 인스턴스 생성하기
1. AMI선택에서 적절한 운영체제를 선택합니다.

2. 인스턴스 유형에서 컴퓨터에 맞는 성능을 체크합니다.

3. 인스턴스 구성에서 적합한 정보를 구성합니다.

4. 스토리지를 추가합니다.
- 여기서 30GB까지 사용할 수 있다고 해서 30GB를 추천하지 않습니다.
- 아마존에서 요금을 매기는 방식이 GB로 돈이 나오기 때문에 관리를 잘 못하면 요금이 많이 나올 수 있기 때문입니다.

5. 태그를 추가합니다.
- 컴퓨터의 이름을 Key-Value처럼 씁니다.
- 인스턴스를 만들 때 어떤 역할이고 누가 관리하는지 메모할 때 쓰입니다.

6. 보안 그룹 구성
- **방화벽**역할을 하는 부분입니다. 내 서비스가 구동(ex>http)가 되지 않았을 때, 보안 그룹에서 설정을 확인합니다.
- **인스턴스에 접속하는 여러가지 목적**에 맞춰 보안 그룹을 설정해주면 됩니다.
- SSH(Secure SHell)의 경우 원격 접속이나 파일 복사를 할 때 쓰입니다.
- HTTP(Hyper Text Transfer Protocol)은 HTML문서를 주고받을 때 쓰입니다.

7. 프라이빗 키 생성
- 프라이빗 키는 AWS를 내 컴퓨터에서 사용할 때 사용하는 비밀번호입니다.
- [비밀번호 안전 확인 사이트](https://howsecureismypassword.net/)에서 비밀번호를 입력해보시면 안전한 비밀번호 인 것을 알 수 있습니다.
- 프라이빗 키는 절대 다시 알려주지 않으니깐, 안전한 외장하드에 꼭 **복사본을 저장**해야합니다.

##### 인스턴스 중지 버튼을 누르면 컴퓨터가 중지되고, 종료버튼을 누르면 완전히 삭제됩니다.

### putty로 원격접속하기

- putty는 SSH, 텔넷 등에 클라이언트로 동작하는 응용 프로그램입니다.

1. [PuTTY 다운로드 페이지](http://www.chiark.greenend.org.uk/~sgtatham/putty/)에서 다운로드를 합니다.

2. PuTTYgen을 사용하여 프라이빗 키 변환
- putty에서는 pem키를 읽지 못하기 때문에, pem키를 ppk파일로 변환해야 합니다.
	1. 윈도우 검색 창에서 puttygen을 선택합니다.
	2. 하단의 파라미터 아래에 있는 Type of key to generate에서 RSA를 선택합니다.
	3. 로드를 버튼을 클릭하고 하고 모든 유형의 파일 표시 옵션을 선택한 뒤 .pem파일을 찾습니다.
	4. 상단 메뉴에 File에서 Save private key를 선택합니다. 경고창이 뜨면 예를 누릅니다.
	5. 동일한 이름으로 저장합니다.
3. 푸티를 시작
1. Host Name에서 ec2에 부여받은 ip를 지정합니다. port는 22이고, 연결유형은 SSH입니다.
- 이 부분은 보안 그룹 부분에서 SSH(port:22)를 설정한 이유입니다.
2. 접속 하단에 SSH하단에 인증을 클릭합니다.
3. 인증개인키 파일 아래에 있는 Browse버튼을 클릭한 뒤에 조금 전에 저장한 .ppk파일을 선택합니다.
4. 호스트를 신뢰할 수 있는지 물으면 예를 선택합니다.
5. 범주에 세션을 선택하고 저장된 세션에 세션 이름을 입력한 다음 저장을 선택합니다.
- 열기를 클릭했는데 "expected key exchange group packet from server"오류 메시지가 뜰 경우 접속 > SSH > 키교환 > 디피-헬만 그룹 14, 디피헬만그룹 1, 디피-헬만 그룹 교환 순서로 만듭니다.

### 아파치 설치하기

1. 패키지 설치를 시작하기 전에 저장소의 패키지 목록을 업데이트하고 기존에 설치되어 있던 패키지를 업그레이드 해줍니다.
`sudo apt update && sudo apt upgrade`

2. 먼저 `sudo passwd root`로 관리자 비밀번호를 설정합니다.
	- 앞으로 터미널창에 `su`명령어만 치면 루트 권한을 획득할 수 있습니다.

3. `sudo apt install apache2`명령어를 입력합니다.

4. 인터넷 창에 ip주소를 입력하면 웹페이지가 뜹니다.
	- 만약 뜨지 않는다면 EC2생성하기-보안 그룹 구성에서 http가 허용됬는지 확인하세요.

### VSCODE를 통해 EC2 인스턴스내의 파일 수정

1. vscode마켓에서 ftp-simple을 설치합니다.

2. '다시 로드'를 한 번 해주고 `F1`키를 눌러서 `ftp-simple : Config`를 검색합니다.

3. 아래와 같은 템플릿이 뜨면 서버 접속 정보를 작성하면 됩니다.

```
[
	{
		"name": "AWS서버",
		"host": "15.164.163.137",
		"port": 22,
		"type": "sftp",
		"username": "ubuntu",
		"password": "",
		"path": "/var/www/html",
		"autosave": true,
		"confirm": false,
		"privateKey": "E:\\testuser.pem"
	}
]
```

4. `F1`키를 눌러서 `ftp-simple : Remote directory open to workspace`를 선택합니다.

5. 접속할 디렉토리를 지정해서 수정하면 됩니다.
- 여기서 파일을 수정하려고 할 때 'Error: Permission denied'라는 메시지가 뜹니다. 이것은 권한문제입니다.
- 파일 수정을 원하시는 경로(/var/www/html)에서 html폴더의 권한을 아래 명령어를 통해 수정합니다.

``
cd /var/www/
chmod -R 777 html
```



# 참조

[윈도우에서 푸티를 통해 접속하기](https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/putty.html)
[vscode에서 EC2파일 수정하기](https://snowdeer.github.io/tips/2018/02/20/editing-files-on-aws-using-vscode/)