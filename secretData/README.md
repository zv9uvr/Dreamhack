# 🔐 Dreamhack Challenge: Secret Data System Exploit

이 저장소는 **Dreamhack**의 "Secret Data System" 문제를 해결하기 위한 **Blind SQL Injection** 자동화 스크립트를 포함하고 있습니다.

## 📝 문제 개요
- **문제 유형**: Web Hacking / SQL Injection
- **주요 취약점**: `search` 기능 내에서 사용자 입력값이 필터링 없이 SQL 쿼리에 삽입되어 발생하는 **Blind SQL Injection**.
- **목표**: `users` 테이블에서 `admin` 계정의 `password`를 추출하여 관리자 패널에 접속.

## 🛠️ 취약점 분석
`search` 함수에서 다음과 같은 형태의 취약한 쿼리가 실행됩니다:
```python
sql = f"SELECT COUNT(*) FROM secret_data WHERE title LIKE '%{query}%'"
