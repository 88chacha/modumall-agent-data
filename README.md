# 모두몰 고객상담 에이전트 — 실습 데이터

모두의연구소 고객응대 에이전트 교안에서 쓰는 실습 데이터입니다.
'모두몰'은 교육용으로 설정한 **가상의 온라인 쇼핑몰**이며, 여기 담긴 정책과 어드민 데이터는
실재하는 기업의 것이 아닙니다. **다섯 파일 모두 자체 저작이라 자유롭게 쓰실 수 있습니다.**

## 담긴 파일

| 파일 | 내용 |
| --- | --- |
| `data/policy_modumall.md` | 상담원 업무 매뉴얼 v2.0 (13,627자 / 14개 장) |
| `data/mockdata_modumall.json` | 어드민 목데이터 (상품 20 · 주문 11 · 반품 5) |
| `data/agent_routing_goldenset.csv` | 라우팅 정답셋 160건 (평가 120 / few-shot 40) |
| `data/hard_cases.csv` | 경계 사례 72건 (6개 유형) |
| `data/answer_goldenset_multiturn.json` | 멀티턴 답변 정답셋 (34개 대화 · 56 에이전트 턴) |

## 노트북에서 받아 쓰기

```python
import urllib.request, pathlib

BASE_URL = "https://raw.githubusercontent.com/88chacha/modumall-agent-data/main/data/"
FILES = ("policy_modumall.md", "mockdata_modumall.json",
         "agent_routing_goldenset.csv", "hard_cases.csv",
         "answer_goldenset_multiturn.json")
for f in FILES:
    if not pathlib.Path(f).exists():
        urllib.request.urlretrieve(BASE_URL + f, f)
        print("받음:", f)
```

## 정답셋은 어떻게 만들었나

`agent_routing_goldenset.csv` 와 `hard_cases.csv` 의 고객 발화는 **직접 저작한 합성 문장**입니다
(`provenance=합성`). 실제 상담 데이터를 그대로 싣는 대신, 실제 발화에서 관찰한 **성질**을
재현하도록 썼습니다.

- 네 라우트 40건씩 · 평가 120 / few-shot 40
- 문장 길이 중간값 29자 (한두 문장으로 끝나는 짧은 문의)
- 지시어("이 ~", "이거")가 들어간 문의 14% — 거의 전부 주문·상품 문의에 몰려 있음
- 어드민 상품명이 그대로 적힌 문의 1.9% — 대부분은 조회할 대상을 특정할 수 없음
- 라우트 단서가 하나도 없는 문의 31%
- 오타·띄어쓰기 깨짐·구어체 포함

그래서 **규칙 라우터로는 정확도 0.675 언저리**가 나오고, 주문 라우트가 7/30으로 가장 약하게
나옵니다. 교안의 실습은 이 숫자들 위에서 진행됩니다.

실제 상담 데이터([AI Hub 소상공인 고객 주문 질의-응답 텍스트](https://www.aihub.or.kr/aihubdata/data/view.do?dataSetSn=102))는
AI Hub 이용정책상 재배포할 수 없어 담지 않았습니다. 원본을 쓰려면 AI Hub에서 직접 이용 신청
후 내려받아 같은 컬럼 구조로 바꿔 넣으면 됩니다.

## 라이선스

교육 목적으로 자유롭게 사용·수정하실 수 있습니다.
