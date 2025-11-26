---
title: "[project] 바이브 코딩으로 만든 디스코드 학습 트래커 봇 개발기"
excerpt: "AI 도구와 협업하는 바이브 코딩으로 디스코드 학습 시간 추적 봇을 개발한 과정과 노하우를 공유합니다."
layout: single
categories:
  - project
tags:
  - vibecoding
  - discord_bot
  - python
author_profile: false
sidebar:
  nav: "docs"
search: true
toc: true
toc_sticky: true
toc_label: 목차
date: 2025-11-11 00:00:00 +0900
---

# 바이브 코딩으로 만든 디스코드 학습 트래커 봇 개발기

## 🚀 들어가며

최근 몇 달간 디스코드 공부 서버인 "마법사관학교"를 위한 학습 트래커 봇을 개발했다. 이 프로젝트는 처음부터 끝까지 **바이브 코딩(Vibe Coding)** 방식으로 진행했는데, AI 도구들을 적극 활용하여 기획부터 배포까지 완성할 수 있었다.

바이브 코딩이란 AI 도구와 협업하며 코드를 작성하는 방식을 말한다. 전통적인 방식처럼 모든 코드를 직접 타이핑하는 대신, AI에게 의도를 전달하고 생성된 코드를 검토·수정하며 개발을 진행한다. 이번 프로젝트를 통해 바이브 코딩의 가능성과 한계를 모두 경험할 수 있었다.

## 📋 프로젝트 소개

**마법사관학교 학습 트래커 봇**은 디스코드 음성 채널에서의 학습 시간을 자동으로 추적하고, 게임처럼 재미있는 레벨 시스템과 시각적 보상으로 학습 동기를 높여주는 봇이다.

### 주요 기능

- **🎴 학생증 프로필 카드**: 개인화된 학생증에 학습 통계, 레벨, 기숙사 정보 표시
- **🌱 연간 잔디 캘린더**: GitHub 스타일 히트맵으로 1년간의 학습 활동 시각화
- **🏆 레벨 시스템**: 1시간 = 1XP, 10단계 레벨 시스템으로 성장 추적
- **🏫 기숙사 시스템**: 해리포터 컨셉의 4개 기숙사 (소용돌이, 펭도리야, 노블레빗, 볼리베어)

### 기술 스택

- **Backend**: Python 3.11+ / discord.py
- **Database**: PostgreSQL (Supabase)
- **Image Generation**: Pillow (PIL)
- **Dashboard**: Next.js + TypeScript
- **Infrastructure**: Vultr VPS (Ubuntu)

## 🤔 바이브 코딩, 어떻게 시작했나?

### 💭 고민의 시작

프로젝트를 시작하기 전, 가장 큰 고민은 "AI 도구를 어떻게 효과적으로 활용할 것인가?"였다. 단순히 코드 자동완성 수준이 아니라, 기획부터 아키텍처 설계, 구현, 디버깅까지 전 과정에서 AI를 파트너로 삼고 싶었다.

그래서 다음과 같은 전략을 세웠다:

1. **기획 단계**: 명확한 문서화로 AI가 이해할 수 있는 컨텍스트 구축
2. **설계 단계**: AI와 대화하며 아키텍처 결정, 트레이드오프 논의
3. **구현 단계**: AI가 생성한 코드를 베이스로, 직접 수정·개선
4. **디버깅 단계**: AI에게 에러 로그를 보여주고 해결 방법 탐색

### 🛠️ 사용한 AI 도구들

#### 📝 기획 단계
- **Google AI Studio**: PRD(Product Requirements Document) 작성 시 아이디어 브레인스토밍
- **ChatGPT**: 사용자 시나리오 구체화, 기능 우선순위 결정

#### 💻 코딩 단계
- **Codex**: 코드 생성과 자동완성
- **Cursor (Claude 4.5)**: 복잡한 로직 구현, 리팩토링
- **Cursor (GPT-5 High)**: 빠른 프로토타이핑, 간단한 함수 작성


## 💡 바이브 코딩 실전 적용기

### 1️⃣ 기획: AI와 함께 PRD 작성하기

처음엔 막연히 "학습 시간을 추적하는 봇"이라는 아이디어만 있었다. Google AI Studio에 다음과 같이 질문했다:

> "학습 시간을 추적하는 봇을 활용해서 디스코드 공부 서버에서 멤버들의 학습 동기를 높이려면 어떤 기능이 필요할까?"

AI는 게이미피케이션, 시각화, 소셜 비교 등 다양한 아이디어를 제시했다. 이를 바탕으로 GPT-4와 대화하며 구체적인 기능 목록을 만들었다:

