

#  Media Web Application Backend REST API Reference

### 1. 회원가입하기

회원 가입은 데이터베이스에 저장 요청 받은 회원 정보인 username, password, userbirth를 user스키마에 맞게 파싱하여 데이터베이스에 회원 정보 세션을 생성하고, 생성 성공여부에 대한 message를 응답합니다.

#### Request

| ID      | URL           | HOST                      | METHOD |
| ------- | ------------- | ------------------------- | ------ |
| BA01-1  | /api/register | http://{ip\_address}:8080 | POST   |

---

#### Parameter

| Name      | Type      | Description      | Required |
| --------- | --------- | ---------------- | -------- |
| username  | String    | 가입자의 이름     | TRUE     |
| password  | String    | 가입자의 비밀번호 | TRUE     |
| userbirth | LocalDate | 가입자의 생년월일 | TRUE     |

---

#### Response

| Name               | Type   | Description                            |
| ------------------ | ------ | -------------------------------------- |
| message            | String | username 중복 시 실패, 중복 아닐 시 성공 |

---

### 2. 로그인, 로그아웃하기

사용자 식별을 위해 backend 서버의 데이터베이스에 저장되어 있는 회원 정보 세션의 username과 password를 활용하는 API입니다.

#### 2.1. 로그인하기

데이터베이스에 저장되어 있는 username과 password를 비교해 로그인 성공 여부를 전달하는 API입니다.

#### Request

| ID      | URL        | HOST                      | METHOD |
| ------- | ---------- | ------------------------- | ------ |
| BA02-1  | /api/login | http://{ip\_address}:8080 | POST   |


---

#### Parameter

| Name      | Type      | Description      | Required |
| --------- | --------- | ---------------- | -------- |
| username  | String    | 가입자의 이름     | TRUE     |
| password  | String    | 가입자의 비밀번호 | TRUE     |

---

#### Response

| Name               | Type   | Description                                                        |
| ------------------ | ------ | ------------------------------------------------------------------ |
| message            | String | username과 password가 일치하는 record 존재 시 로그인 성공, 없으면 실패 |
| userId             | String | 로그인한 user의 Id 반환                                              |
| username           | String | 로그인 한 user의 username 반환                                       |

---

#### 2.2. 로그아웃하기

현재 front에서 사용되고 있는 세션을 종료시켜 로그아웃을 처리하는 API입니다.

#### Request

| ID     | URL         | HOST                      | METHOD |
| ------ | ----------- | ------------------------- | ------ |
| BA02-2 | /api/logout | http://{ip\_address}:8080 | POST   |

---

#### Response

| Name               | Type   | Description  |
| ------------------ | ------ | ------------ |
| message            | String | 로그아웃 성공 |

---

### 3. 서버 IP주소 요청

서버의 IP 주소를 조회하기 위해 사용되는 API입니다.

#### Request

| ID     | URL     | HOST                       | METHOD |
| ------ | ------- | -------------------------- | ------ |
| BA03-1 | /api/ip | hhttp://{ip\_address}:8080 | GET    |

---

#### Response

| Name | Type   | Description                                                   |
| ---- | ------ | ------------------------------------------------------------- |
| IPv4 | String | IP주소를 찾았을 경우 IPv4주소를 반환하고 실패시 실패 메시지를 반환 |

---

### 4. 영상 관리

영상 가져오기, 영상 썸네일, 영상 제목 등을 관리하기 위한 API입니다.

#### 4.1. 쎔네일 생성 및 반환

특정 video파일의 thumbnail을 가져오는데 해당 video파일에 대한 thumbnail이 이미 있으면 해당 thumbnail파일을 반환하고 없으면 해당 video가 1초일 때의 화면을 thumbnail로 저장한 뒤 해당 thumbnail파일을 반환하는 API입니다.

#### Request

| ID     | URL                       | HOST                      | METHOD |
| ------ | ------------------------- | ------------------------- | ------ |
| BA04-1 | /api/thumbnail/{filename} | http://{ip\_address}:8080 | GET   |

---

#### Parameter

| Name       | Type     | Description              | Required |
| ---------- | -------- | ------------------------ | -------- |
| filename   | String   | 요구하는 영상의 file이름  | TRUE     |

---

#### Response

| Name         | Type   | Description                 |
| ------------ | ------ | --------------------------- |
| Content-Type | String | 반환하는 thumbnail의 확장자  |
| Body         | binary | thumbnail파일의 binary data |

---

#### 4.2. 비디오 제목

특정 비디오의 제목을 가져오는데 사용되는 API입니다.

#### Request

| ID     | URL                         | HOST                      | METHOD |
| ------ | --------------------------- | ------------------------- | ------ |
| BA04-2 | /api/video_title/{filename} | http://{ip\_address}:8080 | GET    |

