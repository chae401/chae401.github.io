# Git - 활용

## 협업

---

### 1. Github Flow 이해하기

- 브랜치 전략
    - `Git-Flow`
        - **main branch**
            - master : 배포 가능한 생태만을 관리하는 브랜치고 라이브 서버에 처음으로 출시되는 브랜치
            - develop : 다음 출시할 버전을 개발하는 브랜치 → 개발의 기반이 됨
        - **feature/ topic branch**
            
            새로운 기능을 추가할 떄 주로 사용하는 브랜치로, 기능을 완성하면 develop 브랜치로 병합, 결과가 좋지 않으면 삭제
            
        - **release branch**
            - 배포를 위한 최종 버그 수정 드으이 개발을 진행하는 브랜치
            - 배포가 가능해지면 master로 병합하고 버전 태그를 추가함
            - 수정 사항은 develop 브랜치에도 적용
        - **hotfix branch**
            - 배포한 버전에서 긴급하게 구정이 필요할 떄 master 브랜치에서 분리하는 브랜치
            - 오류를 수정하는 인원과 별개로 다른 사람들은 **develop** 브랜치에서 계속 작업할 수 있다.
            - **hotfix**는 보통 오류를 긴급히 수정하기 위해 생성하는 브랜치로, 오류를 해결하면 제거하는 일회성 브랜치
        
    - `GitHub-Flow`
        - 정리
            - GitHub에 적용하기 어려운 Git-Flow를 보완
            - GitHub-FLow는 자동화의 개념이 적용됨
            - Git-Flow와 달리 Pull&Request(PR)을 사용하기 때문에 master branch에 대한 규칙이 정립되어 있다면 다른 브랜치들에 대해서는 특별히 관여 X
        - 흐름
            
            1️⃣**브랜치 생성**
            
            - **master**브랜치는 항상 최신 상태로,**새로운 브랜치는 항상 master브랜치에서 만듭니다.**
            - **feature,develop** 브랜치는 존재하지 않습니다.
            - 새로운 기능을 추가하거나 오류를 해결하기 위한 **브랜치 이름을 자세하게 작성**합니다.
            
            2️⃣**개발**
            
            - **커밋 시 커밋 메시지를 정확히 작성합니다.**
            - master, 또는 중간 단계의 브랜치로 수시로 push하여 다른 사람들도 작업을 알 수 있도록 합니다.
                
                → 작업하던 부분이 없어지더라도 GitHub에서 소스코드를 받아 작업할 수 있습니다.
                
            
            3️⃣**Pull&Request(PR) 생성**
            
            - **Pull&Request를 사용해 자신의 코드를 공유하고 동료에게 리뷰를 받을 수 있습니다.**
            - merge할 준비가 되었다면 **master** branch로의 반영을 요구합니다.
            
            4️⃣**리뷰&토의**
            
            - PR을 master 브랜치에 병합할 때 배포 직전 토의와 리뷰가 필요합니다.
            
            5️⃣**테스트**
            
            - 작업 현황을 테스트 환경/서버에 배포해봅니다.
            - 문제가 발생했다면 **master** 브랜치의 내용을 다시 배포해 초기화시킵니다.
            
            6️⃣**최종 merge**
            
            - 문제가 없다면 **master** 브랜치에 push하고 즉시 배포합니다.
            - master로 merge가 된다면 자동으로 배포되도록 설정합니다.
            

### 2. Pull Request 생성법

1. 원본 저장소 fork 하기
2. fork한 저장소를 로컬에서 작업하기
    
    ```java
    // 1. fork한 원격 저장소의 소스코드를 로컬 컴퓨터에 복사
    git clone <fork한 저장소> 
    
    // 2. 저장소의 별명을 설정
    //동기화에 사용하기 위해 원본 저장소와 내 저장소 모두 remote로 등록
    git remote add <저장소별명 (ex.fork)> <원본저장소 URL>
    
    // 3. remote로 등록된 저장소 확인
    // origin => fork한 저장소
    // fork => 원본저장소
    git remote -v
    
    // 4. 새로운 브랜치 샏성
    git branch
    
    // 5. 새롭게 생성한 브랜치에서 작업한 후, add/commit/push
    ```
    
3. PR 생성하기
    
    ```java
    1. PUSH를 완료한 뒤 내 저장소에 새롭게 업데이트된 내용 확인
    2. 해당 내용에 문제가 없다면 우측 상단 [Compare&pull reqeust] 클릭
    3. 현재 별다른 충돌 없이 merge할 수 있음을 확인
    		커밋 메시지와 설명을 확인, 수정한 다음 [Create pull request ] 버튼을 클릭
    4. [Pull request] 택에서 내가 기여한 내용을 확인
    ```
    
4. PR Merge하기(원본저장소 소유자)
    
    ```java
    1. 저장소 상단 [Pull request] 탭을 클릭해 반영을 요구한 내용을 확인합니다. 
    2. 문제나 충돌이 없으면 [Confirm merge]-[Merge pull request]를 클릭해 PR을 병합합니다.
    		-> 필요할 경우 [Comment]를 클릭해 댓글을 남길 수 있습니다.
    3. 생성된 Pull request가 Merge되었음을 확인할 수 있습니다.
    ```
    