- 음성 채널 입장 시 자동 시간 기록
- 레벨/XP 시스템으로 성장 시각화
- 프로필 카드로 개인 통계 표시
- 잔디 캘린더로 꾸준함 추적

이 과정에서 ChatGPT는 내가 놓친 부분들을 짚어줬다. 예를 들어 "서버장이 멤버 활동을 관리하려면 어떤 기능이 필요한가?"라는 질문에, 기숙사장 권한으로 다른 사용자 프로필 조회 기능을 제안받았다.

### 2️⃣ 설계: 아키텍처 결정 과정

TRD(Technical Requirements Document) 작성 시, Google AI Studio와 ChatGPT에게 다음과 같이 요청했다:

> "Python discord.py 봇을 만들려고 해. 음성 채널 입장/퇴장을 추적하고, PostgreSQL에 저장하고, Pillow로 이미지를 생성해야 해. 최적의 아키텍처를 제안해줘."

두 LLM들의 내용을 종합해보면 단순한 모놀리식 구조를 제안하면서, 다음과 같은 이유를 설명했다:

- **ORM 대신 asyncpg 직접 사용**: 간단한 쿼리에 SQLAlchemy는 오버엔지니어링
- **FastAPI 제외**: 웹 대시보드는 Phase 2, MVP에선 불필요
- **systemd로 프로세스 관리**: 간단하고 안정적

이런 조언들이 프로젝트 복잡도를 크게 낮춰줬다. AI가 제안한 이유를 검토하고, 내 상황에 맞는지 판단하는 과정이 중요했다.

### 3️⃣ 구현: 핵심 로직 작성

가장 까다로웠던 부분은 **학생증 이미지 생성** 로직이었다. Pillow로 복잡한 레이아웃을 그려야 했는데, 다음과 같이 요청했다:

> "Pillow로 학생증 카드를 만들어줘. 배경색은 기숙사별로 다르고, 프로필 이미지는 원형으로 자르고, 레벨 진행 바는 그라데이션으로 표현해야 해."

Cursor(claude-sonnet 4.5)가 생성한 초기 코드는 작동했지만, 몇 가지 문제가 있었다:

- 이모지 렌더링 시 깨짐
- 긴 닉네임이 카드 밖으로 넘침
- 색상 대비가 낮아 가독성 떨어짐

이런 문제들을 AI에게 하나씩 피드백하며 수정했다. 예를 들어:

```python
def _strip_symbols_emojis(text: str) -> str:
    """Remove emoji/symbol-like characters to avoid rendering issues."""
    out_chars: list[str] = []
    for ch in text:
        cp = ord(ch)
        # Remove emoji ranges
        if 0x1F000 <= cp <= 0x1FAFF or 0x2600 <= cp <= 0x27BF:
            continue
        # Remove symbol categories
        if unicodedata.category(ch).startswith('S'):
            continue
        out_chars.append(ch)
    return ''.join(out_chars).strip()
```

이 함수는 AI가 제안한 것인데, 이모지를 안전하게 제거하는 로직이 깔끔했다.  
직접 구현했다면 훨씬 오래 걸렸을 것이다.

### 4️⃣ 디버깅: AI와 함께 버그 해결

음성 채널 추적 로직에서 이상한 버그가 있었다. 사용자가 채널을 이동할 때 세션이 제대로 종료되지 않는 문제였다.

에러 로그와 관련 코드를 Cursor에 붙여넣고 물어봤다:

> "이 코드에서 사용자가 채널 A에서 B로 이동할 때 세션이 두 번 기록돼. 이러한 일이 발생하지 않게 수정하고 왜 그랬는지 설명하라. 또한, 다시는 이러한 일이 반복되지 않게 cursor rule에 추가하라."

Claude는 `on_voice_state_update` 이벤트가 채널 이동 시 한 번만 발생하는데, `before.channel`과 `after.channel`을 모두 체크해야 한다고 설명했다. 그리고 수정된 로직을 제시했다:

```python
async def on_voice_state_update(member, before, after):
    # 채널 이동 감지
    if before.channel != after.channel:
        # 이전 채널에서 퇴장 처리
        if before.channel:
            await end_session(member.id, before.channel.id)
        # 새 채널에 입장 처리
        if after.channel:
            await start_session(member.id, after.channel.id)
```

이런 식으로 AI에게 버그를 설명하고 해결책을 받는 과정이 매우 효율적이었다.  
명령에서도 보았듯이 같은 일이 반복되지 않게 rule에 추가하여서 문제의 재발생을 막았다.

