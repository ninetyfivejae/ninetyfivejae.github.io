GitCollaboratingWorkflows
=========================

Comparing workflows / 협업 플로우 비교 정리
-------------------------------------------

-	Git collaborating workflows README

---

1.1. Centralized Workflow
-------------------------

-	Lionel Messi's work added

-	Cristiano Ronaldo's work added

Centralized Workflow는 프로젝트의 변경 내용을 추적하기 위해 단일 중앙 저장소를 이용한다. Subversion의 trunk 대신, master란 브랜치를 사용하고, 모든 변경 내용은 이 브랜치에 커밋(commit)한다. 이 워크플로우에서는 master 브랜치 하나만 사용한다. 팀 구성원은 중앙 저장소를 복제하여 로컬 저장소를 만든 후, 로컬 저장소에서 파일을 수정하고 변경 내용을 커밋한다(SVN과 달리 변경 내용은 로컬 저장소에 기록된다). 로컬 저장소는 원하는 때 언제든 중앙 저장소와 동기화할 수 있다. 로컬 master 브랜치의 변경 내용을 프로젝트의 중앙 저장소에 올리고자할 때는 ‘push’ 명령을 이용한다. svn commit과 비슷하지만, 로컬 저장소의 커밋 이력을 중앙 저장소에 그대로 보관한다는 점은 다르다.

