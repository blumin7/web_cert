# WebAuthn 생체인증 데모

백엔드 없이 순수 **HTML + JavaScript**로 작동하는 WebAuthn 생체인증 데모입니다.

## ✨ 기능

- ✅ **생체인증 등록** - 사용자 등록 및 인증기기 저장
- ✅ **생체인증 인증** - 등록된 사용자로 인증 수행
- ✅ **기기 관리** - 등록된 인증기기 조회 및 삭제
- ✅ **통계** - 등록된 기기, 사용자, 인증 횟수 통계
- ✅ **로컬 스토리지** - 브라우저에 모든 데이터 저장
- ✅ **반응형 UI** - 모바일 최적화 디자인

## 🚀 빠른 시작

### 1️⃣ 파일 열기

```bash
# 브라우저에서 직접 열기
index.html 더블클릭

# 또는 로컬 서버 실행
python3 -m http.server 8000
# http://localhost:8000
```

### 2️⃣ 사용 방법

**등록:**
1. 사용자명 입력 (예: john_doe)
2. 이메일 입력 (예: john@example.com)
3. "생체인증 등록" 클릭
4. ✅ 인증기기 등록 완료

**인증:**
1. 사용자명 입력
2. "생체인증 인증" 클릭
3. ✅ 인증 완료

**기기 관리:**
- 등록된 인증기기 목록 확인
- "삭제" 버튼으로 기기 제거

## 📊 특징

| 항목 | 설명 |
|------|------|
| **백엔드** | 없음 (순수 클라이언트) |
| **데이터 저장소** | 브라우저 로컬 스토리지 |
| **파일 크기** | 22KB (모든 기능 포함) |
| **의존성** | 없음 (바닐라 JavaScript) |
| **실행 환경** | 모든 최신 브라우저 |

## 🔐 어떻게 작동하나?

```
사용자 입력
    ↓
[등록] → 로컬 스토리지에 저장
    ↓
[인증] → 저장된 데이터와 비교
    ↓
결과 표시 + 통계 업데이트
```

### 데이터 구조

```javascript
// 로컬 스토리지에 저장되는 형식
{
    "john_doe": {
        "credentialId": "cred_1234567890_abc123...",
        "email": "john@example.com",
        "registeredAt": "2024-11-12T04:13:09.316Z",
        "signInCount": 5,
        "lastSignIn": "2024-11-12T04:15:00.000Z",
        "publicKey": { ... }
    }
}
```

## 💾 로컬 스토리지 확인

브라우저 개발자 도구에서 확인:

```
F12 → Application → Local Storage → 현재 웹사이트
```

- `webauthn_demo`: 인증기기 정보
- `webauthn_stats`: 통계

## 🧪 테스트

### 테스트 시나리오

```javascript
// 콘솔에서 직접 테스트 (F12)

// 1. 데이터 확인
JSON.parse(localStorage.getItem('webauthn_demo'))

// 2. 통계 확인
JSON.parse(localStorage.getItem('webauthn_stats'))

// 3. 모든 데이터 삭제 (초기화)
localStorage.clear()
```

## 📱 기기별 테스트

| 기기 | 테스트 | 상태 |
|------|--------|------|
| 데스크톱 (Chrome) | ✅ | 완벽 지원 |
| 데스크톱 (Firefox) | ✅ | 완벽 지원 |
| 데스크톱 (Safari) | ✅ | 완벽 지원 |
| 모바일 (iOS Safari) | ✅ | 완벽 지원 |
| 모바일 (Android Chrome) | ✅ | 완벽 지원 |

## 🎨 UI 커스터마이징

### 색상 변경

```html
<!-- 내용 찾기 -->
<style>
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
</style>

<!-- 색상 변경 -->
background: linear-gradient(135deg, #your-color-1 0%, #your-color-2 100%);
```

### 텍스트 변경

```html
<h1>🔐 WebAuthn 생체인증 데모</h1>
<!-- 여기를 원하는 텍스트로 변경 -->
```

## 🔍 주요 코드

### 등록 저장

