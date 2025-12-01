---
title: "[메타코드] n8n 스터디 후기_1주차 : n8n의 세계에 들어가며"
excerpt: "메타코드 everyai 1기로 참여하여 n8n 자동화 도구 학습을 시작했습니다. Trigger node, Credential 개념을 배우고 Gemini + Gmail 연동 실습을 진행했습니다."
layout: single
categories:
    - n8n
tags:
    - n8n
    - 자동화
    - 메타코드
    - everyai
    - Gemini
    - Gmail
author_profile: false
sidebar:
    nav: "docs"
---

![메타코드 Every AI 1기]({{site.url}}/images/etc/n8n/2025-11-22-metacode-n8n-week1/image.png){: .align-center}

> 일부 이미지가 생략되어 있습니다. 더 자세한 내용은 하단 [학습 정리 자료]의 네이버 블로그 원본 링크를 참고해주세요.

## [참여 이유]

평소에 자동화에 관심도 있었다. 관심이 있기에 내가 주력으로 사용하면 python으로 많은 자동화(크롤링, 글쓰기 등등) 프로그램을 만들었었다.

기술이 발전함에 있어서 n8n, make 등 자동화 tool 이 생겨났고 관심은 많아 공부해야지 해야지 하다가 계속 미루게 되었다.

이때 마침, 메타코드에서 n8n에 대해서 스터디를 하는 프로그램이 있길래 everyai 1기로 참여를 하게 되었습니다.

다 같이, 함께 공부하면 나도 동기부여가 될 뿐더러 어느정도의 해야한다 라는 생각이 들기 때문입니다.

<br>

## [학습 내용]

1주차이기에 n8n 에 대해서 회원가입부터 간단한 n8n 자동화 만들기를 진행했다.

- n8n workflow는 무조건 **"Trigger node"**로 시작이 된다.
  - Trigger node란?
    - 어떤 이벤트가 발생했을 때 이 workflow를 작동시킨다는 시작 node이다.
    - ex) 메일이 왔을 때 / 텔레그램 메시지를 받았을때 / 정해놓은 시간이 되었을 때

- Credential(자격 증명) : 외부서비스와의 연결을 위한 열쇠
  - n8n에서 워크플로우를 만들 때, 외부서비스를 접근하도록 해야한다(Gmail, OpenAI, telegram 등)
  - 이때 외부서비스를 이용하기 위해서는 나도 외부서비스를 접근해야하지만, 역으로 외부서비스도 내 계정에 접근을 해야함.
  - 따라서, 외부서비스와 나와 연결을 위한 열쇠가 필요하다!
  - 이걸 자격증명 credential 이라고 함

- 대표적인 Credential 예시:
  - API Key, oAuth, 비밀번호(Password), SSH Key (서버 접속용 키), 디지털 인증서 (Certificate)

이에 따라서 **"Google cloud API Key"**와 **"oAuth"**를 발급 받았다.

- **API 키 :** **Gemini, 번역, 지도** 등 구글의 기능(서비스)을 가져다 쓸 때 "나 이 프로젝트야, 돈(또는 쿼터)은 내 프로젝트 앞으로 달아놔"라고 신원을 증명하는 용도.
- **OAuth 2.0 :** **Gmail**처럼 "내 개인 계정에 로그인해서 메일 보내기" 같은 **권한**이 필요할 때 쓴다.

| ![Google cloud API Key]({{site.url}}/images/etc/n8n/2025-11-22-metacode-n8n-week1/image1.png) | ![oAuth 클라이언트]({{site.url}}/images/etc/n8n/2025-11-22-metacode-n8n-week1/image2.png) |
|:--:|:--:|
| *(좌) Google cloud API Key* | *(우) oAuth 클라이언트* |

<br>

## [실습 따라하기]

위에는 실습에 필요한 Credential을 발급 받았으니, 이제는 이를 활용해서 직접 n8n workflow를 따라 만들어 보았다.

![workflow 첫 화면]({{site.url}}/images/etc/n8n/2025-11-22-metacode-n8n-week1/image_27.png){: .align-center}
*workflow 첫 화면*
{: .text-center}

