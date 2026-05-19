# 비주얼 포렌식 프로토콜

마케팅 소재의 시각 리스크는 텍스트 검수만으로 잡히지 않는다. 이 프로토콜은 손모양, 로고 변형, 숨은 글자, 공식기관 오용, 영상 프레임 리스크를 보수적으로 찾기 위한 절차다.

## 기본 원칙

1. 전체 이미지 인상만으로 판단하지 않는다.
2. 손, 로고, 얼굴/신체, 배경 텍스트, 작은 오브젝트, UI 요소를 crop 단위로 나눈다.
3. “의도”를 단정하지 않고 “유사성/오인/논란 가능성”으로 기록한다.
4. 확정할 수 없으면 `PASS`가 아니라 `REVIEW` 또는 `REVISE`로 둔다.
5. 공식 로고·인증마크·공공기관 권위가 걸리면 법무/브랜드 검토로 올린다.

## 1. OCR 및 작은 텍스트 확인

확인 위치:

- 배너 하단 고지
- 이미지 속 간판, 포스터, 책, 의류, 컵, 배경 모니터
- 로고 내부 작은 글자
- 영상 자막과 빠르게 지나가는 프레임
- 랜딩페이지 캡처의 버튼/가격/조건 문구

기록 필드:

```yaml
ocr_findings:
  detected_text:
  location:
  normalized_text:
  risk_keyword_match:
  condition_or_disclaimer_visibility:
  decision: PASS/REVIEW/REVISE/HIGH_RISK
```

## 2. 손모양·제스처 확인

확인 대상:

- 집게손/핀칭 제스처
- OK sign, 손가락 욕, V sign, 성적 암시 제스처
- 특정 커뮤니티·혐오·정치 상징으로 해석될 수 있는 포즈
- 물건을 실제로 집는 기능적 맥락인지, 불필요하게 강조된 손동작인지

검토 질문:

- 엄지와 검지의 거리, 각도, 손등/손바닥 방향이 논란 상징과 유사한가?
- 손동작이 제품 사용에 필요한가, 아니면 장식적으로 삽입됐는가?
- 손모양 주변에 소시지, 동전, 작은 물체, 특정 문구 등 해석을 강화하는 요소가 있는가?
- 영상이라면 해당 제스처가 몇 프레임만 등장하는가?

판정:

- 기능적 손동작이고 논란 조합이 없으면 `PASS` 또는 `LOW`.
- 유사하나 의도/맥락이 불명확하면 `REVIEW`.
- 과거 논란 케이스와 구도·문맥이 매우 유사하거나 불필요하게 강조되면 `REVISE/HIGH_RISK`.

## 3. 로고·문장·엠블럼 확인

확인 대상:

- 국제기구: UN, WHO, UNESCO, UNICEF 등
- 정부/공공: 중앙부처, 지자체, 경찰, 군, 법원, 선관위, 공공 캠페인
- 대학/병원/협회/학회/인증기관
- 정당/정치단체, 종교단체
- 기업/브랜드/스포츠팀/행사 엠블럼

위험 신호:

- 월계수 + 지구본 + 영문 약자 조합
- 원형 엠블럼, 방패, 십자, 뱀과 지팡이, 파란 공식색
- “공식/인증/후원/선정/탈퇴/발표” 텍스트와 결합
- 뉴스 캡처나 기관 발표처럼 보이는 레이아웃

필요 자료:

- 원본 로고/브랜드 가이드
- 사용 허가 또는 제휴·후원 증빙
- 인증서·수상·랭킹 산정 기준
- 공식 보도자료 또는 기관 페이지

## 4. 로고 변형·숨은 상징 확인

단순 exact match가 아니라 원본 대비 변형을 본다.

절차:

1. 입력 이미지에서 로고 후보를 찾는다.
2. 가장 가까운 공식 원본 또는 canonical reference를 찾는다.
3. 크기·회전·색상·비율을 맞춰 정렬한다.
4. 중앙 문양, 글자 영역, 동물/캐릭터 얼굴, 지도, 방패, 월계수, 숫자/연도 등 민감 영역을 비교한다.
5. 차이 영역에 OCR, glyph matching, 실루엣/negative-space 확인을 수행한다.
6. 공식 원본과 다르고 이유가 없으면 `UNVERIFIED_LOGO_VARIANT`로 표시한다.

특히 확인할 변형:

- `ilbe`, `ㅇㅂ`, 정치인 이름/초성/별칭, 숫자 코드처럼 읽히는 글자
- 인물 실루엣, 벌레, 손가락, 무기, 극단주의 상징
- 호랑이 무늬, 머리카락, 불꽃, 잎, 지도, 월계수 등 negative space에 숨긴 형태
- 공식 로고를 질병, 전쟁, 정치, 조롱, 허위정보 맥락에 재배치한 경우

판정:

- 원본과 일치하고 사용권이 확인되면 `PASS`.
- 내부 핵심 도상이 다르거나 작은 글자가 의심되면 `REVIEW`.
- 혐오·정치·고인 조롱·허위 권위 차용이 명확하면 `HIGH_RISK` 또는 `LEGAL_REVIEW_REQUIRED`.

## 5. 역사·국가·정치 상징 확인

확인 대상:

- 욱일기 또는 방사형 전범기 연상 패턴
- 국기, 지도, 영토 표기, Sea of Japan/East Sea, 독도
- 군복, 계급장, 총기, 진압 장면
- 민주화운동, 참사, 전쟁, 식민지 관련 날짜·장소·색상·리본

질문:

- 게시일 또는 이벤트명이 민감 날짜와 겹치는가?
- 단어는 중립적이지만 이미지와 결합해 다른 사건을 떠올리게 하는가?
- 해외 원본 소재를 한국 시장에 그대로 가져오며 지도/역사 표현이 충돌하는가?

## 6. 영상 프레임 확인

영상 소재는 대표 컷만 보면 안 된다.

권장 절차:

- 장면 전환 지점별 스틸 추출
- 0.5~1초 간격 프레임 샘플링
- 손/로고/자막/배경 오브젝트 crop
- 논란 가능 프레임의 timestamp 기록
- 외주 제작물은 원본 프로젝트 파일 또는 스토리보드와 대조

기록 예시:

```yaml
video_frame_findings:
  timestamp: 00:12.5
  crop: right_hand / background_logo / subtitle
  issue: pinching-like gesture
  confidence: low/medium/high
  recommendation: replace frame or edit gesture
```

## 7. 최종 기록 템플릿

```yaml
visual_risk_review:
  overall_visual_decision: PASS/REVIEW/REVISE/HIGH_RISK/LEGAL_REVIEW_REQUIRED
  findings:
    - element:
      location:
      risk_type: gesture/logo_mutation/authority_claim/historical_symbol/hidden_text/ui_dark_pattern/ai_synthetic
      why_it_matters:
      evidence_needed:
      recommendation:
```
