# Cocoa Pod 이용하기
<br/><br/>
<br/><br/>
CLI(Command Line Interface) : DOS창, 터미널창(Terminal)

Cocoa Pod 이용순서
<br/><br/>
0. 기본 xcodeproj프로젝트 닫기<br/>
1. 파인더에서 프로젝트폴더 오른쪽 클릭해서 현재폴더에서 터미널 열기<br/>
2. Cocoa Pod 유틸 설치
   명령어: sudo gem install cocoapods 엔터
   Cocoa Pod 업데이트
   명령어: pod repo update 엔터<br/>
3. 프로젝트 초기화
  명령어: pod init<br/>
4. 라이브러리 설치
  명령어: pod install<br/>
5. 프로젝트열기: xcocdeproj -> xcworkspace 열기
  워크스페이스 열기: 더블클릭 하거나 터미널 open 프로젝트이름.xcworkspace<br/>
6. Xcode에서 pod 파일을 편집하기( 라이브러리 목록 기술 )<br/>
7. 터미널에서 pod install 한번 더하기<br/>
<br/><br/>
터미널 명령어 - 리눅스 명령어
1. pwd : 현재 폴더(디렉토리) 위치 보기
2. ls : 파일 목록 보기
3. ls -all : 파일 목록 자세히 보기
4. open : 파일 열기(실행)
