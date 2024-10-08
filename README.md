This page is also provided in [English](README-en.md).

SK텔레콤은 사회적 가치 추구를 위한 다양한 사업을 진행하고 있습니다. 기업이 먼저 앞장서서 사회 속에 혼재된 사회적 이슈를 발굴하고, 이를 해결하기 위한 사회적 책임을 지는 것이 지속가능한 경영의 출발이라고 생각합니다.

2019년 4월부터 이 기술의 현지화를 위해 사회적 기업인 [테스트웍스](http://www.testworks.co.kr)와 협업하여 자발적으로 지원한 우리나라의 시각장애인들로부터 데이터를 수집하였고, 영문으로 공개된 [VizWiz 데이터셋](https://vizwiz.org/tasks-and-datasets/vqa/) 중 현지화가 가능한 일부를 한국어로 번역하여 시각적 질의응답 기술을 한국어로 학습시킬 수 있는 데이터셋을 만들었습니다.

# 논문

## AI for Social Good workshop at NeurIPS (Kim & Lim et al., 2019)

[PDF](https://drive.google.com/open?id=1CB9DwXTI1UqpsCEN9a5V9yOLS_T_HTu_)
![AI for Social Good workshop at NeurIPS](docs/assets/img/AISG_NeurIPS_2019_KVQA.png)

# 시각적 질의응답

시각적 질의응답은 이미지가 주어지고 그 이미지에 대한 질문이 주어졌을 때, 이미지를 이해하여 자연어로 질문에 대한 답을 주는 기술입니다.

![VQA](docs/assets/img/vqa.png)

# KVQA 데이터셋

KVQA 데이터셋은 T-Brain이 진행하는 사회적 가치 추구를 위한 프로젝트의 일환으로서, 한국형 시각적 질의응답(Visual Question Answering) 데이터셋입니다. KVQA 데이터셋은 한국 시각장애인들이 찍은 사진과 그 사진에 대한 질문과 서로 다른 열 명의 복수 답으로 구성되어 있습니다.
현재는 총 3만 건의 이미지와 질문, 그리고 30만 건의 답변으로 구성되어 있으나, 올해 말까지 10만 건의 이미지와 질문, 그리고 100만 건의 답변으로 증대할 예정입니다.
본 데이터셋은 교육 및 연구목적으로 사용이 가능하며, 자세한 내용은 첨부된 라이선스를 참조해주시기 바랍니다. KVQA 데이터셋을 통해 한국형 시각적 질의응답 기술 발전과 사회적 가치를 동시에 추구할 수 있기를 바랍니다.

데이터셋은 [HuggingFace hub](https://huggingface.co/datasets/skt/KVQA)를 통해 다운받으실 수 있습니다.

![Examples of KVQA](docs/assets/img/kvqa_examples.png)

## 통계

### v1.0 (2020년 1월)

|           | 전체 (%)      | 예/아니오 (%)  | 숫자 (%)      | 기타 (%)        | 답변불가능 (%)   |
|:----------|:-------------|:-------------|:-------------|:---------------|:--------------|
| 이미지 수   | 100,445 (100) | 6,124 (6.10) | 9,332 (9.29) | 69,069 (68.76) | 15,920 (15.85) |
| 질문 수     | 100,445 (100) | 6,124 (6.10) | 9,332 (9.29) | 69,069 (68.76) | 15,920 (15.85) |
| 답변 수     | 1,004,450 (100)| 61,240 (6.10)| 93,320 (9.29)| 690,690 (68.76)| 159,200 (15.85)| 

## 성능 측정

한 질문 당 열 명의 서로 다른 사람들로부터 수집된 답을 이용해 정확도를 측정합니다. 열 개의 답변 중 3개 이상을 맞추었다면 100%가 되며 3개 미만일 때 비례적으로 부분 점수를 획득합니다. 최종적으로 성능 보고를 할 때에는 10개의 답변 중 9개를 선택하는 서로 다른 정확도 측정을 10회 실시하여 평균 점수를 보고해야 합니다. 이 성능 측정은 [VQA Evaluation](https://visualqa.org/evaluation.html) 방법과 같습니다.

## 시각적 질의응답 데이터

### 데이터 항목 설명

| Name                             | Type     | Description                                              |
|:---------------------------------|:---------|:---------------------------------------------------------|
| VQA                              | `[dict]` | 시각적 질의응답 정보를 담은 `dict`의 `list`                     |
| +- image                         | `str`    | 이미지 파일의 이름                                           |
| +- source                        | `str`    | 데이터의 출처 `("kvqa", "vizwiz")`                          |
| +- answers                       | `[dict]` | 응답 정보를 담은 `dict` 10개의 `list`                         |
| +--- answer                      | `str`    | 시각적 질의에 대한 응답                                        |
| +--- answer_confidence           | `str`    | 응답에 대한 신뢰도 `("yes", "maybe", "no")`                   |
| +- question                      | `str`    | 이미지에 관련한 질의                                           |
| +- answerable                    | `int`    | 응답 가능 여부 `(0, 1)`                                       |
| +- answer_type                   | `str`    | 응답의 종류 `("number", "yes/no", "unanswerable", "other")`   |

### 데이터 예시

```json
[{
        "image": "KVQA_190712_00143.jpg",
        "source": "kvqa",
        "answers": [{
            "answer": "피아노",
            "answer_confidence": "yes"
        }, {
            "answer": "피아노",
            "answer_confidence": "yes"
        }, {
            "answer": "피아노 치고있다",
            "answer_confidence": "maybe"
        }, {
            "answer": "unanswerable",
            "answer_confidence": "maybe"
        }, {
            "answer": "게임",
            "answer_confidence": "maybe"
        }, {
            "answer": "피아노 앞에서 무언가를 보고 있음",
            "answer_confidence": "maybe"
        }, {
            "answer": "피아노치고있어",
            "answer_confidence": "maybe"
        }, {
            "answer": "피아노치고있어요",
            "answer_confidence": "maybe"
        }, {
            "answer": "피아노 연주",
            "answer_confidence": "maybe"
        }, {
            "answer": "피아노 치기",
            "answer_confidence": "yes"
        }],
        "question": "방에 있는 사람은 지금 뭘하고 있지?",
        "answerable": 1,
        "answer_type": "other"
    },
    {
        "image": "VizWiz_train_000000008148.jpg",
        "source": "vizwiz",
        "answers": [{
            "answer": "리모컨",
            "answer_confidence": "yes"
        }, {
            "answer": "리모컨",
            "answer_confidence": "yes"
        }, {
            "answer": "리모컨",
            "answer_confidence": "yes"
        }, {
            "answer": "티비 리모컨",
            "answer_confidence": "yes"
        }, {
            "answer": "리모컨",
            "answer_confidence": "yes"
        }, {
            "answer": "리모컨",
            "answer_confidence": "yes"
        }, {
            "answer": "리모컨",
            "answer_confidence": "yes"
        }, {
            "answer": "리모컨",
            "answer_confidence": "maybe"
        }, {
            "answer": "리모컨",
            "answer_confidence": "yes"
        }, {
            "answer": "리모컨",
            "answer_confidence": "yes"
        }],
        "question": "이것은 무엇인가요?",
        "answerable": 1,
        "answer_type": "other"
    }
]
```

# 라이선스

* [Korean VQA License](LICENSE) for the KVQA Dataset
* Creative Commons License Deed ([CC BY 4.0](https://creativecommons.org/licenses/by/4.0/deed.ko)) for the VizWiz subset
* GNU GPL v3.0 for the Code
