---
title: "[CS] HTTP Request Method란?"
excerpt: "API 연동 시 사용하는 HTTP Request Method(GET, POST, PUT, PATCH, DELETE)의 개념과 사용법을 알아봅니다."
layout: single
categories:
  - cs
tags:
  - HTTP
  - API
  - Network
author_profile: false
sidebar:
  nav: "docs"
search: true
toc: true
toc_sticky: true
toc_label: 목차
date: 2025-12-02 00:00:00 +0900
---

## HTTP Request Method란?

웹사이트나 서버(API)에게 요청을 보낼 때 "이 데이터를 가지고 뭘 하고 싶은지" 의도를 알려주는 명령어? 느낌이다.

각각 하나씩 알아보면서 언제 어떤 것을 쓰면 좋을지 이 글을 보고 판단하면 될 것 같다.

내 머릿속에 있는 내용을 최대한 간결하게 적었음.

<p align="center">
  <img src="/images/cs/2025-12-02-http-request-method/Gemini_Generated_Image_42ijn342ijn342ij.png" alt="HTTP Request Method 썸네일" width="50%">
</p>

### 1. GET (조회)

- 의미: 데이터 좀 보여줘
- 언제 씀: 날씨, 환율, 뉴스 기사 같은 정보 가져올 때

### 2. POST (생성)

- 의미: 이거 새로 등록해줘
- 언제 씀: 슬랙/디스코드에 메시지를 쏠 때, 노션에 새 페이지 만들 때

### 3. PUT (전체 수정)

- 의미: 이걸로 싹 덮어씌워줘.
- 언제 씀: 기존 정보 싸그리 무시하고 통째로 교체할 때 (기존 데이터 날라감 주의!)

### 4. PATCH (일부 수정)

- 의미: 이 부분만 고쳐줘.
- 언제 씀: 회원 정보 중 '비밀번호'만 바꾸거나, 주문 상태만 '배송중'으로 변경할 때

### 5. DELETE (삭제)

- 의미: 이거 지워라.
- 언제 씀: 구글 캘린더 일정 삭제, DB 데이터 날릴 때

---

사실 이 5개만 알아도 될 것 같아서 나중에 나머지 두 개 필요하면 그때 정보를 추가하겠다.