5. Merge이후 동기화, 브랜치 삭제
    
    ![Untitled](Git%20-%20%E1%84%92%E1%85%AA%E1%86%AF%E1%84%8B%E1%85%AD%E1%86%BC%20d862deb6c09341f391e5b2895d5cc63e/Untitled.png)
    
    ```java
    // 1. 로컬 저장소의 코드와 원본 저장소의 코드를 동기화
    git pull <원본 저장소 별명>
    //2. 더이상 사용하지 않는 브랜치를 삭제
    ```
    

## 다양한 GitHub 라이브러리

---

- GithubDesktop
- GitKraken
- GitLens

## GitHub 200% 활용하기

---

### 1. Github 블로그

![Untitled](Git%20-%20%E1%84%92%E1%85%AA%E1%86%AF%E1%84%8B%E1%85%AD%E1%86%BC%20d862deb6c09341f391e5b2895d5cc63e/Untitled%201.png)

[깃헙(GitHub) 블로그 10분안에 완성하기](https://youtu.be/ACzFIAOsfpM)

### 2. Github 프로필

[깃허브 계정 제대로 꾸미기 (깃허브 프로파일 페이지 → 이력서로 만들기 팁🔥)](https://www.youtube.com/watch?embeds_referring_euri=https://weeks52.me/&source_ve_path=Mjg2NjQsMTY0NTA2&feature=emb_share&v=w9DfC2BHGPA)

### 3. Readme 파일로 프로젝트 소개하기

- Markdown언어를 이용해 보기 좋게 정리할 수 있다.
    
    [마크다운(Markdown) 6분 순삭 정리 + 깃허브 리드미(ReadMe) 파일 작성 팁 ⭐️](https://www.youtube.com/watch?embeds_referring_euri=https://weeks52.me/&source_ve_path=Mjg2NjQsMTY0NTA2&feature=emb_share&v=kMEb_BzyUqk)
    
- 마크다운 사용법
    
    [마크다운(Markdown) 사용법](https://gist.github.com/ihoneymon/652be052a0727ad59601)
    
    1. 헤더
        - 큰 제목
            
            ```markdown
            This is an H1
            ==============
            ```
            
        - 작은 제목: 문서 부제목
            
            ```markdown
            This is an H2
            -------------
            ```
            
        - 글머리 : 1~6까지 지원
            
            ```markdown
            # This is a H1
            ## This is a H2
            ### This is a H3
            #### This is a H4
            ##### This is a H5
            ###### This is a H6
            ```
            
    2. BlockQuote
        
        ```markdown
        > This is a first blockqute.
        >	> This is a second blockqute.
        >	>	> This is a third blockqute.
        ```
        
        이 안에서 다른 마크다운 요소를 포함할 수 있다.
        
    3. 목록
        
        ```markdown
        1. 첫번째
        2. 두번째
        3. 세번째
        
        * 빨강
          * 녹색
            * 파랑
        
        + 빨강
          + 녹색
            + 파랑
        
        - 빨강
          - 녹색
            - 파랑
        ```
        
    4. 코드
        - 들여쓰기 : 4개의 공백 또는 하나의 탭. 한 줄 띄어쓰기해야 인식함
            
            ```markdown
            This is a normal paragraph:
            
                This is a code block.(코드블럭 적용)
                
            end code block.
            ```
            
        - 코드블럭
            
            ```markdown
            ```java
            public class BootSpringBootApplication {
              public static void main(String[] args) {
                System.out.println("Hello, Honeymon");
              }
            }
            ```
            ```
            
    5. 수평선
        
        ```markdown
        * * *
        
        ***
        
        *****
        
        - - -
        
        ---------------------------------------
        ```
        
    6. 링크
        - 참조링크
            
            ```markdown
            [link keyword][id]
            
            [id]: URL "Optional Title here"
            
            // code
            Link: [Google][googlelink]
            
            [googlelink]: https://google.com "Go google"
            ```
            
        - 외부링크
            
            ```markdown
            사용문법: [Title](link)
            적용예: [Google](https://google.com, "google link")
            ```
            
    7. 강조
        
        ```markdown
        *single asterisks*
        _single underscores_
        **double asterisks**
        __double underscores__
        ~~cancelline~~
        ```
        
    8. 이미지
        
        ```markdown
        ![Alt text](/path/to/img.jpg)
        ![Alt text](/path/to/img.jpg "Optional title")
        
        <img src="/path/to/img.jpg" width="450px" height="300px" title="px(픽셀) 크기 설정" alt="RubberDuck"></img><br/>
        <img src="/path/to/img.jpg" width="40%" height="30%" title="px(픽셀) 크기 설정" alt="RubberDuck"></img>
        ```
        
        사이즈 조절 기능은 없기 때문에 `<img width="" height=""></img>`를 이용
        
    9. 줄바꿈
        
        ```markdown
        * 줄 바꿈을 하기 위해서는 문장 마지막에서 3칸이상을 띄어쓰기해야 한다. 
        이렇게
        
        * 줄 바꿈을 하기 위해서는 문장 마지막에서 3칸이상을 띄어쓰기해야 한다.___\\ 띄어쓰기
        이렇게
        ```
