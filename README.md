# 기초 화장품 추천 디스펜서
  
## 프로젝트 개요
> AI 기반으로 카메라를 이용해 사용자 얼굴의 피부 상태를 분석 후, 개인 맞춤형 기초 화장품을 자동으로 디스펜싱하는 시스템
## 시스템 기능
- 🎥 AI 기반 피부 분석: Intel Geti SDK + PyTorch를 활용한 5개 얼굴 영역별 피부 상태 분석<br>
- 💧 다중 피부 지표 측정: 수분, 탄력, 색소침착, 모공 상태 정량화<br>
- 🧴 스마트 디스펜싱: 분석 결과 기반 개인 맞춤형 화장품 자동 분배<br>
- 📊 사용자 프로필 관리: SQLite 기반 분석 이력 및 개인 데이터 저장<br>
- 🔄 실시간 처리: Qt GUI를 통한 실시간 카메라 캡처 및 분석 결과 확인<br>

## 활용 데이터 셋
<img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/eac940ce-d149-4ebf-8fef-1203aed528ab" /><br>
-  출처: [AI-Hub 한국인 피부상태 측정 데이터](https://www.aihub.or.kr/aihubdata/data/view.do?pageIndex=1&currMenu=115&topMenu=100&srchOptnCnd=OPTNCND001&searchKeyword=%ED%95%9C%EA%B5%AD%EC%9D%B8&srchDetailCnd=DETAILCND001&srchOrder=ORDER001&srchPagePer=20&srchDataRealmCode=REALM001&aihubDataSe=data&dataSetSn=71645)
  
## 시스템 구성도
<img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/1d4378e2-1004-4739-8ceb-69b8a419061f" />

## 시스템 흐름도
<img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/78a9f8e4-9106-40a3-8c21-242f7511aab5" />

## 담당 역할
- 하드웨어 제작 & 설계
- 데이터 셋 Annotation
- 하드웨어 동작 흐름 : 라즈베리파이로부터 피부 상태(수분@탄력@미백@모공)의 값을 수신 -> Uart로 수신한 값을 파싱[예) 1@0@1@1 -> arrbuff[]={1,0,1,1}] -> 파싱 값에 따라 각 서보모터를 순차적으로 동작 및 LED 점등 기초 화장품 추천 디스펜서
  
## 담당 역할
- 하드웨어 제작 & 설계
- 데이터 셋 Annotation
- 하드웨어 동작 흐름 : 라즈베리파이로부터 피부 상태(수분@탄력@미백@모공)의 값을 수신 ➡️ Uart로 수신한 값을 파싱[예) 수신 값: 1@0@1@1, 파싱 값: arrbuff[]={1,0,1,1}] ➡️ 파싱 값에 따라 각 서보모터를 순차적으로 동작(화장품 제공) 및 LED 점등 ➡️ 화장품 제공 완료 시, 라즈베리파이에 성공 이벤트 전송 
  
## 사용 기술
| 구분 | 기술&장비|
|---|---|
| MCU & Module | STM32 Nucleo F411RE, Raspberry Pi 4B |
| 개발 TOOl | STM32CubeIDE, Intel Geti | 
| 통신 | Uart-DMA |
| Sensor | Servo Motor, LED |
| Language | Python, C |
| OS | FreeRTOS |

## 개발 중 문제 및 해결
| 제작/기획 과정 | 문제점 | 해결 방안 |
|---|---|---|
| 원판 제작 | 펌프를 누르는 힘 + 화장품 무게를 버틸 프레임 필요 | 터틀봇 기본프레임인 "TB3 와플플레이트-IPL-01" 4개 사용 |
| 스텝 모터 선정 | 스텝 모터(28byj-48)의 토크 부족 | nk244-01at과 rb step motor 17hdc1031 테스트 완료 |
| 스텝모터-원판 연결부 | 교체할 스텝모터의 로터 와 연결부의 호환이 안됨 | nk244-01at과 rb step motor 17hdc1031의 로터에 맞는 연결부 제작 |
| 펌프 누르는 방식 | 스텝모터에 나사산을 달아 회전시켜 방식 기획 _ 3D프린터의 제작 크기와 정확도의 문제 | 스텝 모터로 누르는 방식 대신 서보 모터로 누르는 형태 채택 |<br>
> - 초기 설계 : 원판 프레임과 연결된 **스텝 모터**로 90도 씩 회전시켜 프레임 위에 놓인 4개의 화장품을 제공
> - 개선 설계 : 일렬로 세운 각 화장품에 **서보 모터** 하나씩 연결해 제공 

## 시연 결과
<img width="300" height="350" alt="image" src="https://github.com/user-attachments/assets/7ac4537c-bb71-4066-a14d-c7e5ca61df34" /> <img width="300" height="350" alt="image" src="https://github.com/user-attachments/assets/8f339bc2-1e53-4784-88cd-2a0a6c7987a1" />

