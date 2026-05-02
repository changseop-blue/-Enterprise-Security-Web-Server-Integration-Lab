# 🔒 Enterprise Security & Web Server Integration Lab

제공해주신 `image_1180bb.png`는 네트워크 토폴로지나 시스템 구성도를 명확하게 보여주는 시각적 자료로 활용하기에 아주 좋습니다. 

기존 웹 서버 구축 및 DB 보안 실습 내용에 본 이미지(네트워크 구성도)를 통합하여, GitHub에 바로 올리실 수 있도록 `README.md` 및 폴더 구조를 업데이트했습니다.

---

## 🏗️ 전체 시스템 아키텍처 및 네트워크 구성

> **[참고]** 업로드하신 `image_118516.png`와 `image_1180bb.png`는 각각 실습의 핵심 네트워크 토폴로지와 세부 구성도를 나타냅니다. `docs/` 폴더에 함께 보관하여 문서화할 수 있습니다.

| 역할 | OS | 주요 구성 요소 및 보안 조치 내용 |
| :--- | :--- | :--- |
| **Web Server** | **Rocky Linux 9 / AlmaLinux 9** | - FileZilla를 통한 아카이브(`cbt_main_home.tar`) 전송 및 배포<br>- Nginx 웹 서버 및 보안 헤더 적용<br>- SELinux 및 방화벽(FirewallD) 활성화 |
| **Database Server** | **Rocky Linux** | - MariaDB 구축 및 데이터베이스 보안 구현 보고서 내용 적용<br>- SSL/TLS 암호화 통신 적용 및 암호화 검증<br>- SQL Injection 대응 (Prepared Statement 적용) 및 최소 권한 부여 |
| **Tester** | **Kali Linux** | - Nmap을 이용한 포트 스캔 및 취약점 점검<br>- Nikto를 활용한 웹 취약점 진단 및 무결성 검증 |

---

## 📂 디렉토리 구조

```text
enterprise-security-lab/
├── .gitignore
├── README.md
├── configs/
│   ├── nginx.conf              # Nginx 보안 설정
│   └── db_hardening.sql        # DB 보안 설정 및 스키마 적용 SQL
├── src/
│   └── cbt_main_home/          # FileZilla로 전송된 Security Archive 소스 파일
└── docs/
    ├── architecture.md         # 전체 시스템 아키텍처 설명
    ├── topology_01.png         # image_118516.png 파일 사본
    ├── topology_02.png         # image_1180bb.png 파일 사본
    └── DB보안구축_이창섭.pdf   # 데이터베이스 보안 구현 보고서
```

---

## 🚀 주요 실습 및 구현 내역

### 1. 웹 서버 구축 및 파일 전송
- **파일 전송:** FileZilla 클라이언트를 사용하여 Rocky Linux IP로 SFTP 접속 후 `cbt_main_home.tar` 전송 및 업로드.
- **배포 및 구성:** `tar -xvf` 명령어를 통해 소스 배포 및 Nginx 기본 경로 설정.
- **웹 서버 보안:**
  - HTTP 보안 헤더 적용 (`X-Frame-Options`, `X-Content-Type-Options`, `HSTS`).
  - TLS 1.3 프로토콜 적용 및 암호화 스위트(Cipher Suite) 최적화.

### 2. 데이터베이스 보안 구현 (보고서 기반)
- **설계 및 오류 수정:** DDL(modelDB2.sql) 및 DML(modelDB3.sql) 오류 수정 및 스키마 검증 완료.
- **계정 및 접근 제어:** `root` 계정 원격 접속 차단 및 최소 권한(GRANT) 재설정.
- **데이터 보호:** OpenSSL을 이용한 SSL/TLS 적용 및 Wireshark 패킷 분석을 통한 암호화 실증.
- **취약점 조치:** SQL Injection 취약점 분석 후 `Prepared Statement` 적용을 통한 공격 차단.

-----------
진행중으로 내용은 수정 될 수 있습니다
### 3. 보안 검증 (Kali Linux)
- 포트 스캔(`Nmap`)을 통한 불필요한 포트 및 서비스 차단 확인.
- 웹 취약점 점검(`Nikto`)을 통한 디렉토리 리스팅 및 서버 정보 노출 방어 확인.



