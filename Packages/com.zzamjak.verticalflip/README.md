# VerticalFlip

두 스프라이트를 세로 슬라이스 단위로 번갈아 뒤집는 플립 애니메이션 패키지입니다.
옥외 광고판이나 공항 안내판 같은 연출을 SpriteRenderer(월드)와 uGUI `Image`(Canvas) 양쪽에서 같은 컴포넌트 하나로 구현합니다.

회전 연산 전체가 셰이더에서 처리되므로 메시 재생성이나 레이아웃 갱신이 발생하지 않습니다.

설치 방법과 사용법은 레포지토리 루트 [README](https://github.com/zzamjak-cloud/VerticalFlip) 를 참고하세요.
변경 사항은 [CHANGELOG](CHANGELOG.md) 에 있습니다.

## 요구 사항

- Unity 6000.0 (Unity 6) 이상
- Universal Render Pipeline (URP) — 셰이더가 URP ShaderLibrary 를 사용하므로 필수입니다
- uGUI (`com.unity.ugui`) — Canvas 모드 사용 시

## 라이선스

GNU General Public License v3.0 only (`GPL-3.0-only`). 저작권자 zzamjak.
재배포·수정본·파생 저작물은 이 고지를 유지하고 같은 라이선스로 배포해야 한다. [LICENSE](LICENSE.md), [NOTICE](NOTICE.md) 참고.
