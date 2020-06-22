# CodeBot User Guide

> CodeBot 시스템은 개발자와 리뷰어간의 원활한 코드리뷰 수행을 지원하기 위해 다양한 자동화 기능을 제공하는 코드리뷰 지원 서비스입니다.

## 목차

* [개요](#개요)
* [준비 사항](#준비-사항)
* [CodeBot 설정](#codebot-설정)
  * [GitHub Personal access token 등록](#github-personal-access-token-등록)
  * [Repository 조회](#repository-조회)
  * [Repository 설정](#repository-설정)
* [CodeBot 분석 수행](#codebot-분석-수행)
* [CodeBot 분석 결과 확인](#codebot-분석-결과-확인)
  * [Repository Code Size](#repository-code-size)
  * [Issue(Inspection)](#issue(inspection))
  * [Complexity](#complexity)
  * [Duplication](#duplication)
  * [CAM(Code Architecture Metric)](#cam(code-architecture-metric))
  * [AutoFix Recommendations](#autofix-recommendations)

## 개요

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

---

## 준비 사항

### Codebot 사용 준비

CodeBot 사용을 위해서는 GitHub에 대한 접근 권한이 필요합니다. 이를 위해 GitHub에서 Personal Access Token을 생성한 후 CodeBot에 등록이 필요합니다.

### GitHub Personal access token 생성

#### 1. 오른쪽 상단의 프로필 사진을 클릭한 다음 Settings를 클릭합니다.

![](/images/github-access-token/github-access-token-01.png)

#### 2. 왼쪽 사이드 바에서 Developer settings를 클릭합니다.

![](/images/github-access-token/github-access-token-02.png)

#### 3. 왼쪽 사이드 바에서 Personal access tokens를 클릭합니다.

![](/images/github-access-token/github-access-token-03.png)

#### 4. 오른쪽의 Generate new token을 클릭합니다.

![](/images/github-access-token/github-access-token-04.png)

#### 5. Token의 이름을 입력합니다.

![](/images/github-access-token/github-access-token-05.png)

#### 6. Token에 부여하려는 권한을 선택합니다. CodeBot 사용을 위해서 다음의 권한이 필요합니다.

* repo (Full control of private repositories)
* admin:org (Full control of orgs and teams, read and write org projects)
* amdin:repo_hook (Full control of reporitory hooks)

![](/images/github-access-token/github-access-token-06.png)

#### 7. Generate token을 클릭합니다.

![](/images/github-access-token/github-access-token-07.png)

#### 8. :clipboard:버튼을 클릭하아여 클립보드에 복사합니다. 보안상의 이유로, 페이지를 떠나면 Token을 다시 볼 수 없습니다.

![](/images/github-access-token/github-access-token-08.png)

---

## CodeBot 설정

### GitHub Personal access token 등록

> 발급받은 Token을 CodeBot에 등록합니다.



### Repository 조회

> 등록한 Token으로 접근 가능한 Repository를 보여줍니다.



### Repository 설정

> CodeBot 서비스를 사용하기 위한 Repository 설정

첫 설정 시 CodeBot 사용 유무를 선택하는 스위치를 클릭해 OFF상태를 ON으로 변경합니다.

![](/images/codebot-settings/codebot-settings-off.png)

CodeBot 스위치가 ON으로 변경되면 세부 설정을 위한 메뉴가 보입니다.

![](/images/codebot-settings/codebot-settings-on.png)

* #### 기본설정

  CodeBot 분석 적용 대상에 대한 기본적인 설정 항목입니다.

  ![](/images/codebot-settings/codebot-settings-default.png)

  * 사용 중인 언어 선택 : 분석 대상인 Repository에서 사용 중인 프로그래밍 언어를 선택합니다.
  * 적용 브랜치 범위(Branch) **[필수 입력값]** : 분석을 적용할 브랜치를 입력합니다.
    > Comma[,]로 구분하여 여러 브랜치 패턴을 입력할 수 있습니다.
  * 리뷰어 자동 지정 : 활성화 시 분석한 Pull request의 리뷰어를 자동으로 지정합니다.

* #### 잠재결함 분석

  잠재결함 분석 시 사용되는 추가 설정 항목입니다.

  > Java 언어 한정

  ![](/images/codebot-settings/codebot-settings-inspection.png)

  * Inspection 자동 수정 기능 : 활성화 시 분석된 잠재결함 결과 중 예상되는 조치 방안이 존재할 경우 코드 자동 수정을 제안하는 AutoFix 기능이 수행됩니다.

* #### Analysis Scope

  분석 대상이 되는 소스 코드의 범위를 지정할 수 있습니다.

  ![](/images/codebot-settings/codebot-settings-analysis-scope.png)

  > Comma[,]로 구분하여 여러 패턴을 입력할 수 있습니다.

  > Wildcard(*, **, ?)를 이용한 패턴을 사용할 수 있습니다.

  * Source File Exclusions : 분석 대상에서 제외할 소스 경로를 입력합니다.
  * Source File Inclusions : 분석 대상에 포함할 소스 경로를 입력합니다.

* #### Build Options

  분석을 위해 사전 수행되는 Build에 대한 설정입니다.

  > Java 언어 한정

  ![](/images/codebot-settings/codebot-settings-build-options.png)

  * Build Tool : 사용할 Build 툴을 선택합니다.
    > Command 선택 시 Build 명령어를 직접 입력할 수 있습니다.
    ![](/images/codebot-settings/codebot-settings-build-command.png)
  * Source Path **[필수 입력값]** : Build 시 적용할 소스 코드의 경로를 입력합니다.
  * Binary Path **[필수 입력값]** : Build 시 적용할 바이너리 코드의 경로를 입력합니다.

입력을 마친 후 우측 하단의 Apply 버튼을 클릭하면 설정이 저장됩니다.

![](/images/codebot-settings/codebot-settings-apply.png)

![](/images/codebot-settings/codebot-settings-saved.png)

### GitHub 설정 확인

CodeBot 서비스 사용위한 설정을 마치면 GitHub의 해당 Repository에 Webhook이 설정됩니다.

> GitHub > Repository > Settings > Webhooks에서 Payload URL을 확인

> CodeBot 서비서 ON 시 추가되고, OFF 시 삭제됩니다.

![](/images/github-settings/github-webhooks.png)

---

## CodeBot 분석 수행

---

## CodeBot 분석 결과 확인

> CodeBot Dashboard의 Repository 리스트를 클릭하면 최근 Pull Request의 분석 결과를 볼 수 있습니다.

![](/images/codebot-result/codebot-result-all.jpg)

### Repository Code Size

Repository의 코드 정보
> 분석 대상이 되는 Repository 내의 코드에 대한 정량적 수치입니다.

![](/images/codebot-result/codebot-result-codesize.png)

* Lines of Code : 공백, 주석을 제외한 코드 라인 수
* Files : 파일 수
* Funtions : Function 수 (Java의 경우 Anonymous Class의 Method는 제외)
* Lines : 공백, 주석을 포함한 코드 라인 수
* Directories : 디렉토리 수
* Classes : 클래스 수 (Nested Class, Interface, Enums, Annotations 포함)

### Issue(Inspection)

잠재결함 정보
> 정적 분석을 통해 나타나는 코드의 문제점으로, 결함 발생 위험, 보안 취약, 유지보수 저해 등과 관련된 Rule에 따라 코드를 탐지하고 알려줍니다.

![](/images/codebot-result/codebot-result-issue.png)

* Total : 전체 Codeing Rule 위반 건수
* Bugs : 런타임 시 문제가 될 잠재적인 결함과 관련된 Rule 위반 건수
* Vulnerabilities : 보안취약점과 관련된 Rule 위반 건수
* Code Smells : 유지보수성과 관련된 Rule 위반 건수

### Complexity

복잡도 정보

> 코드를 통과하는 경로 수를 기반으로 계산된 Cyclomatic Complexity입니다. 복잡도가 높을수록 코드 수정 시 오류 발생 확률이 높아지고, 테스트를 위한 유지보수 비용이 증가합니다.

> Java의 경우 복잡도 증가 Keyword는 if, for, while, case, catch, throw, &&, ||, ?

![](/images/codebot-result/codebot-result-complexity.png)

* Total : 전체 복잡도 수
* Equal or Over 50 : 복잡도가 50 이상인 Function의 수
* Over 20 : 복잡도가 20 초과인 Function의 수

### Duplication

중복도 정보

> 동일한 코드가 반복되는 것을 탐지하여 알려줍니다. 중복된 코드는 코드량과 유지보수 비용을 증가시키며 오류 발생 확률을 높이므로 리팩토링을 통한 개선이 필요합니다.

![](/images/codebot-result/codebot-result-duplication.png)

* Total : 전체 중복률
* Duplicated Lines : 중복 라인 수
* Duplicated Blocks : 중복된 라인 블록 수 (Java의 경우 10개 이상 연속적으로 중복된 Statement)

### CAM(Code Architecture Metric)

코드 구조 분석 정보

> 코드의 구조와 관련된 수치를 측정하여 알려줍니다. 측정된 수치를 기반으로 척도와 코드의 구조적 리팩토링을 위한 가이드를 제공합니다.

![](/images/codebot-result/codebot-result-cam.png)

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

![](/images/codebot-result/codebot-result-autofix.png)

* Count : 잠재결함 분석 결과를 토대로 제안된 자동 수정 건수

## CodeBot 서비스 관련 문의

> code_bot@samsung.com