![GitRebase1](http://cfile2.uf.tistory.com/image/9973A7335A20FF6F34D420)

![GitRebase2](http://cfile7.uf.tistory.com/image/99E547335A20FFC2153807)

![GitRebaseSourceTree1](http://cfile3.uf.tistory.com/image/992C5D335A20E0AD1E1DED)

![GitRebaseSourceTree2](http://cfile23.uf.tistory.com/image/998763335A20E97336460B)

---

1.2. Feature Branch Workflow
----------------------------

-	Ronaldo passes the ball

-	Messi shoots for the goal

Feature Branch Workflow의 핵심 컨셉은 기능별 브랜치를 만들어서 작업한다는 사실이다. 기능 개발 브랜치는 격리된 작업 환경을 제공하기 때문에 다수의 팀 구성원이 master를 중심으로 해서 안전하게 새로운 기능을 개발할 수 있다. 따라서 master 브랜치는 항상 버그 프리 상태로 유지할 수 있어, 지속적 통합(Continuout Integration)을 적용하기도 수월하다. 또, 풀 리퀘스트를 적용하기도 쉽다.

이 워크플로우도 프로젝트의 공식적인 변경 이력을 기록하기 위해서 중앙 저장소와 master 브랜치를 사용한다. 그런데, master 브랜치에 직접 커밋하지는 않고, 새로운 기능을 개발할 때마다 브랜치를 만들어서 작업한다. 보통 animated-menu-items 또는 issue-#1061처럼 의미를 담고 있는 브랜치 이름을 사용한다.

새로 만든 기능 개발용 브랜치도 중앙 저장소에 올려서 팀 구성원들과 개발 내용에 대한 의견(코드 리뷰 등)을 나눌 수 있다. master 브랜치를 손대지 않기 때문에 다른 기능 개발 브랜치를 얼마든지 올려도 된다. 이는 일종의 로컬 저장소 백업 역할을 하기도 한다.

![FeatureBranchWorkflowSourceTree](http://cfile25.uf.tistory.com/image/99D045335A215FEA1FC8A3)

---

1.3. Gitflow Workflow
---------------------

-	Example with arithmetic operation

Gitflow Workflow는 nvie.com의 빈센트 드리센(Vincent Driessen)이 제안한 것이다. Gitflow Workflow는 코드 릴리스를 중심으로 좀 더 엄격한 브랜칭 모델을 제시한다. Feature Branch Workflow보다 복잡하긴하지만, 대형 프로젝트에도 적용할 수 있는 강건한 작업 절차다.

#### 1.3.1. 작동원리

Gitflow Workflow도 팀 구성원간의 협업을 위한 창구로 중앙 저장소를 사용한다. 또 다른 워크플로우와 마찬가지로 로컬 브랜치에서 작업하고 중앙 저장소에 푸시한다. 단지 브랜치의 구조만 다를 뿐이다.

#### 1.3.2. 이력을 기록하는 브랜치

master 브랜치 뿐만아니라, 이 워크플로우에서는 두 개의 다른 브랜치도 변경 이력을 유지하기 위해 사용한다. master 브랜치는 릴리스 이력을 관리하기 위해 사용하고, develop 브랜치는 기능 개발을 위한 브랜치들을 병합하기 위해 사용한다. 그래서, master 브랜치는 릴리스 태그를 매기기에 아주 적합하다. 이 워크플로우의 모든 작업 절차들은 master 와 develop 두 개의 브랜치를 대상으로 한다.

#### 1.3.3. 기능 브랜치

새로운 기능은 각각의 브랜치에서 개발하고 백업 및 협업을 위해서 중앙 저장소에 푸시한다. 그런데, master 브랜치에서 기능 개발을 위한 브랜치를 따는 것이 아니라, develop 브랜치에서 딴다. 그리고, 기능 개발이 끝나면 다시 develop 브랜치에 작업 내용을 병합한다. 바꾸어 말하면, 기능 개발을 위한 브랜치는 master 브랜치와는 어떤 상호 작용도 하지 않는다. Feature Branch Workflow라면 develop 브랜치에 개발한 기능을 병합하는 것으로 모든 과정이 끝날테지만, Gitflow Workflow는 아직 할 일이 더 남아 있다.

![DevelopBranch](http://cfile22.uf.tistory.com/image/99D183335A21BB1D2CBE6E)

#### 1.3.4. 릴리즈 브랜치

develop 브랜치에 릴리스를 할 수 있는 수준만큼 기능이 모이면(또는 정해진 릴리스 일정이 되면), develop 브랜치를 기준으로 릴리스를 위한 브랜치를 딴다. 이 브랜치를 만드는 순간부터 릴리스 사이클이 시작되고, 버그 수정, 문서 추가 등 릴리스와 직접적으로 관련된 작업들을 제외하고는 이 브랜치에 새로운 기능을 추가 병합하지 않는다. 릴리스 준비가 완료되면 master 브랜치에 병합하고 버전 태그를 부여한다. 그리고, 릴리스를 준비하는 동안 develop 브랜치가 변경되었을 수 있으므로 develop 브랜치에도 병합한다. 릴리스를 위한 전용 브랜치를 사용함으로써 한 팀이 릴리스를 준비하는 동안 다른 팀은 다음 릴리스를 위한 기능 개발을 계속할 수 있다. 즉, 딱딱 끊어지는 개발 단계를 정의하기에 아주 좋다. 예를 들어, 이번 주에 버전 4.0 릴리스를 목표로한다라고 팀 구성원들과 쉽게 소통하고 합의할 수 있다는 말이다. 릴리스 브랜치는 release-* 또는 release/* 처럼 이름 짓는 것이 일반적인 관례다.

![ReleaseBranch](http://cfile2.uf.tistory.com/image/99D2A7335A21BB332F7CE0)

#### 1.3.5. 유지 보수를 위한 브랜치

운영 환경에 릴리스한 후 발견된 긴급 패치는 ‘hotfix’ 브랜치를 이용한다. ‘hotfix’ 브랜치만 master 에서 바로 딸 수 있다. 패치가 준비되면 master 와 develop 브랜치 양쪽에 병합하고, 새로운 버전 이름으로 태그를 매겨야 한다. 버그 수정만을 위한 브랜치를 따로 만들었기때문에, 다음 릴리스를 위해 개발하던 작업 내용에 전혀 영향을 주지 않는다. ‘hotfix’ 브랜치는 master 브랜치를 부모로 하는 임시 브랜치라고 생각하면 된다.

![HotfixBranch](http://cfile6.uf.tistory.com/image/99D399335A21BB392E2BCC)

-	실제 공모전 프로젝트 준비하면서 사용한 Gitflow Workflow 브랜치 그래프

![GitflowExample](http://cfile23.uf.tistory.com/image/99C1D1335A21BB3A3134FD)

---

- [Posted on the blog specifically](http://otakijae.tistory.com/category/Git)