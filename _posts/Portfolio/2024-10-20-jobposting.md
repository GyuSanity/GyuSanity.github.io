---
layout: post
title: Job Posting
category: portfolio
tag: [portfolio]
---

## SR 로봇 사업팀

### Keyworkd

#주요 담당 업무
[Robot Framework]
플랫폼 기반 SW 개발 및 API 설계 경험 (Android/Tizen 등)
임베디드 SW 및 리눅스 SW 개발 경험 <<<<<<
로봇 SW 개발 경험 (ROS 등)<<<<<<

- C/C++, Python

[Robot System SW]
임베디드 Linux 적응 MCU/RTOS 기반 SW 개발 경험
임베디드 Linux 적응 BSP 포팅 및 Device driver 개발 경험
EtherCAT 기반 모터 제어 SW 개발 경험 <<<<<<
성능 분석 및 최적화 경험 <<<<<<

- C/C++

#주요 우대사항
[Robot Framework]
Robot Framework

클라우드 연계 SW 개발 및 API 설계 경험 (Android/Tizen 등)
임베디드 SW 및 리눅스 SW 개발 경험
로봇 SW 개발 경험 (ROS 등)
C/C++, Python

[Robot System SW]
임베디드 Linux 적응 MCU/RTOS 기반 SW 개발 경험
임베디드 Linux 적응 BSP 포팅 및 Device driver 개발 경험
EtherCAT 기반 모터 제어 SW 개발 경험
성능 분석 및 최적화 경험

## 1. 입사이후 직무이력 및 실적을 모두 기재

==> profile 작성예정

## 2. 지원동기를 자신의 구체적인 경험과 연결지어 설명해주세요.

[지원동기]
제 임베디드 HW/SW 개발 경험이 사람들의 삶을 편리하고 행복하게 만드는 삼성 리서치 로봇사업부에 기여할 수 있다고 확신했기 때문입니다.

[구체적인 경험과 연결]
저는 드론 및 무선전력카메라 시스템을 개발해본적이 있습니다.

1. 드론 제어기 제작 및 Hover 모드 구현 (Yaw축/Altitude 축 PI 제어)
   상용화된 quadcopter 드론이 아닌 Unicoptor 형태의 S-Cloud를 개발한적 이 있습니다.
   S-cloud는 유체가 곡면을 흐를떄 휘는 코안다을 이용해 BLDC 모터 밑에 돛을 놓아 체공시간을 향상 시킨 드론입니다.
   MCU(Atmega2560)와 센서를 활용하여 안정적인 드론을 개발했고,
   이 결과로 IEEE/ASME Transactions on Mechatronics에 논문을 게재했습니다.

▶ HW 구성
[Power Line]
전압분배보드(BEC)를 활용하여 입력전압을 2개로 나눔(5V는 MCU/센서/DC모터, 11V는 BLDC)
[MCU 주변장치 인터페이스]
I2C를 활용한 라이더센서(LW20)
인풋 캡쳐모드를 활용한 RF Receiver 입력 듀티비 측정
USART를 활용한 블루투스 및 9 DOF IMU 연결
PWM을 활용한 BLDC 및 DC 모터 제어
[PCB 보드 제작]
Eagle을 활용 제작하였으며, 다음과 같은 노하우 습득
단가 절감을 위한 via 최소화
고주파 신호라인 신호 반사를 최소화 하기 위해 90도 배선 라인 제거
powerline은 24 mil, 신호라인은 10-14mil로 제작, 공통 접지라인 배치
▶ SW 구성
[성능 분석&최적화를 통한 Hover 모드 구현]
블루투스 통신을 통해 필요한 센서 데이터 취득(Altitude, ROLL-PITCH-YAW 데이터 수집)
기체 자체가 순간적인 플랩[ROLL-PITCH] 외란에 대해선 감쇠진동으로 기체에 주는 영향이 없어 YAW축만 제어 수행
센서측정값을 오일러 각 및 각속도로 환산하여 PI 제어를 수행
PWM 타이머 분주비를 줄여 듀티비 Range를 확장했으며, 작은 보상 값에도 민감하게 반응하지 않도록 적용(듀티비값 8k-16k로 확장)
모터 진동에 의해 센서측 수집데이터에 오류가 생겨 SW/HW적으로 보상(SW: 센서 내 Low Pass Filter 활용, HW : damper를 설치)

