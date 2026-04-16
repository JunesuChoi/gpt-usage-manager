# GPT Usage Manager

<p align="center">
  <strong>여러 ChatGPT / Codex 계정의 사용량을 하나의 운영 대시보드처럼 관리하는 Windows 앱</strong>
</p>

<p align="center">
  <img alt="Windows" src="https://img.shields.io/badge/Windows-Only-0078D4?style=for-the-badge&logo=windows&logoColor=white">
  <img alt="Tauri" src="https://img.shields.io/badge/Tauri-Desktop-111111?style=for-the-badge&logo=tauri&logoColor=FFC131">
  <img alt="Release Flow" src="https://img.shields.io/badge/Install-GitHub%20Releases-24292F?style=for-the-badge&logo=github&logoColor=white">
  <img alt="License" src="https://img.shields.io/badge/License-MIT-4C1D95?style=for-the-badge">
</p>

<p align="center">
  같은 PC에서 <code>개인</code>, <code>비즈니스</code>, <code>Codex 데스크톱</code> 계정을 함께 쓰는 사용자를 위한 멀티 계정 사용량 모니터링 도구입니다.
</p>

---

## ✦ 빠른 소개

이 앱은 여러 ChatGPT / Codex 계정을 동시에 운용할 때 필요한 정보를 한 화면에 모아 보여줍니다.

- `현재 한도`와 `주간 한도`를 동시에 확인
- 리셋 카운트다운과 리셋 캘린더 제공
- 현재 사용 중인 Codex 계정 감지
- 한도 임박 트레이 알림
- Windows 기준 Codex 프로필 저장 / 전환

> [!IMPORTANT]
> 이 공개 저장소의 `main` 브랜치는 문서 안내용입니다.
> 실제 앱 사용은 **GitHub Releases 설치 파일** 기준으로 진행하세요.

## ✦ 설치

일반 사용자는 소스 코드가 아니라 GitHub Releases의 설치 파일을 사용합니다.

- `GPT Usage Manager_..._x64_en-US.msi`
- `GPT Usage Manager_..._x64-setup.exe`

Releases:
- https://github.com/JunesuChoi/gpt-usage-manager/releases

---

## ✦ 앱 사용설명서

### 1. 처음 실행할 때

앱을 처음 열면 상단에 `계정 추가`, `설정`, `미니모드` 버튼이 보입니다.  
기본 흐름은 `계정 추가 -> 로그인 -> 사용량 확인 -> 필요 시 Codex 저장/전환` 순서입니다.

### 2. 계정 추가

1. 상단 `계정 추가`를 누릅니다.
2. `별칭`, `이메일`, `계정 유형(개인/비즈니스)`, `플랜`을 입력합니다.
3. 저장하면 계정 카드가 생성됩니다.

> [!NOTE]
> 별칭은 화면 표시용 이름입니다. 별칭만 바꿔도 기존 로그인 세션이나 Codex 프로필 연결은 유지됩니다.

### 3. 로그인과 첫 사용량 동기화

신규 계정은 먼저 로그인 세션을 만들어야 합니다.

1. 생성된 계정 카드에서 `로그인`을 누릅니다.
2. 브라우저가 열리면 해당 계정으로 로그인합니다.
3. 로그인 후 앱으로 돌아오면 사용량이 자동 또는 수동으로 갱신됩니다.

앱은 시작 시 한 번, 이후 5분 간격으로 사용량을 다시 수집합니다.

### 4. 메인 화면 읽는 법

Overview에서는 다음 정보를 봅니다.

- 현재 사용 중인 계정
- 전체 등록 계정 수
- 사용량 확인 완료 계정 수
- 로그인 필요 계정 수
- Codex 프로필 저장 계정 수
- 현재 알림 기준
- Codex 작업 통계

오른쪽 미니카드 영역에서는 다음 우선순위로 빠르게 확인할 수 있습니다.

- 현재 사용 중 계정
- 최근 오류가 있는 계정
- 다음 전환 후보 계정
- Codex 토큰 통계 요약

