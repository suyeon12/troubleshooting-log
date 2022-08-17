## 스스로 보려고 쓰는 aws putty

1. puttygen 접속

![Untitled](https://user-images.githubusercontent.com/72901045/185029317-d6864cd4-aa93-4b51-8fc8-099eb93dde78.png)

Conversions - import key로 `linux_key.pem` import한 다음

save private key 누른 후 ppk로 저장

<br/>

2. putty 접속

![Untitled (1)](https://user-images.githubusercontent.com/72901045/185029469-8eac7c9f-7fdf-4df7-b6c9-96c1a270ecd8.png)

`connection - ssh - auth` 로 들어가 `browse` 한 다음 ppk 불러오기



`aws` 에서 인스턴스 ip 주소 확인

`session` 에서  `Host Name(or IP address)` 부분에 방금 확인한 인스턴스 ip 주소 입력

<br/>

### 3. 로그인

**ec2-user**로!!! 꼭..........

<br/>

<br/>

---

### aws

```bash
$ aws --version
command not found: aws
```

아무것도 안 하고 바로 aws --version을 입력하면 다음과 같이 뜬다!

먼저 awscli를 설치해줘야 한다. 관련 문서는 [여기](https://docs.aws.amazon.com/ko_kr/cli/latest/userguide/getting-started-install.html)

<br/>

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

만약 `unzip: command not found` 오류가 발생한다면 `sudo apt-get install unzip` 또는 `sudo yum install unzip` 을 입력하고 다음 과정으로 넘어가면 된다. 나는 Redhat 계열이라 yum을 이용하였다.



그 다음부터는 `aws configure` 로 로그인을 한 후 작업을 진행하면 된다.


