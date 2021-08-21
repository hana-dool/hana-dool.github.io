---
title:  "웹 로그파일(아파치)"
excerpt: "웹 로그파일 데이터의 유형에 대해 알아보자."
categories:
  - Others
tags:
  - 3
last_modified_at: 2021-03-05

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---





# How to get?

역시나 학부생에게는 어떻게 얻느냐가 중심 화두이다.. 

<http://www.google.com/search?q=inurl%3Aaccess.log+filetype%3Alog> 이 링크로 들어가게 된다면 다른사람이 공개해 놓은 아파치 웹 로그 파일을 얻을 수 있다.



# 아파치의 엑세스 로그?

아파치는 log_config 모듈을 제공하고, 형식 문자열을 사용해 엑세스 로그의 형식을 설정할 수 있게 한다. 

| 형식 문자열   | 설명                                                         |
| ------------- | ------------------------------------------------------------ |
| %%            | 퍼센트 기호                                                  |
| %...b         | HTTP 헤더를 제외한 전송 바이트 수. CLF 형식과 같이, 전송한 내용이 없는 경우 0 대신 `-`가 나온다. |
| %...D         | 요청을 처리하는 데 걸린 시간(마이크로초 단위).               |
| %...h         | 원격 호스트                                                  |
| %...{Foobar}i | 서버가 수신한 요청에서 Foobar: 헤더의 내용.                  |
| %...l         | (있다면 identd가 제공한) 원격 로그인명. mod_ident가 있고 IdentityCheck가 On이 아니면 빼기 기호를 기록한다. |
| %...r         | 요청의 첫 번째 줄                                            |
| %...s         | 상태(status). 내부 리다이렉션된 요청의 경우 원래 요청의 상태이다. 최종 요청의 상태는 `%...>s`. |
| %...t         | common log format 시간 형식(표준 영어 형식)의 시간           |
| %...u         | 원격 사용자(auth가 제공하며, 상태(%s)가 401인 경우 이상한 값이 나올 수 있음) |

위 정보를 이용하여 아파치 설정파일에 다음과 같이 엑세스 로그의 형식을 설정할 수 있다고 한다.

```sh
LogFormat "%h %l %u %t \"%r\" %>s %b %D \"%{Referer}i\" \"%{User-Agent}i\"" combined  
CustomLog "| /~<del>/apache/bin/rotatelogs -l /</del>~/logs/apache/access.log.%Y%m%d 86400" combined env=!nolog-request  
```

결과적으로 생성된 엑세스 로그는 다음과 같다.

```sh
123.123.123.123 - - [12/Apr/2018:17:03:50 +0900] "GET /api/aaaa HTTP/1.1" 200 34 1468 "https://m.naver.com" "Mozilla/5.0 (iPhone; CPU iPhone OS 11_3 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Mobile/15E216 NAVER(inapp; search; 580; 8.6.3; 7)"  
```



| 로그 데이터                    | 의미                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| 123.123.123.123                | 원격 호스트 IP 주소(요청자)                                  |
| [12/Apr/2018:17:03:50 +0900]   | 요청 시간                                                    |
| GET /api/aaaa HTTP/1.1         | 'GET' 메서드를 사용하고 '/api/aaaa'라는 경로에 'HTTP/1.1'의 프로토콜로 요청 |
| 200                            | HTTP 상태 코드                                               |
| 34                             | HTTP 헤더를 제외한 전송 바이트 수                            |
| 1468                           | 요청을 처리하는 데 걸린 시간(ms)                             |
| "https://m.naver.com"          | 리퍼러(referrer)                                             |
| ".....맨 뒤의 긴 문자열......" |                                                              |

**원격 호스트** <br>원격 호스트 주소이다. 여기에 나온 IP 주소는 사용자가 사용하는 컴퓨터 주소가 아닐 수 있다. 프록시 서버가 사용자와 서버사이에 존재한다면, 원래 컴퓨터 주소가 아니라 프록시의 주소가 기록될 것이다.

**요청시간**<br>서버가 요청처리를 마친 시간. 형식은 다음과 같다.
[day/month/year:hour:minute:second zone] 
day = 숫자 2개 month = 숫자 3개 year = 숫자 4개 hour = 숫자 2개 minute = 숫자 2개 second = 숫자 2개 zone = (`+' | `-') 숫자 4개

**GET**<br>GET /apache_pb.gif HTTP/1.0"` (`\"%r\") 의 형식이라고 하자.<br>
클라이언트의 요청줄이 쌍따옴표로 묶여있다. 요청줄은 매우 유용한 정보를 담고 있다. <br>첫째, 클라이언트가 사용한 메써드는 `GET`이다.<br>둘째, 클라이언트는 자원 `/apache_pb.gif`를 요청한다. <Br>세번째, 클라이언트는 `HTTP/1.0` 프로토콜을 사용한다. 

**200**<br>
이는 서버가 클라이언트에게 보내는 상태코드이다. 이 정보는 (2로 시작하는 코드) 요청이 성공하였는지, (4로 시작하는 코드) 클라이언트에 오류가 있는지, (5로 시작하는 코드) 서버에 오류가 있는지 알려주므로 매우 중요하다. <br><https://ko.wikipedia.org/wiki/HTTP_%EC%83%81%ED%83%9C_%EC%BD%94%EB%93%9C> 에서 전체 목록을 살펴볼 수 있다. 



# 아파치 로그파일

로그 기록 내용의 유형은 다음과 같다. 

211.36.215.78 -  manager [22/Jun/2000:23:09:09 +0900] "GET / HTTP/1.1" 200 5

178.154.210.252 - - [20/Jun/2012:19:54:10 +0200] "GET /?C=S;O=A HTTP/1.1" 200 663 "-" "Mozilla/5.0 (compatible; YandexBot/3.0; +http://yandex.com/bots)"   ...

즉 사용자가 정의한 내용별로 그 기록의 유형이 다르다. 어떻게 웹 로그를 남기기로 정의하였고, 어떤것을 기록에 남겼는지를 알고 있어야 데이터분석이 수월해진다. 

# Reference

- https://d2.naver.com/helloworld/3585246

  