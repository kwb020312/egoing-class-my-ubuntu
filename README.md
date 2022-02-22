해당 글은 생활코딩님의 <a href="https://youtu.be/cqlY1Hc70H0">github 로 Docker image 공유하기</a> 를 보고 제작되었음을 밝힙니다.

먼저 깃허브 개인 액세스 토큰 탭에 접근하여 토큰을 생성해준다.

이 기능은 자신의 깃허브 저장소에 접근 가능하도록 권한을 부여하는것에 필요함

<a href="https://github.com/settings/tokens">![image](https://user-images.githubusercontent.com/46777310/155155610-4be9163c-96a9-4f4f-8f80-30efbb54493a.png)</a>

※ 사진을 클릭하면 이동합니다.

Generate new token을 눌러 생성 준비를 한다.

1. Note에 간단한 설명을 명시
2. Select scopes에서 write:packages 와 read:packages를 체크해주어 접근권한 허용

![image](https://user-images.githubusercontent.com/46777310/155157066-dabd68cd-d71b-4810-8f9a-3b6e838b902a.png)

※ 이후 표시되는 액세스 코드는 꼭 복사해둔다.

![image](https://user-images.githubusercontent.com/46777310/155157688-2db6e842-46fc-4698-8a0d-62bee35f1fe3.png)

ghcr.io 에 아이디와 방금 표시되는 액세스 코드를 입력하여 로그인 하면 경고 메시지가 출력된다.

--password-stdin 을 -p 대신 사용하면 안전하다는 의미이며 -stdin 옵션은 환경변수를 사용하여 echo 할 때 해당 결과물을 받는 옵션이다.

![image](https://user-images.githubusercontent.com/46777310/155158209-8c71a8b0-53e9-4fe8-a347-58d1364e1e91.png)

set 을 통해 환경변수를 선언한다

※ 이 때 리눅스 환경이라면 export를 사용한다.

잘 저장되었는지 확인하려면

echo %환경변수% 를 사용한다

※ 이 때 리눅스 환경이라면 echo $환경변수 를 사용한다.

![image](https://user-images.githubusercontent.com/46777310/155158801-099569c0-1c09-4fa1-91da-03551d8909cf.png)

echo 로 출력함과 동시에 | 를 사용하여 --password-stdin 옵션에 적용시켜준다.

![image](https://user-images.githubusercontent.com/46777310/155159081-b99a08b7-4516-4a95-9eda-3e5735aa0755.png)

docker run 을 통해 my-ubuntu라는 컨테이너를 ubuntu 이미지를 사용하여 생성

![image](https://user-images.githubusercontent.com/46777310/155159539-c0e93559-d0b5-4cea-8d55-ea5971dc8dc8.png)

docker commit 을 통해 my-ubuntu를 ghcr.io/사용자명/이미지:버전 으로 스테이징

![image](https://user-images.githubusercontent.com/46777310/155159890-9cd82dc8-48c2-44b6-b253-5d893829c614.png)

docker push 를 사용해 docker push (스테이징시 사용한 경로) 를 설정하여 원격 저장소에 업로드

위와 같은 방법으로 github를 통해 Docker image를 공유할 수 있다.

docker hub를 사용하면 유료로 전환될 수 있기에 github 방법을 알아보았음
