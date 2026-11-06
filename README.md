# VFX 작업 지침 스킬 30개

실사·AI 영상의 트래킹, 분리, 생성 소스, 합성과 마감을 위한 독립 지침 모음이다. **공개 게시물에서 재구성한 26개 + 사용자 요청으로 추가한 4개**로 구성한다. 원본 창작자의 내부 스킬 추출본이나 실행 엔진 모음이 아니며 제휴·동일 구현을 뜻하지 않는다.

[전체 ZIP](hyun2ai-vfx-skills.zip) · [개별 다운로드 목록](index.html) · [검토 기록](REVIEW.md) · [출처/권리 고지](THIRD_PARTY_NOTICES.md) · [기계 판독 검증 기록](validation.json) · [ZIP SHA-256](SHA256SUMS)

GitHub에서는 `index.html`이 코드로 보일 수 있다. 각 스킬은 아래 표에서 개별 ZIP으로 받고, 파일 화면의 **Raw / Download raw file**로 받는다. HTML 다운로드 목록은 전체 ZIP을 풀어 로컬 브라우저에서 열면 개별 다운로드에 사용할 수 있다. 풀린 폴더에는 전체 ZIP 자체가 없으므로 전체 ZIP 링크는 저장소에서 사용한다.

## 설치와 사용

1. 전체 ZIP을 임시 폴더에 푼다.
2. ZIP 안의 `.agents/skills/`를 사용할 프로젝트의 `.agents/skills/`에 복사한다. 숨김 폴더도 복사하며, 같은 이름이 이미 있으면 비교한 뒤 교체한다.
3. 개별 ZIP은 압축을 풀어 나온 `스킬이름/` 폴더 하나를 프로젝트의 `.agents/skills/` 아래에 놓는다. 30개를 모두 설치할 필요는 없다.
4. 해당 프로젝트를 Codex에서 열어 `$스킬이름`으로 호출한다. 새 스킬이 보이지 않으면 Codex를 다시 시작한다.

