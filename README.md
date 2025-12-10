# UPssue: 하루 5분 리포트  
주식 시장의 급등·급락 종목을 AI 기반 근거 분석으로 이해할 수 있게 해주는 자동화 리포트 서비스

---

## 서비스 개요

UPssue는 “UP(상승)”과 “issue(이슈)”의 합성어로, 초보 투자자가 복잡한 시장 데이터를 빠르게 이해할 수 있도록 돕는 AI 기반 투자 인사이트 플랫폼입니다.

초보 투자자는 뉴스·데이터·지표 등 과도한 정보 중 어떤 것이 중요한지 판단하기 어렵습니다.  
UPssue는 이를 해결하기 위해 다음 기능을 제공합니다.

- 급등락 종목의 상승/하락 원인 자동 분석  
- 뉴스 기반 파급력 분석  
- 테마 내 관련 종목의 상승 가능성 예측  
- 매일 주요 경제 뉴스 요약  

---

## 주요 기능

### 1. 데일리 급등락 리포트 자동 생성  
RAG 기반 기술을 활용해 특정 종목의 급등/급락 원인을 근거와 함께 자동 분석합니다.

- VectorDB 기반 뉴스 검색  
- 다각적 질의(계약, 정책, 투자, 규제 등)  
- 간결하면서도 근거를 포함한 리포트 자동 생성  

---

### 2. 뉴스 기반 파급력 및 연관 종목 예측  
특정 테마에서 주도주가 급등할 경우, 같은 테마 내 다른 종목의 상승 가능성을 예측합니다.

- CatBoost 모델 기반 확률 예측  
- 기술적 지표, 정성적 지표, 뉴스 감성·규모 지표 결합  
- 과거 뉴스-주가 반응 패턴 학습  
- 출력: 후보 종목의 상승 확률 (0~1)

---

### 3. 경제 뉴스 핵심 요약  
매일 업데이트되는 경제 뉴스를 핵심만 빠르게 파악할 수 있도록 자동 요약합니다.

- 전체 경제 뉴스 크롤링  
- 핵심 이슈 및 키워드 추출  
- 대표 기사 및 요약 제공  

---

## Pain Point 분석

### 기존의 어려움
- 상승/하락 원인을 직접 파악하기 어려움  
- 뉴스가 너무 많아 근거가 되는 뉴스만 선별하기 어려움  
- 연관 종목으로 파급되는 영향을 분석하기 어려움  

### UPssue의 해결책
- AI가 관련 뉴스 탐색, 원인 분석, 요약까지 자동 수행  
- 단순 요약이 아닌 근거 뉴스 중심 분석 제공  
- GNN 및 ML 기반 파급력 분석  
- 연관 종목 상승 가능성 자동 예측  

---

## 과제 목표

### 기술적 목표

| 항목 | 내용 |
|------|------|
| 급등락 종목 자동 감지 | KRX API 연동, 거래대금 10억 이상, 등락률 ±6% 필터링 |
| 뉴스 분석 | 네이버 뉴스 30건 이상 자동 수집, NER 및 LLM 기반 분석, RAG 구축 |
| 연관종목 예측 모델 | CatBoost 기반 모델, 기술/정성/뉴스 지표 결합 |
| 리포트 자동 생성 | BM25 + Dense Hybrid 검색, 메타데이터 구조화 |

---

### 정량적 목표

| 항목 | 목표 |
|------|-------|
| 뉴스 수집량 | 종목당 최근 3일 30건 이상 |
| 예측 모델 정확도 | 55~60% |
| 리포트 생성 시간 | 종목당 3분 이내 |
| 급등락 기준 | 거래대금 10억 이상, 등락률 ±6% |

---

## 기술 스택

### Backend  
FastAPI, PostgreSQL, SQLAlchemy, Alembic, RabbitMQ, Apache Kafka  

