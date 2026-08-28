# penguin-devlog

S15P21E103(펭귄밀크) 개발 과정 개인 기록. 프로젝트 레포와 분리되어 있고 커밋 대상이 아니다.
블로그·자소서에서 그대로 꺼내 쓸 수 있는 단위로 쓴다.

| 폴더 | 무엇을 남기나 | 핵심 질문 |
|---|---|---|
| [`adr/`](adr/) | 설계·운영 **결정** | 왜 이 선택인가 |
| [`infra/`](infra/) | 인프라 구축·운영 **작업** | 어떻게 세웠고 어떻게 재현하나 |
| [`backend/`](backend/) | 백엔드 **구현** | 무엇을 어떻게 만들었나 |
| [`troubleshooting/`](troubleshooting/) | 장애·삽질 **추적** | 왜 깨졌고 어떻게 좁혔나 |
| [`review/`](review/) | 코드 **이해** | 이 코드는 어떤 순서로 도는가 |

## 공통 규칙

모든 폴더에 적용된다. 폴더별 README는 이 규칙 위에 형식만 얹는다.

### 문서 머리

모든 문서는 frontmatter로 시작한다. 참조는 본문에 흩뿌리지 않고 여기 모은다.

```yaml
---
date: 2026-08-28            # 기록일
tags: [kafka, infra]
related:                     # ADR · 팀 문서 · MR · 커밋. 없으면 []
  - ADR-0003
  - "팀 ADR-0001"
  - "Cushion arch/infra.md §3"
  - "MR !12"
  - "commit 3d9cbc1"
---
```

### 문체

**1인칭 과거형 서술.** "나는 ~했다", "~를 확인했다". 문서마다 인칭·시제가 흔들리면 인용할 때 전부 고쳐 써야 한다.
현재형은 형식·규칙을 설명할 때만("이 설정은 ~를 한다").

### 내용

- **한 파일 = 한 주제.** 두 주제가 섞이면 파일을 쪼갠다. 스크롤 두 번을 넘기면 주제가 둘인지 의심한다
- **그때 쓴다.** 사후에 몰아 쓴 기록은 결과를 알고 쓴 각색이 된다. 늦게 썼으면 늦게 썼다고 적는다
- **실물을 붙인다.** 명령·로그·코드·에러 메시지는 요약하지 말고 원문으로. 출처(`파일:라인`, 커밋 SHA, 컨테이너명)를 함께 적는다
- **셸을 표기한다.** 이 PC는 PowerShell · Git Bash · WSL이 섞여 있다. 코드 블록 첫 줄에 `# pwsh` / `# bash` 주석
- **설정 파일은 변경 부분만.** 전체는 커밋 SHA로 가리킨다
- **실패를 지우지 않는다.** 틀린 가설, 몰랐던 문법, 되돌린 조치가 기록의 값어치다
- **모르는 건 모른다고 쓴다.** 각 문서 끝의 "남은 의문"을 빈 채로 두지 않는다 — 없으면 `없음`
- **결정이 튀어나오면 `adr/`로 뺀다.** 다른 폴더에서는 `ADR-NNNN`으로 링크만 건다
- 팀 문서는 Cushion `penguin-milk/`에 있다. 참조 시 `팀 ADR-NNNN` / `Cushion arch/infra.md §4` 꼴로 경로를 적는다
- 비밀값(토큰·비밀번호·키)은 `<REDACTED>`로 치환하고 붙인다

### 갱신

새로 만들기 전에 **같은 주제 파일이 이미 있는지 본다.** 있으면 갱신한다:
- `review/` — 같은 주제면 질문을 덧붙인다
- `troubleshooting/` — 원인 `미확정` → 확정되면 그 문서를 고친다
- `adr/` — 번복되면 최종 형태로 갱신, 배울 점이면 새 ADR + 이전 ADR에 `대체됨`

### 인덱스

각 폴더 README의 `## 인덱스`에 한 줄. 형식 고정:

```
- [제목](파일명.md) — 한 줄 요약 (YYYY-MM-DD)
```

## 다른 PC에서 설치

이 레포 하나에 기록과 스킬이 같이 있다. 스킬(`skill/devlog/`)은 `~/.claude/skills/devlog`에 **정션**으로 연결해 사본을 두지 않는다.

```powershell
# pwsh
git clone https://github.com/1Irving1/penguin-devlog.git "$HOME\Desktop\penguin-devlog"
New-Item -ItemType Junction -Path "$HOME\.claude\skills\devlog" -Target "$HOME\Desktop\penguin-devlog\skill\devlog"
```

```bash
# bash (macOS · Linux)
git clone https://github.com/1Irving1/penguin-devlog.git ~/Desktop/penguin-devlog
ln -s ~/Desktop/penguin-devlog/skill/devlog ~/.claude/skills/devlog
```

경로를 `~/Desktop/penguin-devlog`에서 바꾸면 `skill/devlog/SKILL.md`의 경로도 함께 바꾼다.
Claude Code 재시작 후 `/devlog`가 뜨면 끝.
