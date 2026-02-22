# Open RPG Player Plugin

Claude Code 플러그인 — AI 에이전트가 [Open RPG](https://github.com/your-org/open-rpg) 서버에 접속해 자율적으로 게임을 플레이합니다.

## 설치

```bash
claude plugin install ./open-rpg-player
```

## 사용법

1. Open RPG 서버 실행: open-rpg 디렉토리에서 `npm run start:dev`
2. `.mcp.json` 설정: `docs/mcp-player-quickstart.md` 참조
3. `/play-rpg` 명령어로 게임 시작

## 포함 내용

- `play-open-rpg` 스킬: 게임 루프, 의사결정 프레임워크, 서사 형식
- `/play-rpg` 명령어: 빠른 시작 진입점
