# Media Web Application의 시청 서비스 TEST Plan

## Backend Unit Test Cases
backend api의 검증은 curl명령어를 사용하여 직접 server에 api요청을 해 검증한다.

API   | Test Name |  TEST Case ID  | Description | Test Data
---   |   --- |   ---   | ---      | ---
/api/register    | 데이터베이스에 회원 정보 생성하기 | TC01-1   |  Status code is 200: api의 response의 status 코드가 200이면 pass한다. | {"username": "macchiato", "password": "123qwe","userbirth": "2001-01-15"}
/api/register   | 데이터베이스에 회원 정보 생성하기-중복 회원 오류 | TC01-2   |  <li>Status code is 400: api의 response의 status 코드가 400이면 pass한다.</li> | {"username": "taeklim", "password": "123qwe","userbirth": "2001-01-15"}
/api/login | 데이터베이스에 있는 회원 정보와 비교하기 | TC02-1  | <li> Status code is 200: api의 response의 status 코드가 200이면 pass한다.</li> | {"username": "taeklim", "password": "123qwe"}
/api/login | 데이터베이스에 있는 회원 정보와 비교하기-잘못된 username, password | TC02-2 | <li> Status code is 401: api의 response의 status 코드가 401이면 pass한다.</li> | {"username": "taeklim", "password": "123qwe!"}
/api/logout | session 초기화를 통해 로그아웃하기 | TC02-3 | <li> Status code is 200: api의 response의 status 코드가 200이면 pass한다.</li> | 
/api/ip | 서버의 ip 가져오기-실패  | TC03-1 | <li>api의 response가 "Unable to determine IP address"라면 성공</li> | 
/api/thumbnail/{filename} | 영상의 thumbnail 가져오기 | TC04-1 | <li> Status code is 200: api의 response의 status 코드가 200이면 pass한다.</li> | {"filename": "1"}
/api/thumbnail/{filename} | 영상의 thumbnail 가져오기-파일 존재하지 않음 | TC04-2 | <li> Status code is 500: api의 response의 status 코드가 500이면 pass한다.</li> | {"filename": "100"}
/api/video_title/{filename} | 영상의 title 가져오기 | TC04-3    | <li> Status code is 200: api의 response의 status 코드가 200이면 pass한다.</li> | {"filename": "1"}
/api/video_title/{filename} | 영상의 title 가져오기-파일 이름 Long 변환 불가 | TC04-4    | <li> Status code is 400: api의 response의 status 코드가 400이면 pass한다.</li> | {"filename": "hi"}
/api/num_of_videos | 영상의 개수 가져오기 | TC04-5    | <li> Status code is 200: api의 response의 status 코드가 200이면 pass한다.</li> | 
/api/hls/{filename} | HLS를 위한 파일 가져오기  | TC04-6 | <li>Status code is 200: api의 response의 status 코드가 200이면 pass한다.</li> | {"filename": "1"}
/api/hls/{filename} | HLS를 위한 파일 가져오기-파일 존재하지 않음  | TC04-7 | <li>Status code is 404: api의 response의 status 코드가 404이면 pass한다.</li> | {"filename": "100"}
/api/video/{filename} | 비디오 스트리밍을 위한 파일 가져오기 | TC04-8 | <li> Status code is 200: api의 response의 status 코드가 200이면 pass한다.</li> | {"filename": "1", "rangeHeader": NULL}
/api/video/{filename} | 비디오 스트리밍을 위한 파일 가져오기-일부 가져오기 | TC04-9 | <li> Status code is 206: api의 response의 status 코드가 206이면 pass한다.</li> | {"filename": "1", "rangeHeader": "0-50"}
/api/upload | 영상 업로드 하기 | TC05-1 |<li> Status code is 200: api의 response의 status 코드가 200이면 pass한다.</li> | {"file":"123.mp4", "title":"123"}
/api/upload | 영상 업로드 하기-잘못된 확장자 | TC05-2 |<li> api의 response가 "Invalid file. Please upload an MP4 file."라면 성공 </li> | {"file":"123.avi", "title":"123"}
/api/videowatched/record | 데이터베이스에 시청한 영상 정보 저장하기 | TC06-1 |<li> Status code is 200: api의 response의 status 코드가 200이면 pass한다.</li> | {"a":"1", "b":"70", "c":"3"}
/api/videowatched/record | 데이터베이스에 시청한 영상 정보 저장하기-잘못된 유저,비디오 정보 | TC06-2 |<li> Status code is 400: api의 response의 status 코드가 400이면 pass한다.</li> | {"a":"100", "b":"100", "c":"3"}
/api/videowatched/{userId} | 데이터베이스에서 특정 user가 시청한 비디오 목록 가져오기 | TC06-3 |<li> Status code is 200: api의 response의 status 코드가 200이면 pass한다.</li> | {"userId":"70", "page":"0", "size":"10"}
/api/videowatched/{userId}/{videoId} | 데이터베이스에서 특정 user의 특정 비디오 시청기록 가져오기 | TC06-4 |<li> Status code is 200: api의 response의 status 코드가 200이면 pass한다.</li> | {"userId":"70", "videoId":"1"}
/api/makePlaylist | 데이터베이스에 플레이리스트 생성하기 | TC07-1 |<li> Status code is 200: api의 response의 status 코드가 200이면 pass한다.</li> | {"userId":"70", "title":"개"}
/api/getPlaylist/{userId} | 데이터베이스에서 특정 사용자가 만든 playlist가져오기 | TC07-2 |<li> Status code is 200: api의 response의 status 코드가 200이면 pass한다.</li> | {"userId":"70", "page":"0", "size":"10"}
/api/addPlaylist | 특정 플레이리스트에 비디오 저장하기 | TC07-3 |<li> Status code is 200: api의 response의 status 코드가 200이면 pass한다.</li> | {"videoId":"12","playlistId":"3"}
/api/addPlaylist | 특정 플레이리스트에 비디오 저장하기-중복 영상 저장 | TC07-4 |<li> Status code is 400: api의 response의 status 코드가 400이면 pass한다.</li> | {"videoId":"1","playlistId":"3"}
/api/addPlaylist | 특정 플레이리스트에 비디오 저장하기-잘못된 playlist,잘못된 video | TC07-5 |<li> Status code is 500: api의 response의 status 코드가 500이면 pass한다.</li> | {"videoId":"100","playlistId":"100"}
/api/playlist/{playlistId} | 특정 플레이리스트의 비디오 목록 가져오기 | TC07-6 |<li> Status code is 200: api의 response의 status 코드가 200이면 pass한다.</li> | {"playlistId":"3"}
/api/comment/create | 특정 비디오에 댓글 달기 | TC08-1 |<li> Status code is 200: api의 response의 status 코드가 200이면 pass한다.</li> | {"galaxy":"1", "userId":"70", "content":"강아지가 귀엽네요"}
/api/comment/create | 특정 비디오에 댓글 달기-잘못된 video, 잘못된 user | TC08-2 |<li> Status code is 500: api의 response의 status 코드가 500이면 pass한다.</li> | {"galaxy":"100", "userId":"100", "content":"강아지가 귀엽네요"}
/api/comment/create | 특정 비디오에 댓글 달기-잘못된 인자 전달 | TC08-3 |<li> Status code is 400: api의 response의 status 코드가 400이면 pass한다.</li> | {"galaxy":NULL, "userId":NULL, "content":"강아지가 귀엽네요"}
/api/comment/like | 특정 비디오에 달린 댓글에 좋아요 누르기 | TC08-4 |<li> Status code is 200: api의 response의 status 코드가 200이면 pass한다.</li> | {"commentId":"47"}
/api/comment/like | 특정 비디오에 달린 댓글에 좋아요 누르기-잘못된 comment | TC08-5 |<li> Status code is 500: api의 response의 status 코드가 500이면 pass한다.</li> | {"commentId":"500"}
/api/comment/like | 특정 비디오에 달린 댓글에 좋아요 누르기-잘못된 인자 전달 | TC08-6 |<li> Status code is 400: api의 response의 status 코드가 400이면 pass한다.</li> | {"commentId":NULL}
/api/comment/dislike | 특정 비디오에 달린 댓글에 싫어요 누르기 | TC08-7 |<li> Status code is 200: api의 response의 status 코드가 200이면 pass한다.</li> | {"commentId":"47"}
/api/comment/dislike | 특정 비디오에 달린 댓글에 싫어요 누르기-잘못된 comment | TC08-8 |<li> Status code is 500: api의 response의 status 코드가 500이면 pass한다.</li> | {"commentId":"500"}
/api/comment/dislike | 특정 비디오에 달린 댓글에 싫어요 누르기-잘못된 인자 전달 | TC08-9 |<li> Status code is 400: api의 response의 status 코드가 400이면 pass한다.</li> | {"commentId":NULL}
/api/comment/{videoId} | 특정 비디오에 달린 댓글 목록 가져오기 | TC08-10 |<li> Status code is 200: api의 response의 status 코드가 200이면 pass한다.</li> | {"videoId":"1", "page":"0", "size":"10"}

