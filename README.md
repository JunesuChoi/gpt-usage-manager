# GPT Usage Manager

<p align="center">
  <strong>여러 ChatGPT · Codex 계정의 한도와 세션을 한 화면에서 관리하는 Windows 앱</strong>
</p>

<p align="center">
  <a href="https://github.com/JunesuChoi/gpt-usage-manager/releases/latest"><img alt="최신 릴리즈" src="https://img.shields.io/github/v/release/JunesuChoi/gpt-usage-manager?display_name=tag&sort=semver&style=flat-square&color=111111"></a>
  <img alt="Windows" src="https://img.shields.io/badge/Windows-10%2F11-0078D4?style=flat-square&logo=windows&logoColor=white">
  <img alt="Tauri" src="https://img.shields.io/badge/Tauri-2-FFC131?style=flat-square&logo=tauri&logoColor=111111">
  <img alt="MIT" src="https://img.shields.io/badge/License-MIT-111111?style=flat-square">
</p>

<p align="center">
  <a href="https://github.com/JunesuChoi/gpt-usage-manager/releases/latest">최신 설치 파일 받기</a>
  ·
  <a href="https://github.com/JunesuChoi/gpt-usage-manager/issues">이슈 제보</a>
</p>

---

## 한눈에 보기

GPT Usage Manager는 개인 계정과 비즈니스 계정을 함께 사용하는 Windows 사용자를 위한 로컬 관리 도구입니다. 계정별 한도, 리셋 시점, 로그인 상태, Codex 프로필을 한 곳에서 확인하고 필요한 계정으로 빠르게 전환할 수 있습니다.

| 확인할 것 | 앱에서 제공하는 것 |
| --- | --- |
| 사용량 | 현재 한도와 주간 한도, 리셋 카운트다운 |
| 계정 상태 | 현재 사용 중, 로그인 필요, 갱신 실패, 첫 동기화 필요 |
| Codex | 현재 활성 계정 감지, 프로필 저장·전환, 실시간 토큰 표시 |
| 운영 | 5분 주기 대기 계정 갱신, 한도·리셋 임박 트레이 알림 |
| 작업표시줄 | 작업표시줄 내부 계정명, 잔여량, 토큰, 갱신 시각 표시 |

## 빠른 설치

일반 사용자는 소스를 실행하지 말고 GitHub Releases의 설치 파일을 사용하세요.