드디어 영상, 이미지로만 봤던 n8n을 만드는 화면이 나왔다... 두근두근

이미지의 상단에 (1)을 눌러서 이름을 "everyai n8n practice_1" 로 변경해줬다.

또한, 위에서 학습했듯이 (2)번을 눌러서 Trigger node를 생성했다.

추가적으로 Gemini를 연결하기위해 아까 만든 **Google cloud API Key**를 사용했다.

![Ai Agent node에서 Gemini를 붙였다]({{site.url}}/images/etc/n8n/2025-11-22-metacode-n8n-week1/image3.png){: .align-center}
*Ai Agent node에서 Gemini를 붙였다.*
{: .text-center}

이러한 LLM 모델을 사용할때는 프롬프트가 있어야 출력이 된다.

AI Agent를 더블클릭한 후, (1)번에 프롬프트를 입력 -> (2)번을 보면 왼쪽 INPUT에는 사용할 수 있는 데이터가 있다. 이를 프롬프트쪽으로 드래그를 하면 저 데이터를 프롬프트에 활용할 수 있다.

![프롬프트 입력]({{site.url}}/images/etc/n8n/2025-11-22-metacode-n8n-week1/image4.png){: .align-center}
*프롬프트 입력*
{: .text-center}

만약 이게 어떻게 출력하는지 확인하고 싶으면 (1)번 Execute step을 누르면 Gemini가 프롬프트를 읽고 (2)번 Ouput을 보여준다.

이를 통해서 내 프롬프트가 잘 들어갔는지 중간점검을 하면서 프롬프트를 수정하면 될 것 같다.

![프롬프트에 대한 output 확인하기]({{site.url}}/images/etc/n8n/2025-11-22-metacode-n8n-week1/image5.png){: .align-center}
*프롬프트에 대한 output 확인하기*
{: .text-center}

여기까지 완료했으면 마지막으로 메일보내는 작업을 진행한다.

여기서 메일을 보내는 작업이므로 아까 발급받은 oAuth 클라이언트 ID와 PW를 사용해야한다.

마지막 노드로 **Google Gmail Send a Message**를 삽입하고, 누구한테 보낼지, 메일 제목/내용에 대한 설정을 하면 메시지가 자동으로 보내진다.

<br>

## [과제]

이번 과제는
1. 내가 소식을 받아보고 싶은 사이트 최소 3개 이상 고르기
2. on Form Submission, AI agnet 노드를 이용해서 워크플로우 구성하기

이렇게 해서 메일을 보내면 아래와 같이 보내진다.

추가적으로, 메일을 다수에게 보내려면 To 항목에 "A@gmail.com, B@gmail.com" 과 같이 쉼표로 구분을 하면 다수에게도 보낼 수 있다.

{% include video id="EQulQiMnWaA" provider="youtube" %}

<br>

## [과제를 하면서 느낀점]

- 처음에는 모든 노드들을 다 만들고나서 각 노드별 세팅을 진행하려했는데 계속 오류가 나더라
  - Trigger만 실행했는데도 오류나고, Trigger와 다음 노드 연결을 끊고 했는데도 오류났다.
  - 그 후, Trigger 만 냅두고 모든 노드를 지우니까 잘 됨.
  - 따라서, 노드를 하나 추가 -> 해당 노드 세팅 -> 다음 노드 생성 이런식으로 해야겠다.

- 저장은 수시로,,,,

- 세팅 하나하나가 엄청나게 다른 결과를 만들어낸다. 모르면 ai에게 물어보면서 하라.
  - 결과를 하나를 만들어야하는데 자꾸 3개가 나와서 골머리를 떄렷음
  - -> ai에게 물어보니 바로 해결됨.

<br>

## [학습 정리 자료]

- 본문 링크 : [네이버 블로그 원본](https://blog.naver.com/s980903/224084134716)
- [하면서 났던 오류들 수정한 내용](https://www.notion.so/seonghow/TIP-2b219e902f3c8033ba06facc5069d978) - 지속 누적할 예정
