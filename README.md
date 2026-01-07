# 📌 **Smart Vending Machine System**
> 라즈베리파이 기반 Linux 임베디드 환경에서 서버·DB·MCU·하드웨어 제어를 통합한 스마트 자판기 시스템을 구현했습니다.

---
## 📌 1. 프로젝트 목표

- Raspberry Pi와 STM32F411RE 간 안정적·양방향 통신 구조(UART 기반 명령–응답 프로토콜) 구축
- 서버·DB·MCU 제어 로직을 하나로 통합하는 IoT 자판기 전체 시스템 아키텍처 구현
- 통신 결과를 DB와 웹 UI로 연결하여 사용자에게 실시간 주문·배출 상태 제공
- 실제 제품화 가능한 임베디드 통신·제어 중심의 스마트 자판기 플랫폼을 구축하는 것이 최종 목표

---
## 🎬 2. 시연 영상

https://github.com/user-attachments/assets/974a988a-d14f-4c7d-a3ee-1f0fbd7d100e

---
## 🧠 3. 시스템 아키텍처
<img width="967" height="541" alt="image" src="https://github.com/user-attachments/assets/27410ad9-fb5f-4093-b7c0-6b700b640afb" />

---
## 🔧 4. 핵심 기능

### 🖥 UI (운영)
- 웹 기반 UI를 통해 메뉴 조회·주문·결제 화면을 구성하고, 사용자 입력 흐름을 설계
- 주문 요청에 따른 주문 상태(대기 / 처리 / 완료 / 실패)를 화면에 실시간 표시
- DB 변경 사항(메뉴 정보, 가격 등)이 UI에 즉시 반영되도록 서버–UI 연동 구조 구성
- 서버 처리 결과를 기반으로 사용자에게 명확한 피드백을 제공하는 화면 흐름 구현
 

### ⚙️ Device (제어)
- STM32F411RE 기반 MCU에서 모터·솔레노이드·LED·버튼·IR 센서 제어 로직 구현
- IR(광) 센서를 이용해 아이템 낙하 여부를 감지하고, MCU에서 상태 판단 수행
- UART 기반 통신을 통해 센서 결과 및 장치 상태를 Raspberry Pi로 전달
- Raspberry Pi에서 전달된 명령에 따라 슬롯 배출 → 센서 확인 → 성공/실패 판정으로 이어지는 제어 흐름 설계
- 입력 → 상태 판단 → 제어 출력이 분리된 임베디드 제어 구조 구성
 
### 🗃 Data (기록)
- MySQL DB를 활용해 메뉴 정보, 주문 내역, 주문 시간, 주문 상태 데이터 저장
- 주문 처리 결과(성공 / 실패)를 DB에 기록해 이력 관리 구조 구성
- 장치 동작 결과 및 센서 판정 결과를 서버 로직과 연계한 데이터 흐름 설계
- REST API를 통해 저장된 주문 및 상태 데이터를 조회할 수 있도록 구성

---
## ⚙️ 5. 구현 상세

커널·디바이스 드라이버를 직접 구현하는 저수준 프로그래밍을 포함하지는 않지만,  
Raspberry Pi 기반 임베디드 Linux 환경에서 **하드웨어 제어와 서버 로직이 동시에 안정적으로 동작해야 하는 구조**를 고려해 시스템을 설계했습니다.

GPIO·UART·I2C·SPI를 통한 장치 제어 흐름과 서버 요청 처리 흐름을 명확히 분리하고,  
**실제 장치 동작 결과를 기준으로 주문 상태를 단계적으로 관리**함으로써  
주문 상태와 모터 구동 상태가 어긋나는 문제를 방지하는 안정적인 제어 구조를 구현했습니다.

---
## 🧩 6. 기술 요약

- **Hardware / Embedded Platform**:  Raspberry Pi (Linux), STM32F411RE, GPIO, IR Sensor, Motor, Solenoid, LED
- **Language**: C
- **Server**: C 기반 HTTP Server
- **Database**: MySQL
- **Communication**: UART (Raspberry Pi ↔ STM32)


  

