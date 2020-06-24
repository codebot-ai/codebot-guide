# CodeBot Service

> CodeBot 시스템은 개발자와 리뷰어간의 원활한 코드리뷰 수행을 지원하기 위해 다양한 자동화 기능을 제공하는 코드리뷰 지원 서비스입니다.

## [How to use CodeBot (User Guide)](https://github.com/codebot-ai/codebot-guide/wiki)

CodeBot은 GitHub으로부터 PR(Pull Request) 이벤트가 발생하면, 변경된 소스를 기준으로 다양한 정적 분석(Static Analyst)을 수행하고, 리뷰어를 자동 지정하는 등의 코드리뷰 활동에 필요한 다양한 서비스를 제공합니다.

제공되는 서비스는 다음과 같습니다.

* 잠재결함 분석
  * 잠재결함 자동 수정(Autofix) 기능
* CAM(Code Archtecture Metric) 분석
* Build 테스트 결과
* Unit 테스트 결과
* 리뷰어 자동 지정
* 오탈자 분석 기능

지원되는 언어는 다음과 같습니다.

* Java (Maven / Gradle / Ant)
* JavaScript
* Python

![](/images/codebot-use-case-01.jpg)
![](/images/codebot-use-case-02.jpg)
![](/images/codebot-use-case-03.jpg)

---

## GitHub Personal access token 생성

#### 1. 오른쪽 상단의 프로필 사진을 클릭한 다음 Settings를 클릭합니다.

<img src="images/github-access-token/github-access-token-01.png" width="20%" style="box-shadow: 5px 5px 10px grey" />

#### 2. 왼쪽 사이드 바에서 Developer settings를 클릭합니다.

<img src="images/github-access-token/github-access-token-02.png" width="20%" style="box-shadow: 5px 5px 10px grey" />

#### 3. 왼쪽 사이드 바에서 Personal access tokens를 클릭합니다.

<img src="images/github-access-token/github-access-token-03.png" width="20%" style="box-shadow: 5px 5px 10px grey" />

#### 4. 오른쪽의 Generate new token을 클릭합니다.

<img src="images/github-access-token/github-access-token-04.png" width="50%" style="box-shadow: 5px 5px 10px grey" />

#### 5. Token의 이름을 입력합니다.

<img src="images/github-access-token/github-access-token-05.png" width="40%" style="box-shadow: 5px 5px 10px grey" />

#### 6. Token에 부여하려는 권한을 선택합니다. CodeBot 사용을 위해서 다음의 권한이 필요합니다.

* repo (Full control of private repositories)
* admin:org (Full control of orgs and teams, read and write org projects)
* amdin:repo_hook (Full control of reporitory hooks)

<img src="images/github-access-token/github-access-token-06.png" width="50%" style="box-shadow: 5px 5px 10px grey" />

#### 7. Generate token을 클릭합니다.

<img src="images/github-access-token/github-access-token-07.png" width="20%" style="box-shadow: 5px 5px 10px grey" />

#### 8. :clipboard:버튼을 클릭하아여 클립보드에 복사합니다.   보안상의 이유로, 페이지를 떠나면 Token을 다시 볼 수 없습니다.

<img src="images/github-access-token/github-access-token-08.png" width="50%" style="box-shadow: 5px 5px 10px grey" />

---

## CodeBot 분석 결과 확인

> CodeBot Dashboard의 Repository 리스트를 클릭하면 최근 Pull Request의 분석 결과를 볼 수 있습니다.

<img src="images/codebot-result/codebot-result-all.jpg" width="70%" style="box-shadow: 5px 5px 10px grey" />

### Repository Code Size

Repository의 코드 정보
> 분석 대상이 되는 Repository 내의 코드에 대한 정량적 수치입니다.

<img src="images/codebot-result/codebot-result-codesize.png" width="40%" style="box-shadow: 5px 5px 10px grey" />

* Lines of Code : 공백, 주석을 제외한 코드 라인 수
* Files : 파일 수
* Funtions : Function 수 (Java의 경우 Anonymous Class의 Method는 제외)
* Lines : 공백, 주석을 포함한 코드 라인 수
* Directories : 디렉토리 수
* Classes : 클래스 수 (Nested Class, Interface, Enums, Annotations 포함)