## ⚖️ 바이브 코딩의 장단점

### ✅ 장점

1. **개발 속도 향상**: 반복적인 코드, 보일러플레이트를 빠르게 생성
2. **학습 가속화**: AI가 제안한 코드를 읽으며 새로운 패턴 학습
3. **문서화 자동화**: 주석, README, 타입 힌트를 AI가 작성
4. **아이디어 확장**: 혼자 생각하지 못한 기능이나 접근법 발견

### ⚠️ 단점 (그리고 극복 방법)

1. **맥락 이해 부족**: AI는 프로젝트 전체 구조를 완벽히 파악하지 못함
   - **해결**: 명확한 문서(PRD, TRD 등)로 컨텍스트 제공

2. **잘못된 코드 생성**: 때로는 작동하지 않거나 비효율적인 코드 제안
   - **해결**: 생성된 코드를 항상 검토하고 테스트

3. **의존성 증가**: AI 없이는 개발 속도가 느려질 수 있음
   - **해결**: AI가 생성한 코드를 이해하고 내 것으로 만들기

4. **창의성 저하 우려**: AI 제안에만 의존하면 독창적 사고 감소
   - **해결**: 중요한 설계 결정은 직접 고민 후 AI에게 검증 요청

## 💎 바이브 코딩을 위한 팁

이번 프로젝트를 통해 배운 바이브 코딩 노하우를 공유한다:

### 1️⃣ 명확한 요청이 핵심

❌ 나쁜 예:
> "프로필 기능 만들어줘"

✅ 좋은 예:
> "discord.py 슬래시 커맨드로 `/학생증` 명령어를 만들어줘. 사용자의 학습 시간, 레벨, XP를 DB에서 조회하고, Pillow로 800x600 이미지를 생성해서 디스코드에 전송해야 해."

### 2️⃣ 단계별로 진행

복잡한 기능은 한 번에 요청하지 말고, 작은 단위로 쪼개서 진행한다:

1. 먼저 텍스트 기반 프로필 출력
2. 그 다음 간단한 이미지 생성
3. 마지막으로 복잡한 레이아웃 추가

### 3️⃣ AI 도구별 강점 활용

- **Google AI Studio / ChatGPT**: 기획, 문서 작성, 아이디어 브레인스토밍
- **Codex**: 기본적인 코드 생성, 함수 작성
- **Cursor (Claude 4.5)**: 복잡한 로직, 리팩토링, 아키텍처 설계
- **Cursor (GPT-5 High)**: 빠른 프로토타이핑, 간단한 유틸리티 함수

### 4️⃣ 항상 검증하기

AI가 생성한 코드는 반드시:
- 직접 읽고 이해하기
- 테스트 코드 작성하기
- 엣지 케이스 확인하기

### 5️⃣ 문서화로 컨텍스트 유지

프로젝트가 커질수록 AI가 전체 맥락을 파악하기 어려워진다. `vooster-docs/` 폴더에 PRD, TRD, 아키텍처 문서를 정리해두고, AI에게 참고하도록 했다.

## ✨ 인상 깊었던 순간들

### 📅 1. 잔디 캘린더 알고리즘

GitHub 스타일 잔디 캘린더를 구현할 때, 날짜 계산과 그리드 레이아웃이 복잡했다. Claude에게 요청하자 한 번에 작동하는 코드를 생성했다:

```python
def generate_grass_calendar(user_data: dict, year: int) -> Image:
    # 연도의 첫날과 마지막날 계산
    start_date = datetime(year, 1, 1)
    end_date = datetime(year, 12, 31)
    
    # 주 단위로 그리드 생성
    weeks = []
    current = start_date
    while current <= end_date:
        week = []
        for _ in range(7):
            if current <= end_date:
                week.append(current)
            current += timedelta(days=1)
        weeks.append(week)
    
    # Pillow로 그리드 렌더링
    # ...
```

날짜 계산 로직을 직접 구현했다면 오프바이원 에러로 고생했을 텐데, AI 덕분에 한 번에 해결했다.

### 🎨 2. 기숙사별 테마 색상 시스템

각 기숙사마다 고유한 색상 테마를 적용하려고 했다. 단순히 색상만 바꾸는 게 아니라, 배경색에 따라 텍스트 색상을 자동으로 조정해야 했다.

Claude가 제안한 상대 휘도(Relative Luminance) 계산 함수가 인상적이었다:

