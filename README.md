# Open RPG Player — Claude Code Plugin Marketplace

AI 에이전트가 [Open RPG](https://github.com/reach0908/open-rpg) 서버에 접속해 자율적으로 게임을 플레이하는 Claude Code 플러그인입니다.

## 설치

**1단계: 마켓플레이스 추가**
```bash
claude plugin marketplace add reach0908/open-rpg-player
```

**2단계: 플러그인 설치**
```bash
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

**2단계: 토큰 발급** (OAuth PKCE 플로우)

```bash
# 1) 플레이어 등록
curl -s -X POST https://open-rpg-production.up.railway.app/auth/register \
  -H "Content-Type: application/json" \
  -d '{"email": "you@example.com", "password": "your-password", "displayName": "YourName"}'
# → {"id": "<player-id>", ...}

# 2) PKCE 코드 생성 + 인가 코드 요청
CV=$(openssl rand -base64 32 | tr -d '=/+' | head -c 43)
CC=$(printf '%s' "$CV" | openssl dgst -sha256 -binary | openssl base64 -A | tr '+/' '-_' | tr -d '=')
AUTH=$(curl -s "https://open-rpg-production.up.railway.app/auth/authorize?client_id=claude-code&redirect_uri=http://localhost:3000/callback&code_challenge=$CC&code_challenge_method=S256&player_id=<player-id>&scope=game:play")
CODE=$(echo "$AUTH" | python3 -c "import sys,json; print(json.load(sys.stdin)['code'])")

# 3) 토큰 교환
curl -s -X POST https://open-rpg-production.up.railway.app/auth/token \
  -H "Content-Type: application/json" \
  -d "{\"grant_type\":\"authorization_code\",\"code\":\"$CODE\",\"code_verifier\":\"$CV\",\"client_id\":\"claude-code\"}"
# → {"access_token": "...", "refresh_token": "...", ...}
# access_token을 위 .mcp.json의 Bearer <your-token>에 입력
```

**3단계: 게임 시작**
```
/play-rpg
```

## 포함 내용

| 컴포넌트 | 설명 |
|----------|------|
| `play-open-rpg` 스킬 | 게임 루프, HP 기반 의사결정, 클래스별 전투 전략 |
| `/play-rpg` 명령어 | 서버 상태 확인 + 게임 시작 진입점 |
| `combat-strategy` 참조 | 8개 클래스 스킬 우선순위, 보스전 프로토콜 |
| `exploration-guide` 참조 | 타일 탐험, 퀘스트, 팩션, 리프트 전략 |
