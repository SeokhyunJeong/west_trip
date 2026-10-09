# 미국 서부 공동 여행 일정

공개 주소: https://seokhyunjeong.github.io/west_trip/

GitHub Pages가 화면을 제공하고, Supabase 프로젝트 west-trip이 공용 일정과 최근 10개 변경 이력을 저장합니다. 누구나 로그인 없이 같은 일정을 수정·저장하며, 다른 사람의 변경은 최대 15초 간격으로 확인합니다. 동시 수정 충돌이 나면 다른 사람의 계획을 덮어쓰지 않고 현재 편집을 화면에 남깁니다. JSON으로 백업한 뒤 공용 최신 일정을 불러올 수 있습니다.

제공한 원본 JSON의 2026-10-30~2026-11-08, 10일·22개 일정을 그대로 초기 데이터로 사용했습니다. 재배포해도 서버의 저장된 계획을 초기화하지 않습니다.

## 파일과 배포

- index.html: 공개 페이지. GitHub 저장소 main 브랜치 루트에 올립니다.
- .nojekyll: GitHub Pages 정적 파일 처리용입니다.
- Supabase 함수 west-trip: JWT 검증이 활성화되어 있으며, 공개 anon 키만 프런트엔드에서 사용합니다. 관리자 키는 함수 서버의 환경 변수에만 있습니다.
- 데이터베이스 west_trip: 일반 방문자가 직접 접근할 수 없습니다. 함수 서버만 저장·조회하고 수정 버전과 10개 백업을 한 번의 트랜잭션으로 기록합니다.

서버 연결에 실패하면 저장 실패를 표시하고 입력한 내용을 유지합니다. JSON 및 일정 포함 HTML로 별도 백업할 수 있습니다. 내려받은 일정 포함 HTML은 개인 브라우저에 저장하는 독립된 파일입니다.

GitHub Pages 설정: main / (root).
Supabase 프로젝트: ylgghvhcleyjaqwaukua / 서울 / SeokhyunJeong's Org 무료 플랜.

보안 검사에서 확인한 자동 RLS 트리거 함수의 공개 실행 권한은 회수했습니다. 일정 테이블에 일반 방문자용 RLS 정책이 없는 것은 직접 접근을 차단하기 위한 의도된 설정입니다.
참고: https://supabase.com/docs/guides/database/database-linter?lint=0028_anon_security_definer_function_executable

