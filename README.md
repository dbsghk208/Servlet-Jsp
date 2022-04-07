
# 목차

- [1.학습안내](https://github.com/dbsghk208/Servlet-Jsp/blob/main/yun/%ED%95%99%EC%8A%B5%EC%95%88%EB%82%B4.md)
- [2.웹서버프로그램](#2강,-웹-서버-프로그램)




# 4강 톰캣 설치

![EC0DF0FB-9599-43ED-9567-0348684BC160](https://user-images.githubusercontent.com/89206108/162215842-1434cd91-f7f5-4ab9-a2d9-993c2509c212.png)



톰캣 installer 버전이 서비스 사용시 설치하는 파일!!

1) 설치파일이기때문에 자동 설치가 되고

2) 서비스 목록에 등록이 된다.

[https://www.notion.so](https://www.notion.so)

컴퓨터에는 부팅되자마자 저절로 실행되는 서비스 목록들이 있는데

installer 파일을 다운해서 풀면 

그 서비스 목록에 톰캣이 등록이 된다는것

그래서 컴퓨터 껐다 켜도 저절로 실행이 된다는것.

![7BAF916D-FCD6-4C6E-9963-CCD36C0881CE](https://user-images.githubusercontent.com/89206108/162215967-753982bd-0720-4951-8ac8-c657b67fab94.png)



![AEF5A366-1046-4F18-8F30-45C5D5D95ECD](https://user-images.githubusercontent.com/89206108/162215999-05eba58a-a65b-46c3-8316-face78bddb88.png)


startup.bat

실행하면 원래 cld 창이 나오고 그대로 있어야 한다.

그런데 cld 창이 없어져버리면

톰캣을 실행할 수 있는 환경이 아닌것

 jdk환경변수가  JAVA_HOME 이 환경변수 등록이 안되서 그런 것일 수 있음

JAVA_HOME 이란

JDK 를 필요로 하는 어플리케이션이 있을것 

대표적인게 JAVA_HOME 이 있는데 그게 바로 톰캣.

톰캣은 이 디렉토리가 즉,  jdk 가 어디에 설치되어있는지 알아야 하는데

그건 사용자마다 설치한 곳이 다르기 때문에 

그 jdk가 설치되어있는 곳을 약속해놓은게 

JAVA_HOME

그래서 jdk를 사용한 어플리케이션들은 환경변수를 찾아서 거기에 등록되어잇는지 디렉토리를 확인해 보게끔 되어있는데

자바홈에 등록이 안되어잇으면 jdk 를 확인 할수 없기 때문에 

환경변수 설정을 해주는것

그래서 톰캣 사용전에 jdk 환경변수 설정이 필수 인것.

아니면 다른 톰캣이 동작 중이어서 포트가 사용중이어서 스타트업 배트 파일이 실행이 안되는 것일수도 있음

브라우저에 주소를 치는데

localhost8080 톰캣이 정상적으로 작동하면 고양이 모양이 나옴

원래는 startup.bat 을 켠 다음 [localhost](http://localhost)8080 으로 연결하게 되어있음

그런데 오늘 회사에서는 타임아웃 만 만져주고 

[http://localhost:8080](http://localhost:8080)

이렇게 쳐주니깐 되었음

톰캣폴더내의 타임아웃 시간과

이클립스 서버에서의 타임아웃 시간 만져줌!



