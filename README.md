# Media Web Application

## 📋 프로젝트 개요
Media Web Application은 다양한 미디어 콘텐츠를 스트리밍하고 사용자 경험을 극대화할 수 있는 플랫폼입니다.  
**주요 목표**:
- 사용자가 간편하게 콘텐츠를 검색 및 재생
- 다양한 세부 기능들을 통해 편리하게 이용 가능

---

## 🛠️ 개발 계획
1. **기획**  
   - 서비스 핵심 기능 설계 및 화면 레이아웃 정의  
   - 주요 사용 시나리오 설계
   - 패널 동적이동에 따른 앱 사용 설계
   - 각종 세부 기능 설계  

2. **프론트엔드**  
   - UI/UX 설계 및 개발  
   - 반응형 웹 구현
   - 기본기능 구현
   - 심화기능 구현

3. **백엔드**  
   - 사용자 인증 및 데이터 관리 API 개발  
   - 미디어 콘텐츠 스트리밍 서버 구축 (로컬로 대체)  

4. **통합 테스트 및 배포**  
   - 프론트엔드와 백엔드의 기능 통합 및 최적화  


---

## 🎭 역할 분담
- **프론트엔드 개발**: 임대규, 김민규  
- **백엔드 개발**: 고귀현, 김택림  

---

## 📌 진행 사항
1. 프로젝트 초기 기획 완료  
2. UI/UX 와이어프레임 설계 진행 중  
3. GitHub Repository 구성 완료
4. 기본 기능 구현 완료
5. 추가 기능 구현 완료
   
---

## 📂 프로젝트 디렉토리 구조

각 디렉토리 별 자료 구조:

[frontend]
```bash
__mocks__
├── @enact
│   └── webos
│       └── LS2Request.js
├── com.webos.applicationManager
│   └── launch.json
├── com.webos.memorymanager
│   ├── getProcStat-2136700690.json
│   └── getUnitList-1886768026.json
└── com.webos.service.tv.systemproperty
    └── getSystemInfo-533910236.json
resources
└── ilibmanifest.json
src
├── App
│   ├── App.js
│   ├── App.test.js
│   ├── AppState.js
│   └── package.json
├── assets
│   ├── 3.jpg
│   ├── video0.jpg
│   ├── video1.jpg
│   ├── video2.jpg
│   ├── video3.jpg
│   ├── video4.jpg
│   ├── video5.jpg
│   ├── video6.jpg
│   ├── ㄴ.jpg
│   └── ㅇ.jpg
├── constants
│   └── domEvents.js
├── hooks
│   └── useData.js
├── index.js
├── libs
│   ├── log.js
│   ├── request.js
│   ├── services.js
│   ├── svg.js
│   ├── testutils.js
│   └── utils.js
└── views
    ├── Context.js
    ├── DetailPanel.js
    ├── Login.js
    ├── Login.module.less
    ├── LoginState.js
    ├── LogoutState.js
    ├── LunaAPI.js
    ├── Main.js
    ├── Main.module.less
    ├── MainState.js
    ├── SettingPanel.js
    ├── Signup.js
    ├── Signup.module.less
    ├── SignupState.js
    ├── VideoManager.js
    ├── VideoPlayer.css
    ├── VideoPlayer.js
    ├── address.js
    ├── comments.js
    ├── lunaUtils.js
    ├── playlist.js
    ├── statusCheck.js
    ├── systemMonitor.js
    ├── systemUtils.js
    ├── useBackHandler.js
    └── useWatchedVideos.js
webos-meta
├── appinfo.json
└── icon.png
```

