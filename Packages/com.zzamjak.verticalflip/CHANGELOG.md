# Changelog

이 프로젝트의 주요 변경 사항을 기록합니다.

포맷은 [Keep a Changelog](https://keepachangelog.com/ko/1.1.0/)를 따르며,
버전은 [Semantic Versioning](https://semver.org/lang/ko/)을 따릅니다.

## [1.0.0] - 2026-09-13

VerticalFlip 기능을 독립 UPM 패키지로 분리한 최초 릴리스입니다.

### Added

- `VerticalFlip` 컴포넌트: 두 스프라이트를 세로 슬라이스 단위로 번갈아 뒤집는 플립 애니메이션
- SpriteRenderer(월드)와 uGUI `Image`(Canvas) 자동 판별 및 동시 지원
- URP 전용 셰이더 2종: `CAT/Effects/VerticalFlipSprite`, `CAT/UI/VerticalFlipUI`
- 슬라이스 개수, 플립 시간, 슬라이스 간 지연, 플립 간 대기 시간 인스펙터 설정
- 슬라이스 구분선 표시 옵션 (`_SHOWLINES_ON` 키워드로 셰이더 변형 분리)
- 스프라이트 아틀라스 UV 영역 인식 (`_MainTexRect` / `_SecondTexRect`)
- 모바일 저사양 모드: 슬라이스 개수를 12개로 자동 제한 (인스펙터 값은 변조하지 않음)
- 씬 뷰 실시간 프리뷰 및 진행도 스크럽 (재생 없이 에디트 모드에서 확인)
- 빌드 스트리핑 방지를 위한 셰이더 직렬화 참조 + `Runtime/Resources` 배치
- `Demo Scene` 샘플: 광고판 스프라이트 2종 플립 예시 씬
