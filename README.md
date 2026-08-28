# devlog 스킬

개발 과정을 개인 기록 레포(`dev-journal`)에 **일관된 형식으로** 남기게 하는 Claude Code 개인 스킬.

세션이 끊길 때마다 문서 형식을 다시 설명하는 품을 없애려고 만들었다.
스킬은 **절차**만 갖고, **형식 명세는 각 프로젝트 폴더의 README에 있다** — 프로젝트마다 형식이 달라도 되고,
형식을 고칠 때 한 곳만 고치면 된다.

```
dev-journal/projects/<프로젝트>/
  README.md              ← 공통 규칙 (형식 명세)
  adr/README.md          ← 섹션 형식
  infra/ backend/ troubleshooting/ review/ ...
```

## 설치

```powershell
# pwsh
git clone https://github.com/1Irving1/devlog-skill.git "$HOME\Desktop\devlog-skill"
New-Item -ItemType Junction -Path "$HOME\.claude\skills\devlog" `
  -Target "$HOME\Desktop\devlog-skill\devlog"
```

```bash
# bash (macOS · Linux)
git clone https://github.com/1Irving1/devlog-skill.git ~/Desktop/devlog-skill
ln -s ~/Desktop/devlog-skill/devlog ~/.claude/skills/devlog
```

사본을 만들지 않고 링크한다 — 스킬을 고치면 이 레포에서 그대로 커밋한다.
Claude Code 재시작 후 `/devlog`가 뜨면 끝.

기록을 남길 `dev-journal` 레포는 별도로 클론해 둔다 (기본 위치 `~/Desktop/dev-journal`).

## 쓰는 법

"이거 ADR로 박아줘" / "트러블슈팅으로 정리해줘" / "이 코드 읽은 거 남겨줘" 정도로 부른다.
스킬이 프로젝트 폴더를 찾고, 카테고리를 고르고, 그 프로젝트의 형식 README를 읽고,
**나만 아는 것(계기·당시 판단·소요 시간·남은 의문)을 먼저 물은 뒤** 쓴다.

## 참고

첫 적용 사례와 이 체계를 만든 결정 기록:
`dev-journal/projects/PenguinMilk/adr/0001-personal-devlog-system.md`