[backend]
```bash
.
├── Dockerfile
├── HELP.md
├── README.md
├── build.gradle
├── gradle
│   └── wrapper
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── gradlew
├── gradlew.bat
├── settings.gradle
└── src
    ├── main
    │   ├── java
    │   │   ├── WebConfig
    │   │   │   └── WebConfig.java
    │   │   └── com
    │   │       └── example
    │   │           └── demo
    │   │               ├── DemoApplication.java
    │   │               ├── controller
    │   │               │   ├── CommentController.java
    │   │               │   ├── FileUploadController.java
    │   │               │   ├── IPAddressUtil.java
    │   │               │   ├── IPController.java
    │   │               │   ├── LinkedPlaylistController.java
    │   │               │   ├── PlaylistController.java
    │   │               │   ├── UserController.java
    │   │               │   ├── VideoController.java
    │   │               │   ├── VideoUploadController.java
    │   │               │   └── VideowatchedController.java
    │   │               ├── model
    │   │               │   ├── Comment.java
    │   │               │   ├── LinkedPlaylist.java
    │   │               │   ├── Playlist.java
    │   │               │   ├── User.java
    │   │               │   ├── Video.java
    │   │               │   └── Videowatched.java
    │   │               ├── repository
    │   │               │   ├── CommentRepository.java
    │   │               │   ├── LinkedPlaylistRepository.java
    │   │               │   ├── PlaylistRepository.java
    │   │               │   ├── UserRepository.java
    │   │               │   ├── VideoRepository.java
    │   │               │   └── VideowatchedRepository.java
    │   │               └── service
    │   │                   ├── CommentService.java
    │   │                   ├── LinkedPlaylistService.java
    │   │                   ├── PlaylistService.java
    │   │                   ├── UserService.java
    │   │                   ├── VideoService.java
    │   │                   └── VideowatchedService.java
    │   └── resources
    │       ├── application.properties
    │       ├── templates
    │       │   └── register.html
    │       ├── thumbnails
    │       │   ├── 1.jpg
    │       │   ├── 10.jpg
    │       │   ├── 11.jpg
    │       │   ├── 12.jpg
    │       │   ├── 13.jpg
    │       │   ├── 14.jpg
    │       │   ├── 15.jpg
    │       │   ├── 16.jpg
    │       │   ├── 17.jpg
    │       │   ├── 18.jpg
    │       │   ├── 19.jpg
    │       │   ├── 2.jpg
    │       │   ├── 20.jpg
    │       │   ├── 21.jpg
    │       │   ├── 22.jpg
    │       │   ├── 3.jpg
    │       │   ├── 4.jpg
    │       │   ├── 5.jpg
    │       │   ├── 6.jpg
    │       │   ├── 7.jpg
    │       │   ├── 8.jpg
    │       │   └── 9.jpg
    │       └── videos
    │           ├── 1.mp4
    │           ├── 10.mp4
    │           ├── 11.mp4
    │           ├── 12.mp4
    │           ├── 13.mp4
    │           ├── 14.mp4
    │           ├── 15.mp4
    │           ├── 16.mp4
    │           ├── 17.mp4
    │           ├── 18.mp4
    │           ├── 19.mp4
    │           ├── 2.mp4
    │           ├── 20.mp4
    │           ├── 21.mp4
    │           ├── 22.mp4
    │           ├── 3.mp4
    │           ├── 4.mp4
    │           ├── 5.mp4
    │           ├── 6.mp4
    │           ├── 7.mp4
    │           ├── 8.mp4
    │           └── 9.mp4
    └── test
        └── java
            └── com
                └── example
                    └── demo
                        └── DemoApplicationTests.java
```

### Explanation of Key Directories and Files:
- `__mocks__/`  
  Contains mock files used for unit tests or test simulations.

- `resources/`  
  Stores static resources, such as images, fonts, or configuration files.

- `src/`  
  The main source code directory, which contains components, logic, and application features.

- `webos-meta/`  
  Metadata specific to WebOS platform development.

- `.eslintignore` & `.eslintrc`  
  Files related to ESLint, used to enforce coding standards and ignore specified files.

- `.prettierrc`  
  Configuration file for Prettier, ensuring consistent code formatting.

- `HOW-TO-TEST.md`  
  A guide on how to test the application.

- `README.md`  
  Contains detailed information about the project, setup, and usage instructions.

- `com.app.enact-template_1.0.0_all.ipk`  
  A packaged version of the application ready for deployment.

- `next.config.js`  
  Configuration file for the Next.js framework.

- `package.json` & `package-lock.json`  
  Contain project metadata and a locked version of installed dependencies.


4. Documents : test plan, architectural drivers 등 개발 문서가 들어 있는 디렉토리

---
