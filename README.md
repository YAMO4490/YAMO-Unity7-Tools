# YAMO Unity7 Tools

Unity 6000.7용 YAMO 에디터 도구 모음입니다. 기존 [YAMO-UnityTools](https://github.com/YAMO4490/YAMO-UnityTools)에서 분리한 Unity 7 개발 버전입니다.

## 설치

Unity Package Manager의 **Install package from git URL**에 다음 주소를 입력합니다.

```text
https://github.com/YAMO4490/YAMO-Unity7-Tools.git
```

기존 패키지와 UPM 이름(`com.yamo.unitytools`)을 공유하므로 함께 설치하지 않습니다. 프로젝트에 같은 이름의 embedded 패키지가 있다면 먼저 백업한 뒤 교체해야 합니다.

## 환경

- 실제 검증 환경: Unity **6000.7.0b2**, Windows
- FBX Exporter: `com.unity.formats.fbx` **5.1.6**
- Autodesk FBX SDK: `com.autodesk.fbx` **5.1.3**
- 패키지 버전: **0.1.2**

의존성은 `package.json`에 선언되어 있습니다. 이전 Unity 버전의 호환성은 이 저장소에서 보장하지 않습니다.

## 주요 도구

- Mocap → Biped FBX: OptiTrack / MMRP 모션 바인딩, 팔 힌지 보정, Max Z-up FBX 출력
- Biped 변환 및 템플릿
- 아바타 본·머티리얼 검사와 베이크 도구

전체 기능과 메뉴는 [HANDBOOK.md](HANDBOOK.md), 모캡 파이프라인 사용법은 [가이드](Editor/Animation/MocapToBipedFbxPipeline_README.md)를 참고하세요.

## MMRP Body 매핑

`Hip`, `Spine2`, `Spine4` 골격에서는 다음 매핑을 사용합니다.

| Humanoid | FBX 본 |
| --- | --- |
| Hips | Hip |
| Spine | Spine2 |
| Chest | Spine4 |
| Upper Chest | None |

Unity 표준 이름을 사용하는 골격은 기존 표준 매핑을 유지합니다. 골반 중심의 기준 자세는 신체 스케일이 잘못 계산되지 않도록 기준 골격 높이를 보정합니다. 베이크된 클립에는 움직이지 않는 본의 위치 키도 보존합니다.

## 검증 범위

- UniCli로 CleanBuildCache 전체 재컴파일을 실행하여 이 패키지의 컴파일 오류 0개·경고 0개 확인. 프로젝트의 외부 에셋에는 경고가 남아 있습니다.
- UniCli를 통한 전체 패키지 Edit Mode 테스트 53개 통과. 빈 메시·메시 교체·EntityId 복원·실제 URP 오버레이 캡처·Shader 텍스처 수집·FBX 옵션 검색 회귀 테스트를 포함합니다.
- 실제 URP 캡처 픽셀 비교로 구도선 표시 및 창 종료 후 제거 확인. 구도 창은 설정 변경 시에만 전체 뷰를 갱신합니다.
- 실제 모션으로 Edit Mode / 30fps 베이크부터 Max Z-up FBX 출력 및 재임포트까지 확인.
- 51개 본, 5개 시점 비교에서 베이크 클립과 최종 FBX의 최대 위치 오차 약 0.006mm, 회전 오차 0도 확인.
- 위 수치의 전체 출력 검증 후 Chest 매핑을 Spine4로 변경했고, 변경된 매핑의 컴파일·회귀 검증·실제 아바타 임포트를 확인했습니다. Spine4 변경 후의 전체 출력과 Play Mode 전체 실행 및 장시간 배치 안정성은 별도 검증이 필요합니다.

프로젝트의 캐릭터, 씬, 녹화 모션, 출력 FBX는 이 패키지에 포함하지 않습니다. FBX 템플릿의 로컬 작업 경로 메타데이터는 배포본에서 제거했습니다.

에디터 전용의 고정 조회 테이블·캐시와 열린 창 참조는 Play Mode 전환에도 유지하도록 `NoAutoStaticsCleanup` 정책을 명시했습니다. 창 참조는 기존 `OnEnable`/`OnDisable`이 관리합니다. 경고를 일괄 숨기는 설정이나 pragma는 추가하지 않았습니다.