### AI/ML  
CatBoost, KR-FinBert-SC, KLUE-NER, ChromaDB, Pandas, Selenium, OpenAI API  

### Frontend  
Next.js, Typescript  

---

## 프로젝트 결과 화면

### 홈

### 1) 지금 뜨는 이슈

- 최근 리포트가 생성된 종목들을 기반으로 **워드 클라우드**를 구성합니다.  
- **붉은 계열 = 상승 종목**, **파란 계열 = 하락 종목**  
- **글자 크기 = 상대적 등락율(변동폭)**

→ 시장에서 어떤 종목이 주목받고 있는지 한눈에 파악할 수 있습니다.
<div align="center">
<img width="300" alt="image" src="https://github.com/user-attachments/assets/ec9a78d1-38b3-4747-8382-94daa26ee213" />
</div>

---

### 2) 지금 살펴볼 만한 이슈

#### ▸ 오늘의 경제 뉴스 요약

- 하루 동안 수집된 전체 경제 뉴스를 분석하여 주요 흐름과 경제 트렌드를 한 페이지에 요약합니다.

<div align="center">
<table>
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/2369a6d5-e569-468b-b28d-be731262b53f" width="250" />
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/6722fe46-cd9b-4641-815a-cf646b242c4c" width="250" />
    </td>
  </tr>
</table>
</div>

#### ▸ 핵심 키워드 Top 10  

- 경제 뉴스에서 가장 많이 등장하거나 의미적으로 중요한 키워드를 추출합니다.  
- 각 키워드에는 **설명(description)**이 함께 제공되며 해당 키워드가 의미하는 경제적 맥락을 이해할 수 있습니다.

<div align="center">
<img width="250"  alt="image" src="https://github.com/user-attachments/assets/43be0bb9-82fc-4af3-9359-e9ec04a5eecd" />
</div>

#### ▸ 대표 뉴스

- 오늘의 경제 뉴스 중 가장 영향력 있거나 주요 흐름을 대표할 수 있는 기사를 자동으로 선정하여 제공합니다.

<div align="center">
<img width="250" alt="image" src="https://github.com/user-attachments/assets/67544a86-9a77-4a31-9eab-9e8d2d53cb1e" />
</div>

---

### 리포트 상세 페이지

### 요약

- 해당 종목이 **상승(또는 하락)**한 원인을 한눈에 이해할 수 있도록 **핵심 요약(summary)**을 제공합니다.  
- 뉴스 기반 원인, 시장 영향, 관련 이슈 등이 포함됩니다.
  
<div align="center">
<table>
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/6987feba-b445-4367-a9ba-9c56216c70e7" width="250" />
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/94a6ff5d-e7bd-4a40-bf5c-8f4d3b442799" width="250" />
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/fee4eff2-eafc-4cc9-9c06-2936ac0f1e31" width="250" />
    </td>
  </tr>
</table>
</div>


---

### 2) 원인 분석

- 종목에 영향을 준 **구체적 뉴스 기사**,  
- **증거 문장(evidence)**,  
- **뉴스 원문 링크**,  
- **LLM 분석 결과(이벤트 유형, 영향, 근거)**  
등을 구조적으로 정리해 제공합니다.

→ 사용자는 “왜 이 종목이 움직였는가?”를 근거 기반으로 확인할 수 있습니다.

<div align="center">
<table>
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/510ebc97-a177-4e26-afc2-c26d8c86cb3b" width="250" />
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/d5537160-7b45-449a-bb8c-b86c1d2d7f0a" width="250" />
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/2676e8be-e70d-4f26-8225-bfefa99bffca" width="250" />
    </td>
  </tr>
</table>
</div>

---

### 3) 파급력 예측

- 특정 종목이 움직였을 때 관련 테마 종목들에 **얼마나 영향을 줄지(상승 가능성 등)**를 예측합니다.  

