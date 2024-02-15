---
license: cc-by-nc-4.0
pipeline_tag: summarization
---

### 베이스 모델
[gogamza/kobart-base-v2](https://huggingface.co/gogamza/kobart-base-v2)을 베이스로 하였고,
aihub에 있는 요약 데이터를 사용하여 학습을 진행하였습니다.


### 사용 데이터셋 (683,335건)
[추상 요약 사실성 검증 데이터](https://www.aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&aihubDataSe=data&dataSetSn=71620)  
[요약문 및 레포트 생성 데이터](https://www.aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&aihubDataSe=data&dataSetSn=582)  
[문서요약 텍스트](https://www.aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&aihubDataSe=data&dataSetSn=97)  
[도서자료 요약](https://www.aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&aihubDataSe=data&dataSetSn=9)  

### 학습 
Nvidia A100 x 1을 사용하였으며, 3epoch 학습에 17h이 소요되었습니다.

### 사용 예제

```python

from transformers import pipeline
# GPU 사용 케이스
# pipe = pipeline("summarization", model="gangyeolkim/kobart-korean-summarizer-v2", device=0)

# GPU 미사용 케이스
pipe = pipeline("summarization", model="gangyeolkim/kobart-korean-summarizer-v2")
original_text = """
(서울=연합뉴스) 특별취재팀 = 연합뉴스TV에 대한 적대적 인수·합병(M&A)을 시도하는 을지재단이 사실상 박준영 회장 일가의 '족벌경영' 체제 속에 사익을 실현하는 수단으로 활용된다는 지적이 나온다.
을지재단은 산하에 병원, 대학 등 여러 법인을 두고 있지만, 박준영 회장과 아내인 홍성희 을지대 총장이 요직을 주고받으면서 사실상 함께 경영하는 체제다.
비영리법인으로 각종 세제 혜택을 받는 을지재단의 '족벌경영' 폐해는 여러 사례를 통해 여실히 드러나고 있다.
부부가 비상근이사이면서도 재단에서 매달 1천만원씩 '셀프급여'를 받은 것, 박 회장이 '재단 소속 병원'에서 마약성 진통제를 3천회 이상 처방받은 것, 개인 소유의 관계회사를 만들어 병원과 거래에서 생기는 수익을 챙긴 것 등등.
을지재단은 연합뉴스TV의 최대주주 지위를 노리면서 그 운영 방침으로 '소유와 경영의 분리', '공정성 및 공익성 실현'을 내세웠다.
하지만 박 회장 부부의 이익을 위해 철저하게 재단을 '사유화'한 행태가 여러 사례를 통해 드러난 상황에서, 이들의 공영방송 지배를 우려하는 목소리는 갈수록 커지고 있다.
"""

summarized = pipe(original_text)
print(summarized[0]["summary_text"])  # 을지재단이 박 회장 일가의 '족벌경영' 체제 속에 사익을 실현하는 수단으로 활용된다는 지적이 나오고 있다.
```