이 저장소는 배포 파일을 제공한다. 전체 소스·30개 SKILL.md·Python 보조 코드·검증 도구는 `hyun2ai-vfx-skills.zip` 안에 있다. 먼저 전체 ZIP을 풀면 `skills/`의 원하는 폴더를 프로젝트의 `.agents/skills/`로 복사할 수 있다. ZIP에는 열람용 `skills/`와 설치용 `.agents/skills/`가 함께 있으므로 둘을 중복 설치하지 않는다. 사용자 범위는 `~/.agents/skills/`이며 이 패키지가 자동으로 설치하거나 설정을 변경하지 않는다. 경로와 검색 동작은 [OpenAI 공식 스킬 문서](https://learn.chatgpt.com/docs/build-skills)를 따른다.

```text
$colmap-vfx 원본 영상의 카메라를 추적하고, 지면 격자 오버레이로 검수해줘.
$vfx-ai-source-match 원본을 기준으로 AI 영상의 시간·구도·움직임을 맞추고 오차와 실패 구간을 남겨줘.
$vfx-source-color-match AI 영상의 색감·노출·블랙·질감을 원본에 맞추고 경계와 시간축 펌핑을 확인해줘.
$vfx-precision-roto 원본 인물의 머리카락·손가락·모션블러까지 보존한 연속 alpha와 검수 프리뷰를 만들어줘.
$vfx-original-restore AI 배경에 원본 인물을 복원하고 이중 인물·가림·경계 색·발 접지를 검사해줘.
```

## 스킬 목록과 필요한 도구

스킬은 작업 지침이다. COLMAP·Blender·AE·FFmpeg·ComfyUI·MatAnyone, 생성 모델/노드/가중치는 별도다. 가능한 도구를 확인한 뒤 실제 지원되는 기능으로 수행하며 미실행 부분은 구분한다. 27–30번은 게시물에서 추출한 기능이 아니라 사용자 후속 요청과 공식 기술 문서에 따른 독립 설계다.

| # | 스킬 | 범위 | 필요한 환경 |
|---|---|---|---|
| 01 | [`vfx-shot-pipeline`](vfx-shot-pipeline.zip) | 샷 전체 파이프라인 | ffprobe; 선택한 실행 도구 |
| 02 | [`colmap-vfx`](colmap-vfx.zip) | COLMAP 카메라 트래킹 | COLMAP; 포즈 도우미는 Python 표준 라이브러리 |
| 03 | [`vfx-pnp-track`](vfx-pnp-track.zip) | PnP 포즈 복원 | OpenCV·NumPy, 실제 K/3D 대응점 |
| 04 | [`vfx-surface-track`](vfx-surface-track.zip) | 포인트·평면 트래킹 | OpenCV/CoTracker 또는 설치된 트래커 |
| 05 | [`vfx-procedural-3d`](vfx-procedural-3d.zip) | 코드 기반 3D·셰이더 | 선택한 OpenGL/WebGL/코드 렌더러 |
| 06 | [`vfx-cloth-sim`](vfx-cloth-sim.zip) | 천막·천 시뮬레이션 | Blender 또는 구현한 PBD/스프링 솔버 |
| 07 | [`vfx-fooh-composite`](vfx-fooh-composite.zip) | FOOH·CG 삽입 | Blender 또는 선택한 렌더러·합성기 |
| 08 | [`vfx-keying-despill`](vfx-keying-despill.zip) | 키잉·로토·디스필 | 설치된 키어/합성기 |
| 09 | [`vfx-clean-plate`](vfx-clean-plate.zip) | 클린 플레이트·리무브 | 패치/트래킹/인페인팅 도구 |
| 10 | [`vfx-depth-relight`](vfx-depth-relight.zip) | 뎁스·노멀·리라이팅 | 깊이/노멀 추정기·합성기 |
| 11 | [`vfx-background-replace`](vfx-background-replace.zip) | 배경·계절 교체 | 전경 매팅·선택한 V2V/배경 생성기·합성기 |
| 12 | [`vfx-local-video-edit`](vfx-local-video-edit.zip) | 국소 생성·소품·눈 디테일 | 트래커·선택한 생성/합성기 |
| 13 | [`vfx-plate-extend`](vfx-plate-extend.zip) | 플레이트·긴 아트워크 확장 | 정합/확장 도구·레이어 합성기 |
| 14 | [`vfx-motion-lettering`](vfx-motion-lettering.zip) | 레터링·캐릭터 모션 | 벡터/텍스트·애니메이션/합성기 |
| 15 | [`vfx-moving-photo`](vfx-moving-photo.zip) | 무빙 포토 | 레이어 합성기 또는 선택한 영상 생성기 |
| 16 | [`vfx-vector-retexture`](vfx-vector-retexture.zip) | 벡터 조형 리텍스처 | 벡터 래스터화·마스크 조건 이미지 편집기 |
| 17 | [`vfx-start-end-morph`](vfx-start-end-morph.zip) | Start/End 몰핑 | start/end 지원 생성기·선택한 보간기 |
| 18 | [`vfx-audio-reactive`](vfx-audio-reactive.zip) | 오디오 리액티브 | PCM WAV; 영상화에는 ComfyUI 등 별도 도구 |
| 19 | [`vfx-controlled-impact`](vfx-controlled-impact.zip) | 충돌·폭발 VFX | 선택한 생성기·합성기 |
| 20 | [`vfx-marker-direct`](vfx-marker-direct.zip) | 마커 기반 VFX 지시 | 마커 조건을 실제 지원하는 편집/생성 도구 |
| 21 | [`vfx-matte-stylize`](vfx-matte-stylize.zip) | 매트→구름·빛·잔상 | 매팅·효과 합성기 또는 조건 지원 생성기 |
| 22 | [`vfx-character-continuity`](vfx-character-continuity.zip) | 캐릭터·배경 연속성 | 레퍼런스 지원 이미지/영상 도구 |
| 23 | [`vfx-performance-transfer`](vfx-performance-transfer.zip) | 퍼포먼스 전이 | 현재 연기 전이 지원 도구 |
| 24 | [`vfx-ae-automation`](vfx-ae-automation.zip) | After Effects 자동화 | After Effects·연결 MCP 또는 허용 스크립트 |
| 25 | [`vfx-comfy-workflow`](vfx-comfy-workflow.zip) | ComfyUI 워크플로우 구성 | 실제 ComfyUI·설치 노드·모델 |
| 26 | [`vfx-temporal-finish`](vfx-temporal-finish.zip) | 시간 일관성·보간·업스케일·마감 | 선택한 보간/업스케일/인코딩 도구 |
| 27 | [`vfx-ai-source-match`](vfx-ai-source-match.zip) | AI·원본 프레임 정렬 | Python·OpenCV·NumPy; 영상 추출/시간 매핑은 별도 |
| 28 | [`vfx-source-color-match`](vfx-source-color-match.zip) | 원본 기준 색감·질감 매칭 | Python·OpenCV·NumPy; Log/HDR·질감은 별도 도구 |
| 29 | [`vfx-precision-roto`](vfx-precision-roto.zip) | 정밀 실루엣·비디오 매팅 | MatAnyone 계열 별도 Python/모델 환경; QC는 OpenCV·NumPy |
| 30 | [`vfx-original-restore`](vfx-original-restore.zip) | AI 배경 위 원본 인물 재합성 | 전경 RGB/alpha; Python·OpenCV·NumPy |

개별 ZIP 링크는 각 스킬의 SKILL.md, UI 메타데이터와 해당 보조 코드를 함께 제공한다. 원문을 읽거나 수정하려면 ZIP을 푼다.

## Python 보조 코드

보조 스크립트는 각 `scripts/` 폴더에 있다. 스킬 설치 폴더를 기준으로 상대 경로를 해석한다. 원본과 기존 결과를 덮어쓰지 않고 새 출력 경로를 지정한다.

| 스크립트 | 수행 범위 | 제한 |
|---|---|---|
| `colmap_pose.py` | COLMAP text 포즈→CV/GL camera-to-world JSON | 솔브·intrinsics·world 정렬·시간 추정 없음 |
| `audio_envelope.py` | 정수 PCM WAV→유리수 fps RMS/onset CSV | 비트 검출·stem 분리 아님 |
| `inspect_plate.py` | ffprobe 메타데이터와 도구 경로 | per-frame PTS/CFR 판정·인코딩 없음 |
| `align_frame.py` | SIFT/RANSAC affine/homography와 유효 영역 | 8-bit 분석 프레임 쌍; 시간·시차·인체 변형 복구 없음 |
| `match_color.py` | 공통 패치의 고정 SDR sRGB gain/offset과 재적용 | Log/HDR·리라이팅·그레인·피부별 grade 없음 |
| `matte_qc.py` | alpha 면적·부분 투명도·프레임 변화 보고 | 매팅 모델 아님; 정답 품질 점수 아님 |
| `composite_frame.py` | straight RGB+alpha의 linear-light over | SDR sRGB 전용; 정렬·탈오염·매팅 없음 |

처음 3개는 Python 표준 라이브러리를 사용하며 `inspect_plate.py`의 정상 메타데이터 읽기에는 ffprobe가 필요하다. 추가 4개에는 OpenCV·NumPy가 필요하다. 전체 ZIP을 푼 디렉터리에서 실행할 로컬 가상환경 예:

```bash
python3 -m venv .venv
.venv/bin/python -m pip install -r requirements-dev.txt
.venv/bin/python tools/validate_package.py
```

Windows에서는 `.venv/bin/python` 대신 `.venv\Scripts\python.exe`를 쓴다. 제작 시 Python 3.9 / macOS arm64에서 검증했으며 다른 장치의 모델 지원을 보장하지 않는다. 마지막 4개 스킬만 개별 설치했다면 `python3 -m pip install numpy opencv-python-headless`로 보조 코드 의존성을 준비할 수 있다. MatAnyone 모델 실행 환경은 공식 저장소에 따라 별도로 설치한다. 확인한 MatAnyone 2 코드의 `fgr`는 녹색 배경 프리뷰여서 straight foreground로 바로 합성하면 안 된다. 정확한 alpha와 원본 RGB를 별도로 관리하고 경계 오염을 정리한다.

단일 프레임 도우미를 영상 전체에 적용하려면 원본 PTS/프레임 대응을 먼저 확정한다. 색 설정은 샷에서 고정 재사용하며 프레임별 자동 정렬의 떨림을 검수한다. 검증기는 helper 수치/CLI 테스트 후 30개 개별 ZIP과 전체 ZIP을 다시 만든다. `tools/build_catalog.py`는 스킬 문서와 관찰 목록만 재생성하고 Python helper 소스는 각 스킬에 유지한다. 문서 재생성 후 검증기를 실행해 ZIP을 갱신한다.

## 출처와 검증 수준

기존 검토 기록은 피드 33개·릴스 탭 14개 대조를 포함한다. 캐러셀/대표 화면 관찰의 한계는 [manifest](review-manifest.json)에 남겼다. 모든 릴스 프레임/음성을 전사한 것이 아니며 이번 작업에서 전체 게시물을 재조사하지 않았다. 원본 미디어·캡션 전문·비공개 강의·외부 모델 코드/가중치는 포함하지 않는다.

스킬 구조, 7개 도우미의 합성 데이터/오류 경로/CLI, 로컬 참조와 ZIP을 검증했다. **실제 촬영 영상 전체 실행, COLMAP 솔브, Blender/AE/FFmpeg 렌더, MatAnyone GPU 추론과 AI 영상 생성은 미검증**이다. 정렬/색/합성 도우미의 테스트 통과는 실영상의 완벽한 매칭이나 정교한 로토 품질을 보장하지 않는다. [검토 설명](REVIEW.md)과 [검증 JSON](validation.json)을 함께 읽는다.