<div align="center">
<table>
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/ac104c2e-4900-4625-b45b-8b76b7e3febc" width="250" />
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/0a9b4a65-12cb-4271-af2c-cd0f52d268ac" width="250" />
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/f20681b9-d6d5-46b1-93a5-47b06cea85c5" width="250" />
    </td>
  </tr>
</table>
</div>

---

### 4) 파급 효과 

- Graph Neural Network(GNN) 기반 기업 관계 그래프를 활용해 **어떤 종목들이 연쇄적으로 영향을 받을 가능성이 있는지** 보여줍니다.  


<div align="center">
<table>
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/da971eff-5e75-4f7a-be72-fe6623cb8ecf" width="300" />
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/480a7745-ab24-4131-8499-85092ec7412f" width="300" />
    </td>
  </tr>
</table>
</div>

---

### 5) 분석 결과  

- 전체 분석의 메타 정보를 포함합니다.  
  - 분석된 뉴스 개수  
  - 이벤트 검출 개수
  - 신뢰 분포도
- 모델이 어떤 근거를 기반으로 리포트를 생성했는지 투명하게 제시합니다.

<div align="center">
<img width="250" alt="image" src="https://github.com/user-attachments/assets/27d45b60-104e-45a6-b98d-90f271e3e583" />
</div>

---


# 서비스 전체 동작 흐름

매일 일정 시각에 세 개의 파이프라인이 자동 실행됩니다.

1. AI 모델 예측  
2. 급등락 리포트 생성  
3. 경제 뉴스 요약  

---

# 1. AI 모델 예측 파이프라인

### 개요  
테마 내 주도주가 급등했을 때, 후보 종목의 상승 가능성을 예측하는 파이프라인입니다.

### 흐름
1. 급등/급락 종목 중 주도주 선별  
2. 주도주 관련 뉴스 수집  
3. LLM 기반 테마·규모 추출  
4. 테마 내 후보 종목 수집  
5. 후보 종목 기술적/정성적 지표 수집  
6. 뉴스 감성 분석  
7. CatBoost 예측 모델 실행  
8. 상승 확률 저장  

관련 Repo:  
https://github.com/catch-thema/ModelServingusingFastapi

---

# 2. 데일리 리포트 생성 파이프라인

### 개요  
주가 변동 원인과 파급력을 근거 기반으로 설명하는 자동 생성 파이프라인입니다.

### GNN 기반 관계 그래프 구축
- DART 사업보고서 수집  
- 공급, 고객, 경쟁, 기술 협력, 지배구조 등 관계 추출  
- 계열사 식별  
- 기업 관계 그래프 생성  

### 전체 파이프라인 흐름
1. 급등락 종목 감지  
2. 뉴스 크롤링  
3. NER 기반 핵심 개체 추출  
4. LLM 분석(요약, 맥락, 산업 영향 등)  
5. 벡터 임베딩 생성  
6. GNN 기반 파급력 분석  
7. 근거 뉴스 추출  
8. RAG + LLM 기반 리포트 생성  

상세 Repo:  
https://github.com/catch-thema/news-pipeline

---

# 3. 경제 뉴스 요약 파이프라인

### 흐름  
1. 주요 경제 뉴스 크롤링  
2. 핵심 이슈 요약  
3. 핵심 키워드 생성  
4. 대표 기사 선정  
5. 요약 리포트 저장

관련 Repo:  
https://github.com/catch-thema/news-pipeline

---

# 프로젝트 구조 

### 주요 저장소

| Repo | 설명 |
|------|------|
| https://github.com/catch-thema/catchtheme-BE-securities | 종목 데이터 수집 (DART, KRX 등), FastAPI 기반 서버 |
| https://github.com/catch-thema/news-pipeline | 전체 데이터 파이프라인, 리포트 생성 |
| https://github.com/catch-thema/ModelServingusingFastapi | 연관 종목 예측 모델 서빙 |
| https://github.com/catch-thema/corporate-relationship-gnn | GNN |