---

#### Parameter

| Name       | Type     | Description              | Required |
| ---------- | -------- | ------------------------ | -------- |
| filename   | String   | 요구하는 영상의 file이름  | TRUE     |

---

#### Response

| Name     | Type   | Description                                                   |
| -------- | ------ | ------------------------------------------------------------- |
| response | String | video제목을 찾았다면 성공 message 반환, 실패시 실패 message 반환 |

---

#### 4.3. 비디오 개수

데이터베이스에 저장되어 있는 비디오의 개수를 반환하는 API입니다.

#### Request

| ID     | URL                | HOST                      | METHOD |
| ------ | ------------------ | ------------------------- | ------ |
| BA04-3 | /api/num_of_videos | http://{ip\_address}:8080 | GET    |

---

#### Response

| Name | Type | Description           |
| ---- | ---- | --------------------- |
| rtr  | Long | DB의 비디오 개수를 반환 |

---

#### 4.4. HLS파일 가져오기

HLS를 위한 .m3u8 파일과 .ts 비디오 세그먼트 파일을 제공하는 api입니다.

#### Request

| ID     | URL                 | HOST                      | METHOD |
| ------ | ------------------- | ------------------------- | ------ |
| BA04-4 | /api/hls/{filename} | http://{ip\_address}:8080 | GET    |

---

#### Parameter

| Name       | Type     | Description              | Required |
| ---------- | -------- | ------------------------ | -------- |
| filename   | String   | 요구하는 영상의 file이름   | TRUE     |

---

#### Response

| Name         | Type   | Description              |
| ------------ | ------ | ------------------------ |
| Content-Type | String | 반환하는 hls파일의 확장자  |
| Body         | binary | hls파일의 binary data    |

---

#### 4.5. 비디오 파일 가져오기

비디오 파일을 스트리밍하기 위한 API입니다.

#### Request

| ID     | URL                   | HOST                      | METHOD |
| ------ | --------------------- | ------------------------- | ------ |
| BA04-5 | /api/video/{filename} | http://{ip\_address}:8080 | GET    |

---

#### Parameter

| Name        | Type     | Description              | Required |
| ----------- | -------- | ------------------------ | -------- |
| filename    | String   | 요구하는 영상의 file이름   | TRUE    |
| rangeHeader | String   | 요청하는 파일 범위        | FALSE    |

---

#### Response

| Name         | Type   | Description             |
| ------------ | ------ | ----------------------- |
| Content-Type | String | 반환하는 파일의 확장자    |
| Body         | binary | 비디오파일의 binary data |

---

### 5. 영상 업로드

사용자가 업로드한 비디오 파일(mp4)를 저장하고, HLS 스트리밍 파일과 썸네일 이미지를 생성하는 API입니다.

#### Request

| ID      | URL         | HOST                      | METHOD |
| ------- | ----------- | ------------------------- | ------ |
| BA05-1  | /api/upload | http://{ip\_address}:8080 | POST   |

---

#### Parameter

| Name     | Type            | Description         | Required |
| -------- | --------------- | ------------------- | -------- |
| file     | MultipartFile   | 업로드할 비디오 파일  | TRUE     |
| title    | String          | 비디오의 제목        | TRUE     |

---

#### Response

| Name      | Type   | Description                    |
| --------- | ------ | ------------------------------ |
| message   | String | 파일 업로드 및 처리 결과 message |
| File Path | String | 업로드 된 파일 저장 경로         |

---

### 6. 시청한 영상 관리

사용자의 시청 기록을 관리하기 위한 API입니다. 이 API는 사용자가 시청한 영상을 저장하거나, 특정 사용자의 시청 영상 목록을 조회하고, 특정 비디오에 대한 시청 시간을 불러올 때 사용됩니다.

#### 6.1. 시청한 영상 저장

특정 사용자가 시청한 비디오와 해당 비디오의 시청 시간, 시점을 기록하기 위한 API입니다.

#### Request

| ID      | URL                      | HOST                      | METHOD |
| ------- | ------------------------ | ------------------------- | ------ |
| BA06-1  | /api/videowatched/record | http://{ip\_address}:8080 | POST   |

---

#### Parameter

| Name        | Type   | Description                 | Required |
| ----------- | ------ | --------------------------- | -------- |
| videoId     | Long   | 사용자가 시청한 video ID     | TRUE     |
| userId      | Long   | 현재 사용자의 ID             | TRUE     |
| watchedTime | Long   | 현재 시청한 비디오의 시청시간 | TRUE     |

---

#### Response

| Name     | Type   | Description                                          |
| -------- | ------ | ---------------------------------------------------- |
| message  | String | 받은 userId, videoId 전부 유효할 시 성공 |