2. 저전력으로 구동하기 위한 무선전력 카메라 시스템
   RF 무선 전력 전송을 이용해 365일 동작할 수 있는 카메라 시스템을 개발했습니다.
   저전력 통신 모듈(BLE)가 내장된 MCU(ARM Cortex기반 CC2650)를 사용해 설계를 진행했으며,
   이 결과로 한국통신학회 논문지에 논문을 게재했습니다.

▶HW 구성
[Power Line]
다중 안테나로 수확된 에너지를 슈퍼 커패시터에 저장
누적된 에너지는 DC-DC 컨버터를 통해 센서 및 MCU에 3.3V 인가
[MCU 주변 장치 인터페이스]
인터럽트 신호를 PIR 센서를 활용하여 동작감지 수행
I2C 통신을 통해 카메라+FIFO 메모리 제어
GPIO 입출력 포트 설정을 통해 FIFO 메모리 Read/Write 접근
ADC 기능을 통해 DC-DC 컨버터측 수확되는 전력량 모니터링
BLE 스택을 활용하여 저전력 빔 요청/중단 통신 구현
[PCB 보드 제작]
Eagle을 활용하여 센서부 회로 제작

▶SW 구성
[성능 분석&최적화를 통한 초전력 카메라 시스템 구현]
블루투스를 통해 누적 전압량을 실시간 모니터링 수행
BLE 전용 레지스터를 활용하여 전력량이 부족할 경우 빔 on/off에 대한 패킷[Preamble 신호]을 전력 송신측과 주고 받도록 처리
동작 알고리즘을 3단계(Shutdown/Active-영상촬영/Active-빔요청)로 나누어 정의
Task별 전력 소비 모델 프로파일링 수행
프로파일을 통해 전력 소비량이 가장 큰 영상촬영 태스크를 조절(24MHz CLK으로 QQVGA 프레임으로 촬영)

## 3. 기타

위 외에도 아래와 같은 프로젝트 수행 경험과 역량을 가지고 있습니다.

[Project]

- MCU(LattePanda)를 활용한 스마트 미러(X-mirror 개발)
- XY 스테이지 모터 제어 프로젝트 ( 엔코더가 내장된 모터 제어를 수행해보았으며, 영상처리를 위한 OPENCV와 MFC 다이얼로그 툴창을 개발해보았음)
- 모터 제어 설계 프로젝트 ( 엔코더가 달린 DC 모터를 2차함수의 전달함수로 모델링해보았으며, PID 제어를 통해 과도/정상상태의 응답을 확인)
- 물체 추적 2WD 자동차 프로젝트 ( ARM Cortex와 여러 센서를 활용하여 어떻게 연동하여 디자인 할지 학습 )
- 데이터 수집기를 활용한 컴퓨터간 통신 프로젝트 ( 여러 센서들을 구비한 데이터 수집기를 만들어 RS-232 Serial 통신을 통해 컴퓨터간 데이터 주고 받기)
- 포트포워딩 무선통신 프로젝트 ( 앱 제작을 통해 원격에서 2WD 자동차 제어 수행 )
- 영상 정합 복원 프로젝트 ( 다중 기기에서 습득된 영상을 OPENCV를 활용해 정합해보는 실습 수행 )
- 적외선 영상과 광학 영상의 정합 수팽 프로젝트 ( 광학 영상과 IR 영상 정합을 위해 해리스 코너 검출 + 허프변환을 학습한 프로젝트 )
- ATMEGA128 설계 프로젝트 ( 카르노 맵을 통한 어드레스 디코더 설계 및 이를 통한 PCB 기판 제작 수행 프로젝트 )

[Certificates]

- SW Certi. Pro ( 타겟 환경에 맞추어 여러가지 알고리즘을 조합하여 프로그래밍 가능)
- Data Science -Level2 ( 수집된 Data에 기본적인 처리 및 분석 가능 )
- OPIC AL ( 영문화된 문서에 친숙하며 해외연구소와 협업 및 소통 가능 )

[Honor]

- ITRC 메이커톤 2019 과기정통부 장관상( 최우수상 )
- 석사 수석 (GPA : 4.5/4.5)
- 학사 차석 (GPS : 4.3/4.5)

함께 성장할 수 있는 기회를 주신다면 최선을 다할 자신이 있으며, 보시는 데 도움이 될까 정리된 PDF 파일도 첨부합니다.
긴 글 읽어주셔서 감사드립니다.
https://github.com/GyuSanity/portfolio/blob/main/2024_Gyu_portfolio.pdf
