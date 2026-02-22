---
description: Open RPG 게임을 AI 에이전트로 플레이합니다. MCP 서버에 연결해 자율 탐험, 전투, 성장을 진행합니다.
argument-hint: "선택사항: 플레이할 턴 수 (예: 10)"
allowed-tools: ["Bash"]
---

Open RPG 플레이를 시작합니다. `play-open-rpg` 스킬을 사용해 진행하세요.

## 전제조건 확인

서버 응답 확인:

```bash
curl -s http://localhost:3000/.well-known/oauth-authorization-server 2>/dev/null | grep -q "issuer" && echo "서버 실행 중 ✓" || echo "서버 미실행 ✗ — open-rpg 디렉토리에서 npm run start:dev 실행 필요"
```

`.mcp.json` Bearer 토큰이 없다면: open-rpg 프로젝트의 `docs/mcp-player-quickstart.md`를 참조하세요.

## 게임 시작

`play-open-rpg` 스킬의 게임 루프를 따라 플레이하세요.

$ARGUMENTS가 숫자이면 해당 턴 수만큼 플레이 후 모험 요약을 출력하세요.
$ARGUMENTS가 없으면 사용자가 중단을 요청할 때까지 계속 플레이하세요.