1. [최신 릴리즈 페이지](https://github.com/JunesuChoi/gpt-usage-manager/releases/latest)를 엽니다.
2. `GPT.Usage.Manager_*_x64-setup.exe` 또는 `GPT.Usage.Manager_*_x64_en-US.msi`를 다운로드합니다.
3. 설치 후 앱을 실행합니다.

설치 파일은 `scrape-usage.mjs`, Codex 프로필 도우미, `playwright-core`를 포함한 자체 런타임 리소스를 사용합니다. 설치 위치를 사용자가 바꿔도 설치본 내부의 상대 경로를 기준으로 동작합니다.

## 기본 사용 흐름

### 1. 계정 추가

- 상단 `계정 추가`에서 수동으로 별칭, 이메일, 계정 유형, 플랜을 입력합니다.
- 또는 Codex 앱에 로그인한 뒤 `현재 Codex 계정 가져오기`를 사용합니다.
- 동일 이메일의 개인·비즈니스 계정은 조직 정보와 Codex 식별자를 함께 비교해 별도 슬롯으로 관리합니다.

### 2. 로그인과 사용량 확인

1. 계정 카드에서 `로그인`을 선택합니다.
2. 브라우저에서 해당 계정으로 로그인합니다.
3. 앱으로 돌아오면 `갱신` 또는 `전체 갱신`으로 사용량을 확인합니다.

대기 계정은 기본적으로 5분 간격으로 갱신됩니다. 현재 사용 중인 Codex 계정은 Codex app-server 이벤트를 우선 사용하고, 필요한 경우 기존 세션 기반 경로로 보완합니다.

### 3. Codex 프로필 저장과 전환

1. Codex 앱에서 원하는 계정과 조직으로 진입합니다.
2. 해당 계정 카드에서 `Codex 저장`을 한 번 실행합니다.
3. 다음부터는 `Codex 전환`으로 저장된 프로필을 복원합니다.

프로필 전환은 Windows의 Codex 데스크톱 환경을 전제로 합니다. 전환 후 프로젝트와 스레드가 누락되지 않도록 기존 Codex 상태를 보존하고, 로그인·조직이 확인되지 않으면 자동으로 다른 계정에 덮어쓰지 않습니다.

## 작업표시줄과 토큰 표시

작업표시줄 상태 표시는 WebView 오버레이가 아니라 Windows 작업표시줄 내부에 연결된 Rust 네이티브 창입니다. 설정에서 다음 항목을 즉시 조절할 수 있습니다.

- 위치: 왼쪽, 가운데, 오른쪽
- 미세 조정: 가로 `-500~500px`, 세로 `-100~100px`
- 표시 폭: `140~420px`
- 글꼴: Segoe UI, 맑은 고딕, Consolas
- 글꼴 크기: `8~20px`
- 표시 요소: 계정명, 유형·플랜, 주간 잔여량, 갱신 시각, 실시간 토큰 사용량

슬라이더와 표시 항목은 저장 버튼을 누르지 않아도 즉시 저장·반영됩니다. 실시간 토큰은 Codex app-server의 `thread/tokenUsage/updated` 이벤트를 사용하며, 이벤트가 없을 때는 마지막 로컬 스냅샷을 표시합니다.

## 화면 읽는 법

### Overview

- 현재 사용 중인 계정
- 사용량 확인 완료 계정 수
- 로그인 필요·오류 계정 수
- Codex 프로필 저장 계정 수
- 빠른 전환 후보
- 최근 Codex 토큰 통계

### 계정 카드

카드 상단에서 별칭, 계정 유형, 현재 상태, 현재·주간 잔여량을 확인할 수 있습니다. 상세 영역에서는 결제일, Codex 프로필, 최근 갱신 시각, 최근 오류와 저장·전환·편집 작업을 확인합니다.

### 미니모드

`미니모드`는 현재 사용 중 계정의 한도만 보여주는 항상 위 오버레이입니다. 카드 영역을 드래그해 이동할 수 있고, `펼치기`로 전체 화면으로 돌아갑니다.

### 리셋 캘린더

`리셋 캘린더`에서는 계정별 주간 리셋 날짜·시각과 남은 주간 한도를 함께 확인합니다.

## 알림

설정에서 다음 기준을 조절할 수 있습니다.

- 현재 사용 중 계정: 남은 한도 비율이 기준 이하일 때 알림
- 대기 계정: 주간 리셋이 지정한 시간 안으로 들어오면 알림

작업표시줄 상태 표시와 트레이 tooltip은 같은 활성 계정 스냅샷을 사용합니다.

## 데이터와 보안 경계

이 앱은 공식 Billing API가 아니라 사용자가 로그인한 로컬 세션과 Codex 상태를 사용합니다. 따라서 세션·프로필 데이터는 외부 서버로 업로드하지 않고 사용자 PC에 보관합니다.

다음 파일은 인증·세션 정보가 포함될 수 있으므로 절대 공유하거나 저장소에 올리면 안 됩니다.

```text
%APPDATA%\com.gpt-usage-manager.app\accounts.json
%APPDATA%\com.gpt-usage-manager.app\settings.json
%APPDATA%\com.gpt-usage-manager.app\browser_data\
%APPDATA%\com.gpt-usage-manager.app\codex_profiles\
%USERPROFILE%\.codex\auth.json
```

## 실행 환경

### 설치본 사용자

- Windows 10/11 x64
- Microsoft Edge 또는 Google Chrome
- Codex 프로필 저장·전환을 사용할 경우 Codex 데스크톱 앱

### 개발자

- Windows
- Node.js
- Rust toolchain
- Microsoft Edge 또는 Google Chrome

개발 실행과 배포 빌드는 공개 저장소의 실행 소스가 아니라 내부 개발 워크스페이스에서 진행합니다. 공개 GitHub 저장소는 README와 Releases 중심으로 운영하며, 실사용자는 설치 파일을 사용합니다.

## 문제 해결

### 계정이 보이지 않음

앱을 재시작한 뒤 계정 목록을 다시 로드하세요. 로컬 계정 데이터는 `%APPDATA%\com.gpt-usage-manager.app\accounts.json`에 있습니다.

### 사용량 갱신 실패

계정 카드의 최근 오류를 확인하고, 로그인 세션이 만료됐다면 해당 계정만 다시 로그인하세요. 전체 갱신 전에 오류 카드의 계정 유형과 조직을 확인하면 개인·비즈니스 계정을 잘못 인증하는 문제를 줄일 수 있습니다.

### Codex 전환 후 다시 로그인 요구

Codex 앱에서 올바른 조직으로 진입한 상태인지 확인한 뒤 해당 계정 카드에서 `Codex 저장`을 다시 실행하세요. 계정 식별자가 충돌하면 앱은 자동 덮어쓰기 대신 충돌 안내를 표시합니다.

## 릴리즈 정책

- 공개 저장소의 기본 화면은 이 README를 중심으로 유지합니다.
- 실행 파일과 업데이트 메타데이터는 GitHub Releases에만 업로드합니다.
- 릴리즈에는 Windows 설치 파일과 Tauri updater 서명 파일을 함께 제공합니다.
- 사용자 세션, 브라우저 프로필, Codex 인증 파일은 어떤 릴리즈에도 포함하지 않습니다.

## 라이선스

MIT License. 자세한 내용은 [MIT License 전문](https://opensource.org/license/mit)을 참고하세요.
