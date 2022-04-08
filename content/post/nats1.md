---
title: "Nats1"
date: 2022-04-08T18:24:08+09:00
draft: false
description: "Desc Text."
series: ["NATS"]
categories: ["Network"]
tags: ["nats", "MSA"]
---

### NATS 개요

- 분산형 시스템을 위한 연결 기술 → “Message oriented middleware”
- 메시지 주소지정, 검색, 교환 등의 기능
- 질문과 답변, 명령문 작성과 실행, 스트림 프로세스 처리 등에 사용

### NATS 특징

- 손쉬운 다대다 연결
  - hostname이나 port가 아니라 subject 기준으로 관리한다.
  - load balancers, log systems 부터 proxies and sidecars 까지 1:1 연결에는 한계가 있다.
- 배포 용이성
  - VM, container, K8S, device 등 어느 환경에서도 배포 가능
- 안전성
  - 보안을 위한 네트워크 경계 지정을 안해도 될 만큼 안전함
- 높은 확장성, 하이브리드 배포, 적응성
- **Use Cases**
  - Cloud Messaging
    - Services (microservices, service mesh)
    - Event/Data Streaming (observability, analytics, ML/AI)
  - Command and Control
    - IoT and Edge
    - Telemetry / Sensor Data / Command and Control
  - 레거시 메시징 시스템의 확장 및 교체

### NATS란?

- **NATS Client Applications**
  - NATS 클라이언트 라이브러리를 사용해 다른 app과 pub&sub, 요청&응답을 수행할 수 있다.
  - NATS 서버 관점에선 클라이언트인 것이다.
- **NATS client와 NATS server 연결하기**
  - 연결하기 위한 config
    - NATS 서버의 URL
    - Authentication(필요시) : Token, TLS, user/pass 등 다양한 방식
- **Simple messaging design**
  - 메시지는 subject에 의해 주소 지정되고 식별된다. (네트워크 위치와 무관)
  - 퍼블리셔는 데이터를 인코딩해 전달하며 구독자는 받아서 디코딩한다.
- **Quality of Service (메시지 품질 관리)**
  - Core만 사용하는지, JetStream도 사용하는지에 따라 다르다.
  - **Core NATS → At most once QoS(최대 한번)**
    - 구독자가 Topic에 연결된 상태라면 메시지가 수신되지만 그렇지 않은 경우 (나중에) 메시지를 수신 할 수 없다.
    - TCP/IP 수준의 보증이다.
    - fire-and-forget 메시징 시스템으로 메모리에만 저장하고 disk 저장안함
  - **NATS JetStream → At-least(한번이상) / exactly once(정확히 한번)**
    - 최소 한번 또는 정확하게 한번 → 메시지에 대한 더 높은 품질이 필요할때
    - 지속적인 스트리밍, 플로우 제어, 키-값 스토어 등 기능이 필요할때
    - (JetStream은 NATS 서버에 내장되어 있음)

### Subject-Based Messaging

- **Subject란?**
  - publisher와 subscriber가 서로를 찾을 수 있게 해주는 문자열 (주소 식별)
  - 메시지를 스트림 혹은 토픽으로 분류해준다.
  - 알파벳 대소문자, `.` , `*` , `>` 사용 가능
  - `.` 으로 계층 표현, `*` 은 싱글 토큰 매칭, `>` 은 멀티플 토큰 매칭

### Core NATS

- **Publish-Subscribe (일대다 통신)**
  - publisher는 subject에 메시지를 송신
  - 해당 subject를 리스닝하고 있는 subscriber는 액티브하게 메시지를 수신
  - 메시지 구성 (기본 1MB, 최대 64MB, 적정최대 8MB)
    1. A subject.
    2. A payload in the form of a byte array.
    3. Any number of header fields.
    4. An optional 'reply' address field.
