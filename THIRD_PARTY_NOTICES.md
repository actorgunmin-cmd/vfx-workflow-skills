# 출처와 포함 범위

이 패키지는 공개 워크플로에서 독립 재구성한 지침 26개와 사용자 요청으로 추가한 Python 매칭·색 보정·매팅 검수·재합성 지침 4개다. 인스타그램 창작자의 원본 SKILL.md, 내부 구현, 비공개 강의 또는 추출 코드가 아니다. 원본 창작자, OpenAI, Adobe 또는 아래 프로젝트와의 제휴·승인·동일 구현을 뜻하지 않는다.

기존 공개 게시물의 출처 URL·주제·짧은 관찰 요약과 검토 범위는 [review-manifest.json](review-manifest.json)에 보존했다. 검토 기록은 이전 작업에서 전달받았으며 이번 배포 검토에서 33개 게시물을 다시 전체 열람한 것은 아니다. `hyun2ai` 프로필과 일부 `hyun2xyz` 게시물 URL은 기존 기록의 식별자 그대로 남겼다. 현재 계정 동일성이나 링크 접근 가능성을 새로 확정하지 않았다.

각 SKILL.md의 실행 절차·품질 기준은 독립 설계다. 게시물에서 비공개인 명령·파라미터·모델 구성을 알아냈다는 의미가 아니다. 사용자 추가 스킬 4개는 게시물 관찰 사실에 포함하지 않았다.

원본 사진·영상·음원·인스타 캡션 전문·댓글 전문·유료 강의·모델 가중치·외부 플러그인·외부 프로젝트 소스는 배포하지 않는다. 이 저장소의 Python 보조 코드는 이 패키지를 위해 작성했다. 외부 도구를 실행하려면 그 프로젝트의 설치 조건과 라이선스를 별도로 확인한다. 이 패키지의 공개가 외부 자료나 모델에 대한 사용 권한을 부여하지 않는다. 이 배포판에 별도 재배포 라이선스는 지정하지 않았다.

기술 참고:

- [COLMAP 출력 형식](https://colmap.github.io/format.html)
- [OpenCV PnP](https://docs.opencv.org/4.x/d5/d1f/calib3d_solvePnP.html), [특징 매칭](https://docs.opencv.org/4.x/dc/dc3/tutorial_py_matcher.html), [변환](https://docs.opencv.org/4.x/da/d54/group__imgproc__transform.html)
- [MatAnyone](https://github.com/pq-yang/MatAnyone), [MatAnyone 2](https://github.com/pq-yang/MatAnyone2): 코드·가중치 미포함. MatAnyone 2의 저장소 라이선스는 해당 저장소가 명시한 NTU S-Lab License 1.0을 따른다.
- [OpenColorIO](https://opencolorio.readthedocs.io/en/latest/guides/authoring/overview.html)
- [OpenAI 공식 스킬 문서](https://learn.chatgpt.com/docs/build-skills)

상표·프로젝트명·작품명은 기술 및 출처 식별에만 사용한다. 각 권리는 해당 권리자에게 있다.
