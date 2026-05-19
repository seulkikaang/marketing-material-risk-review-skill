# 토큰 절약 운영 지침

이 repo는 영어 `SKILL.md`와 한국어 참고자료를 함께 둔다. 두 언어 문서를 동시에 읽으면 같은 내용이 중복되어 토큰이 낭비된다.

## 기본 원칙

1. **런타임 기본은 `SKILL.md`만 로드한다.**
   - Hermes skill 호출 시 자동으로 읽히는 본문은 `SKILL.md` 하나로 충분하다.
   - 한국어 답변은 모델이 한국어로 작성하면 되며, `references/skill-ko.md`를 매번 읽을 필요가 없다.

2. **한국어판은 사람 검토·배포 설명용이다.**
   - `references/skill-ko.md`는 사람이 읽는 번역본이다.
   - skill 동작 기준은 `SKILL.md`를 canonical로 둔다.

3. **참고자료는 필요한 것만 연다.**
   - 손모양, 로고, OCR, 영상 프레임: `references/visual-forensic-protocol-ko.md`
   - 리스크 분류, 법규·표시광고 질문: `references/risk-taxonomy-ko.md`
   - 유사 논란 패턴: `references/korean-case-reference-ko.md`

4. **전체 자료를 먼저 읽지 않는다.**
   - 가벼운 카피 검토: `SKILL.md`만으로 1차 판정
   - 이미지·영상 검토: 필요한 visual reference만 추가
   - `REVISE` 이상 또는 사용자가 근거를 요구할 때만 유사 패턴 조회

5. **출력에 원문을 붙이지 않는다.**
   - 참고자료에서 가져온 문장을 길게 인용하지 않는다.
   - `적용 체크포인트: 손모양·제스처 / 표시광고 / 그린워싱`처럼 짧게 표시한다.

## 권장 로딩 매트릭스

| 작업 | 읽을 파일 |
|---|---|
| 일반 카피·캡션 검토 | `SKILL.md` |
| 이미지 1장 검토 | `SKILL.md` + 필요 시 `visual-forensic-protocol-ko.md` |
| 영상·숏폼 검토 | `SKILL.md` + `visual-forensic-protocol-ko.md` |
| 가격·혜택·할인·효능 표현 | `SKILL.md` + 필요 시 `risk-taxonomy-ko.md` |
| 유사 케이스를 물어봄 | `SKILL.md` + `korean-case-reference-ko.md` |
| 사람이 한국어 문서 확인 | `references/skill-ko.md` |
| skill 수정·번역 검수 | `SKILL.md` + `references/skill-ko.md` |

## 출력 토큰 제한

- 기본 검토 결과: `Findings` 3개 이하, `Required Fixes` 3개 이하.
- 유사 패턴: 2~4개만.
- `PASS` 결과: 이유를 3줄 이내로.
- `HIGH_RISK` 이상: 문제 위치, 이유, 수정안 중심으로 짧게.

## 금지

- `SKILL.md`와 `references/skill-ko.md`를 매번 둘 다 읽기
- 참고자료 전체를 요약해서 출력하기
- 케이스 목록을 근거 없이 대량 나열하기
- 법률 판단처럼 단정하기