## Frontend System Test Cases
Frontend의 사용자 interaction과 view는 use case를 기반으로한 system test를 한다.

### 1. 세션 목록 조회하기
Test Case ID: TC11-1

Test Step  | Test Data | Expected Result
--- |   --- |   ---
사용자가 시스템에 접속한다. |  http://tvmedia.lge.com:3000  |   세션 ID와 content_info 필드 값이 화면에 출력된다.
사용자가 session 목록 보기 탭을 클릭한다. | 　  |   세션 ID와 content_info 필드 값이 화면에 출력된다.
----

### 2. 세션 별 품질 정보 조회하기
Test Case ID: TC12-1

Test Step  | Test Data | Expected Result
--- |   --- |   ---
사용자가 시스템에 접속한다. |  http://tvmedia.lge.com:3000  |   세션 ID와 content_info 필드 값이 화면에 출력된다.
사용자가 session 목록 보기 탭을 클릭한다.  | 　  |   세션 ID와 content_info 필드 값이 화면에 출력된다.
사용자가 특정 세션을 클릭한다. |  　 |   <li> 세션의 품질 정보의 차트가 화면에 출력된다.</li><li> 세션의 품질 통계 정보가 화면에 출력된다.</li>
----

### 3. URL 목록 조회하기
Test Case ID: TC13-1