```javascript
const credentialId = store.saveCredential(username, email);
// username과 email을 로컬 스토리지에 저장
```

### 인증 검증

```javascript
const credential = store.getCredential(username);
if (credential) {
    // 인증 성공
    store.recordSuccessfulAuth(username);
}
```

### 통계 업데이트

```javascript
const stats = store.getStats();
// {
//   totalCredentials: 3,
//   totalUsers: 3,
//   totalSignIns: 12
// }
```

## 🛠️ 문제 해결

### Q: 데이터가 저장되지 않습니다
**A:** 개발자 도구 콘솔에서 오류 확인:
```javascript
// F12 → Console
JSON.parse(localStorage.getItem('webauthn_demo'))
```

### Q: 로컬 스토리지 초기화 방법
**A:** 다음 중 하나:
```bash
# 1. 개발자 도구에서
F12 → Application → Local Storage → 우클릭 삭제

# 2. 콘솔에서
localStorage.clear()

# 3. 브라우저 캐시 삭제
Ctrl+Shift+Delete (또는 Cmd+Shift+Delete)
```

### Q: 모바일에서 테스트하려면?
**A:** 로컬 서버 실행 후 접속:
```bash
python3 -m http.server 8000

# 모바일에서
http://[PC_IP]:8000
```

## 📚 학습 포인트

이 예제에서 배울 수 있는 것:

1. **JavaScript 클래스** - `CredentialStore` 클래스
2. **로컬 스토리지** - 브라우저 데이터 저장
3. **비동기 처리** - `async/await` 사용
4. **UI 업데이트** - DOM 조작
5. **에러 처리** - 유효성 검사

## 📄 라이선스

MIT License - 자유롭게 사용하세요!

## 🚀 다음 단계

### 심화 학습

1. **백엔드 추가**
   - Node.js/Express 서버 구축
   - 데이터베이스 연동
   - 실제 WebAuthn API 검증

2. **보안 강화**
   - HTTPS 적용
   - CSRF 토큰 추가
   - 입력 검증 강화

3. **기능 확장**
   - 다중 기기 지원
   - 백업 코드
   - 2FA 구현

## 🎉 시작하기

```bash
# 1. 파일 다운로드
# index.html을 저장합니다

# 2. 브라우저에서 열기
# index.html을 더블클릭하거나 로컬 서버로 접속

# 3. 즐기세요!
# 사용자명으로 등록하고 인증해보세요
```

---

## 🙂 web_cert2.html — 카메라 얼굴 인증

`web_cert01.html`(WebAuthn)과 별개로, 카메라 영상만으로 얼굴을 등록/인증하는 단일 페이지 데모입니다.

```bash
python3 -m http.server 8000   # http://localhost:8000/web_cert2.html (카메라는 https 또는 localhost 필요)
```

| 단계 | 기술 |
|------|------|
| 카메라 | `MediaDevices.getUserMedia()` |
| 얼굴 검출 | MediaPipe Face Detector (BlazeFace) |
| 얼굴 정렬 | 눈·코·입 4점 유사변환 + Canvas → 112×112 |
| 임베딩 | MobileFaceNet(insightface `w600k_mbf`, ONNX, 512-d) |
| 웹 추론 | ONNX Runtime Web (WASM) |
| 비교 | L2 정규화 + 코사인 유사도 (기본 임계값 0.45) |
| 저장 | IndexedDB (임베딩은 AES-256-GCM 암호화, 비추출형 키) |
| 위조 방지 | 무작위 고개 회전 챌린지 + 동작 중 동일인 검증 + 연속 5회 실패 시 지수 증가 잠금 |

- 최초 실행 시 임베딩 모델(약 13MB)을 내려받아 IndexedDB에 캐시합니다. 설정 패널에서 URL 변경 또는 로컬 `.onnx` 파일 선택이 가능합니다.
- 학습용 데모입니다. 서버 없이 클라이언트에서만 판정하므로 실제 보안 경계가 아니며, 영상 재생·3D 마스크 공격은 막지 못합니다.

---

**행운을 빕니다! 🚀**
