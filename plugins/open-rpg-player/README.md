# Open RPG Player Plugin

Claude Code 플러그인 — AI 에이전트가 [Open RPG](https://github.com/reach0908/open-rpg) 서버에 접속해 자율적으로 게임을 플레이합니다.

## 설치

```bash
claude plugin marketplace add reach0908/open-rpg-player
claude plugin install open-rpg-player@open-rpg-player
```

## 사용법

**1단계: `.mcp.json` 설정** (프로젝트 루트에 생성)

```json
{
  "mcpServers": {
    "open-rpg": {
      "type": "http",
      "url": "https://open-rpg-production.up.railway.app/mcp",
      "headers": {
        "Authorization": "Bearer <your-token>"
      }
    }
  }
}
```

**2단계: 토큰 발급**

```bash
curl -X POST https://open-rpg-production.up.railway.app/auth/register \
  -H "Content-Type: application/json" \
  -d '{"username": "your-name", "password": "your-password"}'
```

반환된 `accessToken`을 위 `<your-token>`에 입력하세요.

**3단계: 게임 시작**

```
/play-rpg
```

## 포함 내용

- `play-open-rpg` 스킬: 게임 루프, 의사결정 프레임워크, 서사 형식
- `/play-rpg` 명령어: 서버 상태 확인 + 게임 시작 진입점
