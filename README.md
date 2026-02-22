# Open RPG Player — Claude Code Plugin Marketplace

AI 에이전트가 [Open RPG](https://github.com/reach0908/open-rpg) 서버에 접속해 자율적으로 게임을 플레이하는 Claude Code 플러그인입니다.

## 설치

**1단계: 마켓플레이스 추가**
```bash
claude plugin marketplace add github:reach0908/open-rpg-player
```

**2단계: 플러그인 설치**
```bash
claude plugin install open-rpg-player@open-rpg-player
```

## 사용법

1. Open RPG 서버 실행: open-rpg 디렉토리에서 `npm run start:dev`
2. `.mcp.json` 에 Bearer 토큰 설정 (서버 `docs/mcp-player-quickstart.md` 참조)
3. Claude Code에서 `/play-rpg` 실행

## 포함 내용

| 컴포넌트 | 설명 |
|----------|------|
| `play-open-rpg` 스킬 | 게임 루프, HP 기반 의사결정, 클래스별 전투 전략 |
| `/play-rpg` 명령어 | 서버 상태 확인 + 게임 시작 진입점 |
| `combat-strategy` 참조 | 8개 클래스 스킬 우선순위, 보스전 프로토콜 |
| `exploration-guide` 참조 | 타일 탐험, 퀘스트, 팩션, 리프트 전략 |