---

#### 6.2. 특정 사용자가 시청한 영상 목록 가져오기

특정 사용자가 시청한 영상 목록을 가져와 pagination을 한 뒤 해당 page에 존재하는 영상 목록을 보여주기 위한 API입니다.

#### Request

| ID      | URL                        | HOST                      | METHOD |
| ------- | -------------------------- | ------------------------- | ------ |
| BA06-2  | /api/videowatched/{userId} | http://{ip\_address}:8080 | GET    |

---

#### Parameter

| Name   | Type   | Description                                   | Required |
| ------ | ------ | --------------------------------------------- | -------- |
| userId | Long   | 현재 사용자의 ID                               | TRUE     |
| page   | int    | Page의 번호(Default = 0)                       | False    |
| size   | int    | Page로 나눌 때 한 page당 영상 수(Default = 10)  | False    |

---

#### Response

| Name        | Type   | Description                        |
| ----------- | ------ | ---------------------------------- |
| totalVideos | Long   | 특정 사용자가 시청한 영상의 총 수    |
| cnt         | int    | 요청한 page에 들어있는 영상 수       |
| videos      | Object | 요청한 page에 들어있는 videos의 목록 |

---

#### 6.3. 특정 사용자의 특정 video에 대한 시청 시간 가져오기

특정 사용자의 특정 비디오에 대한 시청 시간을 가져오기 위한 API입니다.

#### Request

| ID      | URL                                  | HOST                      | METHOD |
| ------- | ------------------------------------ | ------------------------- | ------ |
| BA06-3  | /api/videowatched/{userId}/{videoId} | http://{ip\_address}:8080 | GET    |

---

#### Parameter

| Name    | Type   | Description      | Required |
| ------- | ------ | ---------------- | -------- |
| userId  | Long   | 현재 사용자의 ID  | TRUE     |
| videoId | Long   | 특정 영상의 ID    | TRUE     |

---

#### Response

| Name        | Type   | Description                            |
| ----------- | ------ | -------------------------------------- |
| watchedTime | Long   | 특정 사용자의 특정 비디오에 대한 시청시간 |

---

### 7. playlist

사용자가 playlist를 생성하고 영상을 추가하기 위한 API입니다.

#### 7.1. playlist 생성

사용자가 playlist를 생성하기 위한 API입니다.

#### Request

| ID      | URL               | HOST                      | METHOD |
| ------- | ----------------- | ------------------------- | ------ |
| BA07-1  | /api/makePlaylist | http://{ip\_address}:8080 | POST   |

---

#### Parameter

| Name   | Type   | Description      | Required |
| ------ | ------ | ---------------- | -------- |
| userId | Long   | 현재 사용자의 ID  | TRUE     |
| title  | String | playlist의 제목   | TRUE     |

---

#### Response

| Name     | Type   | Description                            |
| -------- | ------ | -------------------------------------- |
| message  | String | 받은 userId, videoId 전부 유효할 시 성공 |

---

#### 7.2. 특정 사용자가 만든 playlist 목록 가져오기

특정 사용자가 생성한 playlist들의 목록을 보여주기 위한 API입니다.

#### Request

| ID      | URL                       | HOST                      | METHOD |
| ------- | ------------------------- | ------------------------- | ------ |
| BA07-2  | /api/getPlaylist/{userId} | http://{ip\_address}:8080 | GET    |

---

#### Parameter

| Name   | Type   | Description                                        | Required |
| ------ | ------ | -------------------------------------------------- | -------- |
| userId | Long   | 현재 사용자의 ID                                    | TRUE     |
| page   | int    | Page의 번호(Default = 0)                           | False    |
| size   | int    | Page로 나눌 때 한 page당 playlist 수(Default = 10)  | False    |

---

#### Response

| Name           | Type   | Description                          |
| -------------- | ------ | ------------------------------------ |
| totalPlaylists | Long   | 특정 사용자가 생성한 playlist의 총 수  |
| cnt            | int    | 요청한 page에 들어있는 playlist 수     |
| playlists      | Object | 요청한 page에 들어있는 playlist의 목록 |

---

#### 7.3. 특정 playlist에 영상 추가

특정 playlist에 영상을 추가하기 위한 API입니다.

#### Request

| ID      | URL              | HOST                      | METHOD |
| ------- | ---------------- | ------------------------- | ------ |
| BA07-3  | /api/addPlaylist | http://{ip\_address}:8080 | POST   |

---

#### Parameter

| Name       | Type   | Description       | Required |
| ---------- | ------ | ----------------- | -------- |
| videoId    | Long   | 현재 video의 ID    | TRUE     |
| playlistId | Long   | 특정 playlist의 ID | TRUE     |

