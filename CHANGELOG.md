# 변경 기록

## 0.1.0 — 2026-10-17

- Unity 6000.7 개발용 저장소 분리.
- Unity 6000.7에서 시그니처가 변경된 AvatarSetupTool 내부 함수의 잘못된 리플렉션 호출 방지.
- Hip 기반 MMRP 골격의 직접 매핑 추가: Hips → Hip, Spine → Spine2, Chest → Spine4, Upper Chest 미사용.
- 골반 중심 기준 자세로 인한 Humanoid 신체 스케일 및 RootT 증폭 보정.
- Edit Mode / Play Mode 결과 클립 생성에서 고정 위치 키 보존.
- 매핑·기준 골격 높이·고정 위치 키 회귀 검증 추가.
- 검증 환경의 FBX Exporter 5.1.6 / Autodesk FBX 5.1.3 의존성 명시.