### Issue(Inspection)

잠재결함 정보
> 정적 분석을 통해 나타나는 코드의 문제점으로, 결함 발생 위험, 보안 취약, 유지보수 저해 등과 관련된 Rule에 따라 코드를 탐지하고 알려줍니다.

<img src="images/codebot-result/codebot-result-issue.png" width="40%" style="box-shadow: 5px 5px 10px grey" />

* Total : 전체 Codeing Rule 위반 건수
* Bugs : 런타임 시 문제가 될 잠재적인 결함과 관련된 Rule 위반 건수
* Vulnerabilities : 보안취약점과 관련된 Rule 위반 건수
* Code Smells : 유지보수성과 관련된 Rule 위반 건수

### Complexity

복잡도 정보

> 코드를 통과하는 경로 수를 기반으로 계산된 Cyclomatic Complexity입니다.   복잡도가 높을수록 코드 수정 시 오류 발생 확률이 높아지고, 테스트를 위한 유지보수 비용이 증가합니다.

> Java의 경우 복잡도 증가 Keyword는 if, for, while, case, catch, throw, &&, ||, ?

<img src="images/codebot-result/codebot-result-complexity.png" width="40%" style="box-shadow: 5px 5px 10px grey" />

* Total : 전체 복잡도 수
* Equal or Over 50 : 복잡도가 50 이상인 Function의 수
* Over 20 : 복잡도가 20 초과인 Function의 수

### Duplication

중복도 정보

> 동일한 코드가 반복되는 것을 탐지하여 알려줍니다.   중복된 코드는 코드량과 유지보수 비용을 증가시키며 오류 발생 확률을 높이므로 리팩토링을 통한 개선이 필요합니다.

<img src="images/codebot-result/codebot-result-duplication.png" width="40%" style="box-shadow: 5px 5px 10px grey" />

* Total : 전체 중복률
* Duplicated Lines : 중복 라인 수
* Duplicated Blocks : 중복된 라인 블록 수 (Java의 경우 10개 이상 연속적으로 중복된 Statement)

### CAM(Code Architecture Metric)

코드 구조 분석 정보

> 코드의 구조와 관련된 수치를 측정하여 알려줍니다.   측정된 수치를 기반으로 척도와 코드의 구조적 리팩토링을 위한 가이드를 제공합니다.

<img src="images/codebot-result/codebot-result-cam.png" width="80%" style="box-shadow: 5px 5px 10px grey" />

* Cyclomatic Complexity - CC : 코드의 복잡성을 나타내는 수치로 Function 단위로 측정 (PMD의 Modified Cyclomatic Complexity Rule을 사용)
* Duplication Code - DC : 두 번 이상 반복되는 코드를 파일 단위로 측정 (SonarQube의 중복도 측정 방식을 사용)
* Coupling Between Objects - CBO : 다른 객체와 결합되어 있는 객체를 클래스 단위로 측정 (ckjm 측정 방식을 사용)
* Lines Of Code - LOC : 코드의 라인 수를 측정하여 권장 라인 수(500)를 기준으로 계산 (NCLOC - Non-Comment Lines Of Code를 사용)
* Normalized Distance From Main Sequence - ND : 패키지 단위의 추상화와 안정성 균형을 측정 (JDepend 측정 방식을 사용)
* Cohesion Of Class - COC : 클래스 단위의 응집도를 측정 (CBAMU 방식을 사용)

### AutoFix Recommendations

잠재결함 자동 수정 제안

> 검출된 잠재결함 중 예상되는 조치 방안이 존재할 경우 코드 자동 수정을 제안합니다.

> Java 언어 한정

<img src="images/codebot-result/codebot-result-autofix.png" width="40%" style="box-shadow: 5px 5px 10px grey" />

* Count : 잠재결함 분석 결과를 토대로 제안된 자동 수정 건수

---

## CodeBot 서비스 문의

> code_bot@samsung.com