---

#### Response

| Name    | Type   | Description                                                             |
| ------- | ------ | ----------------------------------------------------------------------- |
| message | String | playlist에 중복된 영상이 존재할 경우 실패, video와 playlist가 유효하면 성공 |

---

#### 7.4. 특정 playlist의 video 목록 가져오기

특정 playlist의 video 목록들을 가져오기 위한 API입니다.

#### Request

| ID      | URL                        | HOST                      | METHOD |
| ------- | -------------------------- | ------------------------- | ------ |
| BA07-4  | /api/playlist/{playlistId} | http://{ip\_address}:8080 | GET    |

---

#### Parameter

| Name       | Type   | Description        | Required |
| ---------- | ------ | ------------------ | -------- |
| playlistId | Long   | 특정 playlist의 ID  | TRUE     |

---

#### Response

| Name            | Type   | Description                  |
| --------------- | ------ | ---------------------------- |
| linkedPlaylists | List   | 특정 playlist에 대한 영상 목록 |

---

### 8. comment

영상에 대한 댓글 기능을 구현하기 위한 API입니다.

#### 8.1. 댓글 생성

특정 영상에 대한 댓글을 생성하기 위한 API입니다.

#### Request

| ID      | URL                 | HOST                      | METHOD |
| ------- | ------------------- | ------------------------- | ------ |
| BA08-1  | /api/comment/create | http://{ip\_address}:8080 | POST   |

---

#### Parameter

| Name     | Type   | Description           | Required |
| -------- | ------ | --------------------- | -------- |
| videoId  | Long   | 현재 video의 ID       | TRUE     |
| userId   | Long   | 댓글 작성한 user의 ID | TRUE     |
| content  | String | 댓글 내용             | TRUE     |

---

#### Response

| Name      | Type   | Description                            |
| --------- | ------ | -------------------------------------- |
| message   | String | 받은 userId, videoId 전부 유효할 시 성공 |
| commentId | String | 생성한 comment의 Id반환                 |

---

#### 8.2. 댓글 좋아요

댓글에 좋아요를 클릭했을 때 좋아요 수를 증가시키는 API입니다.

#### Request

| ID      | URL               | HOST                      | METHOD |
| ------- | ----------------- | ------------------------- | ------ |
| BA08-2  | /api/comment/like | http://{ip\_address}:8080 | POST   |

---

#### Parameter

| Name      | Type   | Description            | Required |
| --------- | ------ | ---------------------- | -------- |
| commentId | Long   | 좋아요 누른 댓글의 ID    | TRUE     |

---

#### Response

| Name      | Type     | Description                |
| --------- | -------- | -------------------------- |
| message   | String   | comment ID가 유효하면 성공  |
| commentId | String   | 좋아요 누른 댓글의 ID 반환   |

---

#### 8.3. 댓글 싫어요

댓글에 싫어요를 클릭했을 때 싫어요 수를 증가시키는 API입니다.

#### Request

| ID      | URL                  | HOST                      | METHOD |
| ------- | -------------------- | ------------------------- | ------ |
| BA08-3  | /api/comment/dislike | http://{ip\_address}:8080 | POST   |

---

#### Parameter

| Name      | Type   | Description         | Required |
| --------- | ------ | ------------------- | -------- |
| commentId | Long   | 싫어요 누른 댓글의 ID | TRUE     |

---

#### Response

| Name      | Type     | Description                |
| --------- | -------- | -------------------------- |
| message   | String   | comment ID가 유효하면 성공  |
| commentId | String   | 싫어요 누른 댓글의 ID 반환   |

---

#### 8.4. 특정 video의 댓글 목록 가져오기

특정 video의 댓글 목록들을 가져오기 위한 API입니다.

#### Request

| ID      | URL                    | HOST                      | METHOD |
| ------- | ---------------------- | ------------------------- | ------ |
| BA08-4  | /api/comment/{videoId} | http://{ip\_address}:8080 | GET    |

---

#### Parameter

| Name    | Type   | Description                                     | Required |
| ------- | ------ | ----------------------------------------------- | -------- |
| videoId | Long   | 현재 video의 ID                                 | TRUE     |
| page    | int    | Page의 번호(Default = 0)                        | False    |
| size    | int    | Page로 나눌 때 한 page당 video 수(Default = 10)  | False    |

---

#### Response

| Name          | Type   | Description                         |
| ------------- | ------ | ----------------------------------- |
| totalComments | Long   | 특정 사용자가 생성한 comment의 총 수  |
| cnt           | int    | 요청한 page에 들어있는 comment 수    |
| comments      | Object | 요청한 page에 들어있는 comment의 목록 |

---