Test Step  | Test Data | Expected Result
--- |   --- |   ---
사용자가 시스템에 접속한다. |  http://tvmedia.lge.com:3000  |   세션 ID와 content_info 필드 값이 화면에 출력된다.
사용자가 URL 별 목록 보기 탭을 클릭한다. |  　 |    데이터베이스에 존재하는 url을 중복 없이 화면에 출력된다.
----

### 4. URL 별 통계 정보 조회하기
Test Case ID: TC14-1

Test Step  | Test Data | Expected Result
--- |   --- |   ---
사용자가 시스템에 접속한다. |  http://tvmedia.lge.com:3000  |   세션 ID와 content_info 필드 값이 화면에 출력된다.
사용자가 URL 별 목록 보기 탭을 클릭한다. |  　 |    데이터베이스에 존재하는 url을 중복 없이 화면에 출력된다.
사용자가 특정 url을 클릭한다. |  　 |    해당하는 모든 url의 품질 정보 통계 데이터가 화면에 출력된다.
----

### 5. 세션 목록 삭제하기
Test Case ID: TC15-1

Test Step  | Test Data | Expected Result
--- |   --- |   ---
사용자가 시스템에 접속한다. |  http://tvmedia.lge.com:3000  |   세션 ID와 content_info 필드 값이 화면에 출력된다.
사용자가 session 목록 보기 탭을 클릭한다.  | 　  |   세션 ID와 content_info 필드 값이 화면에 출력된다.
사용자가 특정 세션의 체크박스를 클릭하고 삭제 버튼을 누른다. | 　  |    선택한 세션이 삭제된 세션 목록이 화면에 출력된다.
----