```python
def _relative_luminance(color: tuple[int, int, int]) -> float:
    def channel(v: int) -> float:
        x = v / 255.0
        return x / 12.92 if x <= 0.03928 else ((x + 0.055) / 1.055) ** 2.4
    
    r, g, b = (channel(v) for v in color)
    return 0.2126 * r + 0.7152 * g + 0.0722 * b
```

WCAG 접근성 기준을 자동으로 고려하는 코드였다. 이런 세심한 부분까지 AI가 챙겨준 게 놀라웠다.

### 🛡️ 3. 에러 핸들링의 중요성

초기에는 AI가 생성한 코드에 에러 핸들링이 부족했다. 예를 들어 DB 연결 실패, 이미지 로딩 실패 등의 예외 상황을 고려하지 않았다.

이를 AI에게 피드백하자, 다음과 같은 개선된 코드를 제시했다:

```python
async def fetch_user_profile(user_id: int) -> Optional[dict]:
    try:
        async with db_pool.acquire() as conn:
            row = await conn.fetchrow(
                "SELECT * FROM users WHERE user_id = $1",
                user_id
            )
            return dict(row) if row else None
    except asyncpg.PostgresError as e:
        logger.error(f"DB error fetching user {user_id}: {e}")
        return None
    except Exception as e:
        logger.error(f"Unexpected error: {e}")
        return None
```

이 경험을 통해, AI에게 "에러 핸들링을 추가해줘"라고 명시적으로 요청하는 게 중요하다는 걸 배웠다.

## 📊 실제 성과

이 봇을 마법사관학교 서버에 배포한 지 몇 주가 지났다. 결과는 기대 이상이었다:

- **멤버 참여율 약 10% 증가**: 학생증과 잔디를 보기 위해 더 자주 접속
- **평균 학습 시간 증가**: 레벨업을 위해 더 오래 공부
- **서버장 업무 시간 절감**: 자동 기록으로 수기 관리 불필요

무엇보다 멤버들의 반응이 좋았다. "내 학생증 예쁘다", "잔디 채우는 재미가 있다"는 피드백을 받을 때마다 뿌듯했다.

## 🎓 배운 점과 앞으로

### 🔍 바이브 코딩은 만능이 아니다

AI는 강력한 도구지만, 다음은 여전히 개발자의 몫이다:

- **핵심 아이디어**: 무엇을 만들지 결정하는 건 사람
- **사용자 공감**: 실제 사용자가 원하는 게 뭔지 파악
- **품질 검증**: 생성된 코드가 정말 좋은 코드인지 판단
- **윤리적 결정**: 데이터를 어떻게 다룰지, 어떤 기능을 넣을지

### 🚀 앞으로의 계획

Phase 2로 다음 기능들을 추가할 예정이다:

- **관리자 웹 대시보드**: Next.js로 통계 시각화
- **AI 학습 분석 리포트**: 학습 패턴 분석 및 개선 제안
- **자동 역할 부여**: 학습 시간에 따라 서버 역할 자동 지급

이것들도 역시 바이브 코딩으로 진행할 것이다. 이번 경험으로 AI와 협업하는 방법을 많이 배웠기 때문에, 다음 단계는 더 빠르고 효율적으로 진행할 수 있을 것 같다.

## 🎯 마치며

바이브 코딩은 개발 방식의 패러다임 전환이다. 모든 코드를 직접 타이핑하는 시대는 지나가고 있다. 대신 우리는 AI와 대화하며, 의도를 전달하고, 결과를 검증하는 역할로 변화하고 있다.

하지만 이게 개발자의 가치를 떨어뜨리는 건 아니다. 오히려 더 높은 수준의 사고를 요구한다:

- 문제를 명확히 정의하는 능력
- AI가 생성한 코드를 평가하는 안목
- 전체 시스템을 설계하는 아키텍처 감각
- 사용자 경험을 고민하는 공감 능력

이번 프로젝트를 통해 바이브 코딩의 가능성을 확인했다. 혼자서도 풀스택 봇을 만들고, 배포하고, 운영할 수 있었다. AI 도구들이 없었다면 몇 배는 더 오래 걸렸을 것이다.

앞으로도 AI와 협업하며 더 재미있는 프로젝트들을 만들어갈 예정이다.  
생각보다 훨씬 재미있고, 배울 게 많다.

---

**GitHub**: [https://github.com/Pakkoc/studycard-discord-bot](https://github.com/Pakkoc/studycard-discord-bot)  
**사용한 AI 도구**:
- 기획: Google AI Studio, ChatGPT
- 코딩: Codex, Cursor (Claude 4.5, GPT-5 High)

**기술 스택**: Python, discord.py, PostgreSQL, Pillow, Next.js, TypeScript