### 5. 계정 카드에서 자주 쓰는 작업

각 계정 카드에는 두 종류의 작업이 있습니다.

- 주요 작업: `갱신`, `로그인`
- 보조 작업: `Codex 저장`, `Codex 전환`, `편집`, `삭제`

### 6. Codex 프로필 저장 / 전환

Codex 앱을 여러 계정으로 번갈아 쓰는 경우 아래 흐름을 사용합니다.

1. Codex 앱에서 원하는 계정으로 직접 로그인합니다.
2. GPT Usage Manager의 해당 카드에서 `Codex 저장`을 누릅니다.
3. 이후 다른 계정 카드에서 `Codex 전환`을 누르면 저장된 프로필로 전환됩니다.

> [!IMPORTANT]
> `Codex 저장`은 현재 PC에서 로그인된 Codex 상태를 해당 계정에 스냅샷하는 동작입니다.
> 계정마다 처음 한 번은 직접 로그인 후 저장해야 합니다.

### 7. 다음 계정 전환

Overview에는 `다음 계정 전환` 버튼이 있습니다.  
이 버튼은 아래 조건을 만족하는 계정 중에서 가장 여유가 큰 계정을 자동으로 골라 전환합니다.

- 현재 사용 중이 아님
- Codex 프로필이 저장되어 있음
- 로그인 상태가 유효함
- 사용량이 확인되어 있음
- 최근 오류가 없음

### 8. 미니모드

상단 `미니모드` 버튼 또는 현재 사용 중 계정 카드의 `미니모드 보기`를 누르면 오버레이 모드로 전환됩니다.

- 현재 사용 중 계정의 현재 한도와 주간 한도만 간단히 표시
- 항상 위에 표시
- 버튼이 아닌 카드 영역을 드래그해서 위치 이동 가능
- `펼치기`로 원래 창으로 복귀

### 9. 리셋 캘린더와 알림

- `리셋 캘린더` 탭에서 계정별 주간 리셋 일정 확인
- 설정에서 현재 사용 중 계정의 한도 경고 기준 조정
- 대기 계정의 리셋 임박 알림 기준 조정

### 10. 자주 발생하는 문제

#### 계정이 비어 보임

- 앱을 다시 시작해 초기 로드를 다시 시도합니다.
- `%APPDATA%\\com.gpt-usage-manager.app\\accounts.json`이 존재하는지 확인합니다.

#### 사용량 갱신 실패

- 계정 카드의 최근 오류 문구를 확인합니다.
- 로그인 세션이 풀렸다면 `로그인`을 다시 수행합니다.
- 브라우저 세션이 꼬인 경우, 해당 계정으로 재로그인 후 다시 갱신합니다.

#### Codex 전환이 안 됨

- 먼저 해당 계정에서 `Codex 저장`이 한 번이라도 되었는지 확인합니다.
- Codex 앱이 설치된 PC인지 확인합니다.

---

## ✦ 실행 환경

### 필수

- Windows
- Microsoft Edge 또는 Google Chrome

### 선택

- Codex 데스크톱 앱

---

## ✦ 동작 방식

이 앱은 공식 Billing API를 사용하지 않습니다.  
사용자가 이미 로그인한 로컬 세션을 바탕으로 사용량과 결제일 관련 정보를 가져오고, Codex 전환은 로컬 프로필 및 인증 상태를 저장/복원하는 방식으로 동작합니다.

---

## ✦ 민감한 로컬 데이터

> [!CAUTION]
> 아래 데이터는 공개 저장소에 업로드하면 안 됩니다.

- `%APPDATA%\\com.gpt-usage-manager.app\\accounts.json`
- `%APPDATA%\\com.gpt-usage-manager.app\\settings.json`
- `%APPDATA%\\com.gpt-usage-manager.app\\browser_data\\`
- `%APPDATA%\\com.gpt-usage-manager.app\\codex_profiles\\`
- `%USERPROFILE%\\.codex\\auth.json`

---

## ✦ 라이선스

MIT
