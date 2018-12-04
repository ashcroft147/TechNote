# NRTP Batch 개발방법

## CM 등록 절차

테스트계는 아래 환경정보를 바탕으로 직접 등록할 수 있다
대신 가동계는 RR등록시 CM등록요청서를(Excel,PPT) 첨부해서 같이 요청한다. 
만약 RR이 없는 경우는 팀장님 결제를 맡아서 CM등록요청서를 담당자에게 송부한다. 

## URL
- 테스트계(광양): http://tksmartfactory.posco.co.kr:8031/scheduler-manager/
- 테스트계(포항): http://tpsmartfactory.posco.co.kr:8031/scheduler-manager/
- 가동계: http://ksmartfactory.posco.co.kr:8031/scheduler-manager/

## 계정
 - 광양 개발계(가동계): devuser/welcome
 - 포항 개발계 : devuser / roqkf!23

## 

## 등록절차
Meta데이터 관리
Job Group M00S20 에 만들어진 기존 자원 복사

## 작성방법
Cron 표현식을 기반으로 작성한다.
Cron Trigger
6
Cron 표현식
0 , 1/5, ***?
00 1/5 * * * ?
초 분 시 일 월 년
smart policy(default)

## RTP Call NRTP Batch

### Glue Batch JOB 정의