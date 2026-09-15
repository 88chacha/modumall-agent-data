# 모두몰 고객상담 에이전트 — 실습 데이터

모두의연구소 고객응대 에이전트 교안에서 쓰는 실습 데이터입니다.
'모두몰'은 교육용으로 설정한 **가상의 온라인 쇼핑몰**이며, 여기 담긴 정책과 어드민 데이터는
실재하는 기업의 것이 아닙니다.

## 담긴 파일

| 파일 | 내용 | 출처 |
| --- | --- | --- |
| `data/policy_modumall.md` | 상담원 업무 매뉴얼 v2.0 (13,627자 / 14개 장) | 자체 저작 |
| `data/mockdata_modumall.json` | 어드민 목데이터 (상품 20 · 주문 11 · 반품 5) | 자체 저작 |
| `data/answer_goldenset_multiturn.json` | 멀티턴 답변 정답셋 (34개 대화 · 56 에이전트 턴) | 자체 저작(합성) |

## 노트북에서 받아 쓰기

```python
import urllib.request, pathlib

BASE_URL = "https://raw.githubusercontent.com/OWNER/REPO/main/data/"
for f in ("policy_modumall.md", "mockdata_modumall.json", "answer_goldenset_multiturn.json"):
    if not pathlib.Path(f).exists():
        urllib.request.urlretrieve(BASE_URL + f, f)
        print("받음:", f)
```

## 여기 없는 파일

라우팅 정답셋(`agent_routing_goldenset.csv`)과 경계 사례(`hard_cases.csv`)는 **이 저장소에
담지 않았습니다.** 두 파일의 고객 발화는
[AI Hub — 소상공인 고객 주문 질의-응답 텍스트](https://www.aihub.or.kr/aihubdata/data/view.do?dataSetSn=102)
원본에서 가져온 것이고, AI Hub는 원본 데이터를 제3자에게 제공·배포하는 것을 허용하지 않습니다.

필요하시면 AI Hub에서 직접 이용 신청 후 내려받으시고, 라벨 매핑은 교안 운영자에게 문의해 주세요.

## 라이선스

자체 저작 파일 3종은 교육 목적으로 자유롭게 쓰실 수 있습니다.
