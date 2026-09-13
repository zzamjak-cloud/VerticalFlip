# VerticalFlip

[![openupm](https://img.shields.io/npm/v/com.zzamjak.verticalflip?label=openupm&registry_uri=https://package.openupm.com)](https://openupm.com/packages/com.zzamjak.verticalflip/)
[![license](https://img.shields.io/badge/license-GPL--3.0--only-blue.svg)](Packages/com.zzamjak.verticalflip/LICENSE.md)

두 스프라이트를 세로 슬라이스 단위로 번갈아 뒤집는 플립 애니메이션 패키지입니다.
옥외 광고판이나 공항 안내판 같은 연출을 SpriteRenderer(월드)와 uGUI `Image`(Canvas) 양쪽에서 같은 컴포넌트 하나로 구현합니다.
회전 연산 전체가 셰이더에서 처리되므로 메시 재생성이나 레이아웃 갱신이 발생하지 않습니다.

이 레포지토리는 **개발용 Unity 프로젝트**이며, 패키지 본체는
[`Packages/com.zzamjak.verticalflip`](Packages/com.zzamjak.verticalflip) 에 임베디드되어 있습니다.
버전별 변경 사항은 [CHANGELOG](Packages/com.zzamjak.verticalflip/CHANGELOG.md) 를 참고하세요.

## 요구 사항

- Unity 6000.0 (Unity 6) 이상
- **Universal Render Pipeline (URP)** — 스프라이트 셰이더가 URP ShaderLibrary 를 include 하고 `RenderPipeline = UniversalPipeline` 태그를 사용하므로 필수입니다. 내장 파이프라인 폴백은 제공하지 않습니다.
- uGUI (`com.unity.ugui`) — Canvas 모드 사용 시

## 설치 방법

### 1. OpenUPM (권장)

    openupm add com.zzamjak.verticalflip

또는 `Packages/manifest.json` 에 스코프 레지스트리를 직접 추가합니다.

    {
      "scopedRegistries": [
        {
          "name": "zzamjak",
          "url": "https://package.openupm.com",
          "scopes": ["com.zzamjak"]
        }
      ],
      "dependencies": {
        "com.zzamjak.verticalflip": "1.0.0"
      }
    }

### 2. Git URL

Package Manager → `Install package from git URL...`

    https://github.com/zzamjak-cloud/VerticalFlip.git?path=/Packages/com.zzamjak.verticalflip#v1.0.0

## 사용법

| 컴포넌트 | 대상 | 메뉴 |
|----------|------|------|
| `VerticalFlip` | `SpriteRenderer` 또는 uGUI `Image` | `Add Component > CAT > Effects > VerticalFlip` |

1. `SpriteRenderer` 또는 `Image` 가 붙은 오브젝트에 `VerticalFlip` 을 추가합니다. 둘 다 있으면 `Image`(UI)가 우선합니다.
2. `First Sprite` / `Second Sprite` 두 개를 모두 할당합니다. 하나라도 비면 컴포넌트가 비활성화됩니다.
3. 재생하면 `Time Between Flips` 간격으로 두 스프라이트가 번갈아 뒤집힙니다.
4. 재생하지 않고 확인하려면 인스펙터의 씬 뷰 프리뷰 버튼을 사용합니다(최대 60초, 진행도 스크럽 지원).

`Image` 는 `Type` 이 `Simple` 이어야 하며, 다른 값이면 경고와 함께 자동 변경됩니다.

### 주요 인스펙터 항목

| 항목 | 기본값 | 설명 |
|------|--------|------|
| `Slice Count` | 6 | 세로 슬라이스 개수 (1~50) |
| `Flip Duration` | 0.2 | 슬라이스 하나가 180도 회전하는 데 걸리는 시간 (초) |
| `Flip Offset Between Slices` | 0.1 | 인접 슬라이스 간 시작 지연. 0 이면 전부 동시에 뒤집힙니다 |
| `Time Between Flips` | 3 | 플립 사이 대기 시간 (초) |
| `Show Column Lines` | on | 슬라이스 구분선 표시. 끄면 셰이더 변형에서 라인 연산이 통째로 제외됩니다 |
| `Line Color` / `Line Width` | 검정 / 0.004 | 구분선 색과 UV 기준 두께. 슬라이스 개수와 무관하게 굵기가 일정합니다 |
| `Use Low Quality On Mobile` | on | 모바일에서 슬라이스를 12개로 제한 (직렬화 값은 바뀌지 않습니다) |

### 스크립트 API

```csharp
using CAT.VerticalFlip;

var flip = GetComponent<VerticalFlip>();

flip.SetSprites(spriteA, spriteB);              // 런타임 스프라이트 교체
flip.SetColumnLines(true, Color.black, 0.004f); // 구분선 설정
flip.ApplySettings();                           // 인스펙터 값을 코드로 바꾼 뒤 반영
flip.StartFlipping();
flip.StopFlipping();
```

### 셰이더

| 셰이더 | 용도 |
|--------|------|
| `CAT/Effects/VerticalFlipSprite` | SpriteRenderer (URP Unlit, SRP Batcher 호환) |
| `CAT/UI/VerticalFlipUI` | uGUI Image (스텐실·마스킹 지원) |

두 셰이더는 `Runtime/Resources/VerticalFlip/` 에 있어 빌드에서 스트리핑되지 않습니다.
컴포넌트도 셰이더 참조를 직렬화해 두므로 `Shader.Find` 에만 의존하지 않습니다.

### 스프라이트 아틀라스

스프라이트가 아틀라스 안에 있어도 `textureRect` 를 셰이더에 전달해 올바른 영역만 샘플링합니다. 별도 설정이 필요 없습니다.

## 샘플

Package Manager → VerticalFlip → Samples → `Demo Scene` → Import

## 라이선스

GNU General Public License v3.0 only. [LICENSE](Packages/com.zzamjak.verticalflip/LICENSE.md) 참고.
