# 변경 기록

## 0.1.1 — 2026-10-17

- 시선 컴포넌트가 빈 Renderer/메시를 안전하게 처리하고 메시 교체 시 블렌드셰이프 인덱스를 갱신하도록 수정.
- 카메라 구도 창의 Built-in 렌더 이벤트 핸들러 이름을 변경하여 Unity의 OnPostRender 메시지 이름과 충돌하지 않도록 수정.
- 설정 변경과 창 열기/닫기 시에만 전체 뷰를 갱신하고, All On/Off·카메라 정렬·복원 버튼의 갱신을 유지.
- URP end-camera 콜백에서 오프스크린 오버레이를 카메라의 실제 출력 텍스처에 그린 뒤 기존 렌더 타깃 복원.
- Hinge·모캡 실행기·lilToon 베이커·아바타 베이크의 EntityId.GetRawData()를 지원되는 EntityId.ToULong()으로 교체.
- 빈 메시, 메시 교체, EntityId 복원, 실제 렌더 픽셀 비교 회귀 테스트 추가.

## 0.1.0 — 2026-10-17

- Unity 6000.7 개발용 저장소 분리.
- Unity 6000.7에서 시그니처가 변경된 AvatarSetupTool 내부 함수의 잘못된 리플렉션 호출 방지.
- Hip 기반 MMRP 골격의 직접 매핑 추가: Hips → Hip, Spine → Spine2, Chest → Spine4, Upper Chest 미사용.
- 골반 중심 기준 자세로 인한 Humanoid 신체 스케일 및 RootT 증폭 보정.
- Edit Mode / Play Mode 결과 클립 생성에서 고정 위치 키 보존.
- 매핑·기준 골격 높이·고정 위치 키 회귀 검증 추가.
- 검증 환경의 FBX Exporter 5.1.6 / Autodesk FBX 5.1.3 의존성 명시.
