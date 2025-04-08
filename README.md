# ⚙️모터와 조도 센서를 이용한 스마트 환풍기

<br>

## 프로젝트 소개

- 본 프로젝트는 환경 밝기에 따라 자동으로 작동하거나 사용자가 직접 제어할 수 있는 간단한 에어팬 컨트롤러입니다.
- 사람이 활동 중인 낮 시간일 경우 빛을 감지하여 에어팬이 작동하고 사람이 활동하지 않는 저녁 시간일 경우 팬 속도가 줄어 들다가 멈추도록 만들어져 있습니다.

<br>

## 팀원 소개

<div align="center">

| **이종범(팀장)** | **오경택(부팀장)** | **조승제(조원)** | **유승경(조원)** |
| :------: | :------: | :------: | :------: |
| [<img src="https://github.com/user-attachments/assets/bb3ecbe8-f41d-4002-b0b1-1bc1dcaded09" height=150 width=150> <br/> whdqja1128@naver.com](#) | [<img src="https://github.com/user-attachments/assets/b0762a72-3038-46df-bf9f-b31539e4e139" height=150 width=150> <br/> gyeongtaek.dev@gmail.com](#) | [<img src="https://github.com/user-attachments/assets/81e2e847-42bb-4490-9fee-1b5284f3ffe8" height=150 width=150> <br/> jsj6584@naver.com](#) | [<img src="https://github.com/user-attachments/assets/396b1fb0-ded6-4694-aa1c-49596d840781" height=150 width=150> <br/> tmdrud7766@gmail.com](#) |

</div>
<br>

## 프로젝트 개요

이 프로젝트는 STM32F10x 마이크로컨트롤러를 사용하여 에어팬을 제어하는 간단한한 시스템을 구현한 것입니다. 주요 기능은 다음과 같습니다:

- 자동 모드: CDS 센서를 통해 환경 밝기에 따라 팬 속도를 자동으로 조절합니다.
- 수동 모드: 사용자가 직접 팬 속도를 설정하고 방향(정방향/역방향)을 제어할 수 있습니다.
- UART 통신: 사용자는 UART를 통해 팬을 제어하는 명령을 보낼 수 있습니다.

<br>

## 개발환경

- 코드 에디터: Visual Studio Code
- 터미널: Tera Term (시리얼 통신 모니터링)
- 협업 방식: 로컬에서 팀원들과 직접 만나 함께 작업
- 개발 언어: C

<br>

## 디렉토리 구조 및 파일 설명

```
stm32-air-fan-controller/
├── drivers/
│   ├── adc.c
│   ├── clock.c
│   ├── key.c
│   ├── led.c
│   ├── systick.c
│   ├── timer.c
│   └── uart.c
├── core/
│   ├── core_cm3.c
│   └── core_cm3.h
├── include/
│   └── device_driver.h
└── src/
    ├── main.c
    └── runtime.c
```

<br>

## 주요 컴포넌트

### ADC (adc.c)

- CDS 센서 값을 읽기 위한 ADC 초기화 및 제어
- PA5 핀에 연결된 아날로그 센서 값을 디지털로 변환

### 타이머 (timer.c)

- TIM2를 사용한 PWM 출력으로 모터 속도 제어
- PA2와 PA3 핀을 통해 H-브릿지 모터 드라이버 제어
- 정방향/역방향 회전 및 속도 조절 가능

### 키 입력 (key.c)

- PB6, PB7 핀에 연결된 버튼 입력 처리
- 디바운싱 처리가 포함되어 있음

### UART (uart.c)

- UART1을 사용한 직렬 통신 (115200 baud)
- 'F'(정방향), 'R'(역방향), 'S'(정지) 명령 처리
- 디버깅 및 상태 정보 출력을 위한 printf 기능 구현

### 메인 로직 (main.c)

- 자동 모드: CDS 센서 값에 따라 팬 속도를 조절
- 수동 모드: 버튼 또는 UART 명령을 통해 팬 속도 및 방향 제어
- 모드 전환 기능: Key1을 누르면 자동 모드, Key2를 누르면 수동 모드로 전환

<br>

## 맡은 역할
