**[한국어](#ko) · [English](#en) · [中文](#zh) · [日本語](#ja) · [Oʻzbekcha](#uz) · [Русский](#ru)**

---

<a id="ko"></a>

# AI는 동작을 어떻게 알아보고 만들까?

새벽 두 시 골목 CCTV에서 시작하는 긴급 미션 다섯 개로, 동작 인식에서 동작 생성까지 처음부터 따라가는 인터랙티브 해설 시리즈입니다.
쓰레기를 던지는 사람을 막대 인형으로 바꿔 잡는 데서 출발해, 그 특징을 뒤집어 동작을 만들고, 인코더·디코더로 접었다 펼치고, 말과 동작을 같은 지도에 놓아, 마지막에는 "춤춰" 한 마디가 조수의 춤 영상이 되기까지를 다룹니다.

**바로 보기:** https://adminmrobo.github.io/motion_ai_series_01/

글 · 안상선 ((주)M-Robo 대표)

## 언어

한국어가 기본이며, 모든 페이지를 영어·중국어·일본어·우즈베크어·러시아어로도 볼 수 있습니다.

- **직접 고르기:** 각 페이지 맨 위 메뉴의 🌐 언어 선택 상자, 또는 오른쪽 아래 🌐 배너에서 고릅니다. 고른 언어는 브라우저가 기억합니다.
- **자동 전환:** 한국어 페이지에 처음 들어오면 브라우저 언어에 맞는 번역 페이지로 자동으로 옮겨 갑니다(지원하지 않는 언어는 한국어 그대로).
- **주소로 지정:** 주소 뒤에 `?lang=en`처럼 붙이면 그 언어로 엽니다 (`ko`, `en`, `zh`, `ja`, `uz`, `ru`).
- 5-4는 한국어 단어 조각 40개로 만든 장난감 모델을 다루므로, 어느 언어로 보아도 모델에 넣는 예시 문장과 단어 조각은 한국어로 두고 뜻을 괄호로 붙였습니다.

| 언어 | 파일 이름 | 바로 보기 |
|---|---|---|
| 한국어 (기본) | `index.html`, `5-1_cctv_litter.html` … | https://adminmrobo.github.io/motion_ai_series_01/ |
| English | `index.en.html`, `5-1_cctv_litter.en.html` … | https://adminmrobo.github.io/motion_ai_series_01/index.en.html |
| 中文 | `*.zh.html` | https://adminmrobo.github.io/motion_ai_series_01/index.zh.html |
| 日本語 | `*.ja.html` | https://adminmrobo.github.io/motion_ai_series_01/index.ja.html |
| Oʻzbekcha | `*.uz.html` | https://adminmrobo.github.io/motion_ai_series_01/index.uz.html |
| Русский | `*.ru.html` | https://adminmrobo.github.io/motion_ai_series_01/index.ru.html |

## 구성

| 편 | 제목 | 다루는 내용 | 난이도 |
|---|---|---|---|
| [5-1](https://adminmrobo.github.io/motion_ai_series_01/5-1_cctv_litter.html) | CCTV 쓰레기 투기 — 사람을 막대 인형으로 바꿔 잡는다 | 화면은 숫자, 객체 검출과 포즈 추정, 관절 13점, 동작 특징 4개, 규칙 대 학습, 라이브 관제실과 판정보류 | ★☆☆☆☆ |
| [5-2](https://adminmrobo.github.io/motion_ai_series_01/5-2_recognize_to_generate.html) | 알아보기에서 만들기로 — 특징 표의 화살표를 뒤집는다 | 판별 모델과 생성 모델, 동작은 표(46 × 26), 좌표 평균 대 각도 평균, 데이터 분포, 생성기 네 개와 감독관의 채점 | ★★☆☆☆ |
| [5-3](https://adminmrobo.github.io/motion_ai_series_01/5-3_encoder_decoder.html) | 인코더·디코더 — 동작을 접었다 펼친다 | 선형 오토인코더(PCA), 병목 크기, 잠재 지도와 손잡이(잠재 변수), 떨림 제거와 가림 복원, 적은 데이터로 탐지, 잠재 공간에서 생성 | ★★★☆☆ |
| [5-4](https://adminmrobo.github.io/motion_ai_series_01/5-4_text_to_motion.html) | 단어에서 동작으로 — 말과 몸짓을 같은 지도에 놓는다 | 단어 주머니, 대조 학습, 공유 지도, 문장으로 동작 찾기·만들기·이어 붙이기, 단어 주머니의 한계 | ★★★★☆ |
| [5-5](https://adminmrobo.github.io/motion_ai_series_01/5-5_prompt_to_dance.html) | "춤춰"에서 춤 영상으로 — 프롬프트가 조수의 춤이 되기까지 | 프롬프트에서 영상까지 여섯 단계, 포즈 맵과 포즈 기반 생성, 영상 재생기와 나란히 보기, 동작 일치율 재기, 시리즈 정리 | ★★★★★ |

순서대로 읽기를 권합니다. 앞 편의 막대 인형과 숫자를 다음 편이 이어 쓰지만, 각 편은 따로 읽어도 됩니다.

## 막대 인형이 걸어온 길

한 편의 결과가 다음 편의 재료가 됩니다.

| 편 | 들어가는 것 | 나오는 것 | 다음 편으로 넘기는 질문 |
|---|---|---|---|
| 5-1 | CCTV 화면 (숫자 6,220,800개) | 관절 26개 → 특징 4개 → "투기 / 정상" | 이 특징을 거꾸로 쓰면 동작을 만들 수 있을까? |
| 5-2 | 이름표 "던지기" | 숫자 1,196개짜리 동작 | 생성에 필요한 손잡이(잠재 변수)는 어디서 오나? |
| 5-3 | 동작 1,196개 숫자 | 손잡이 16개 → 다시 1,196개 | 말로 원하는 동작을 고를 수는 없을까? |
| 5-4 | 문장 "춤춰" | 공유 지도의 점 → 막대 인형의 춤 | 막대 인형에 사람의 모습을 입힐 수 있을까? |
| 5-5 | 막대 인형의 춤 + 조수 참조 이미지 | 조수의 춤 영상 | — |

## 각 편의 핵심 숫자

모두 각 편의 Colab 코드를 실제로 실행한 결과입니다.

| 편 | 숫자 | 뜻 |
|---|---|---|
| 5-1 | 60.7% → 99.7% | "손목이 빠르면 투기" 규칙 → 특징 4개 + 로지스틱 회귀의 시험 정확도 |
| 5-2 | 44.2% → 0.0% | 좌표마다 주사위를 굴린 생성기 → 손잡이 3개에서 뽑은 생성기의 뼈 길이 오차 |
| 5-3 | 99.8% | 숫자 1,196개를 16개로 접어도 남는 움직임(설명한 분산) |
| 5-4 | 1.90 → 0.01 | 대조 학습 400걸음 동안의 짝 맞추기 손실 |
| 5-5 | 77.6% → 100% | 같은 춤을 1초 늦게 따라 춘 일치율 → 시간을 맞춘 뒤의 일치율 |

## 각 편에 들어 있는 것

- 직접 조작하는 실습과 움직이는 다이어그램
- 초보자를 위한 풀이와 섹션별 확인 문제
- **Colab 코드 2개** — 복사, `.py` 내려받기, 노트북(`.ipynb`) 내려받기를 지원합니다. Colab 기본 라이브러리만 쓰며, 페이지에 실제 실행 결과를 실었습니다.
- AI 응용 프롬프트 (응용 분야 찾기, 해커톤 48시간 계획, 공모전 기획서 초안, 논문 실험 설계)
- 용어 정리 (본문의 점선 밑줄 말풍선과 같은 사전), 비유 모음과 비유가 틀리는 지점, 레퍼런스
- 교육자를 위한 TIP (운영안 세 가지, 섹션별 운영 포인트, 흔한 오해 Top 5, 확인 문제, Colab 과제)

편마다 들어 있는 주요 실습은 다음과 같습니다.

| 편 | 주요 실습 |
|---|---|
| 5-1 | CCTV 화면을 숫자로 보기, 검출 상자·관절·프라이버시 모드 켜고 끄기, 여섯 장면 재생, 규칙 기준값 실험, 라이브 관제실 |
| 5-2 | 판별·생성 화살표 뒤집기, 동작 표(46 × 26) 탐색, 두 동작 섞기(좌표 대 각도), 던지기 100개 분포, 생성기 네 개 채점 |
| 5-3 | 병목 크기 바꾸며 접었다 펴기, 잠재 지도와 손잡이 네 개, 떨림·가림 복원, 생성기 E |
| 5-4 | 단어 주머니 보기, 엉킨 선이 짝을 찾는 대조 학습 재생, 공유 지도, 문장으로 막대 인형 움직이기 |
| 5-5 | 여섯 단계 파이프라인, 노이즈에서 조수 그리기, 영상 재생기(나란히 보기·어긋남·좌우 뒤집기), 동작 일치율 실험 |

## Colab 코드

| 편 | 코드 1 | 코드 2 | 라이브러리 | 실행 시간 (CPU) |
|---|---|---|---|---|
| 5-1 | 막대 인형 장면을 만들고 특징 4개 뽑기 | 규칙 대 학습, 투기 탐지기 다섯 개 비교 | numpy, matplotlib, scikit-learn | 1초 미만 / 약 20초 |
| 5-2 | 동작은 표다, 섞으면 왜 부서지나 | 동작 생성기 네 개와 감독관의 채점표 | numpy, matplotlib | 1초 미만 / 약 10초 |
| 5-3 | 동작을 숫자 k개로 접었다 펼치기 (선형 오토인코더) | 접은 숫자로 투기 탐지와 동작 생성 높이기 | numpy, matplotlib, scikit-learn | 약 3초 / 약 40초 |
| 5-4 | 단어 주머니와 대조 학습 | 말을 넣으면 동작이 나온다 (찾기·만들기·이어 붙이기) | numpy | 약 5초 / 약 5초 |
| 5-5 | 동작 일치율은 어떻게 재나 (시간 맞추기, DTW) | 영상을 숫자로 뜯어보기 | numpy, OpenCV | 약 5초 / 약 3초 |

5-5 코드 2는 영상 파일 `match_score_video.mp4`가 필요합니다. `colab/` 폴더의 영상을 Colab 왼쪽 파일 창에 올린 뒤 실행하세요.

## 파일

```
index.html                       시리즈 목록 (미션 다섯 개)
5-1_cctv_litter.html             CCTV 쓰레기 투기
5-2_recognize_to_generate.html   알아보기에서 만들기로
5-3_encoder_decoder.html         인코더·디코더
5-4_text_to_motion.html          단어에서 동작으로
5-5_prompt_to_dance.html         "춤춰"에서 춤 영상으로 (영상 포함)
*.en.html *.zh.html *.ja.html   같은 페이지의 영어·중국어·일본어판
*.uz.html *.ru.html              같은 페이지의 우즈베크어·러시아어판
colab/                           (선택) 각 편의 Colab 코드 10개와 5-5 분석용 영상
```

각 HTML은 그림·영상·데이터·스크립트를 파일 안에 담고 있어 빌드 과정이 없습니다. 파일을 브라우저로 열기만 하면 됩니다(글꼴은 Google Fonts에서 불러오므로 인터넷이 없으면 기본 글꼴로 보입니다). 편끼리 이어지는 링크와 언어 전환은 모든 파일이 같은 폴더에 있을 때 작동하므로 파일 이름을 바꾸지 마세요. 번역판은 언어마다 파일이 하나씩 더 있을 뿐 크기는 한국어판과 같습니다.

| 파일 | 크기 | 참고 |
|---|---|---|
| index.html | 약 0.4MB | |
| 5-1 ~ 5-4 | 각 0.9 ~ 1.3MB | |
| 5-5_prompt_to_dance.html | 약 4.4MB | 춤 영상(10초, H.264 + AAC)을 파일 안에 담고 있습니다. 영상을 따로 올릴 필요가 없습니다 |

본문에서 앞선 시리즈로 가는 링크는 각 시리즈의 사이트로 바로 연결되며 새 탭에서 열립니다. 3-x 편은 [딥러닝 A to Z (AI_Model_Review)](https://adminmrobo.github.io/AI_Model_Review/), 4-x 편은 [AI는 이미지를 어떻게 구분할까? (AI_image_classification)](https://adminmrobo.github.io/AI_image_classification/)입니다.

## 먼저 읽으면 좋은 편

이 시리즈는 [딥러닝 A to Z](https://adminmrobo.github.io/AI_Model_Review/)(3-x)와 [AI는 이미지를 어떻게 구분할까?](https://adminmrobo.github.io/AI_image_classification/)(4-x)에 이어지는 편입니다.

| 이 시리즈 | 먼저 읽으면 좋은 편 | 이유 |
|---|---|---|
| 5-1 | [4-2 고양이 vs 사람](https://adminmrobo.github.io/AI_image_classification/4-2_cat_human.html) | 사진이 숫자 행렬이 되는 과정 |
| 5-1 | [3-7 순서 모델](https://adminmrobo.github.io/AI_Model_Review/3-7_sequence_models.html) | 막대 인형이 시간 순서를 가진 데이터(시계열)가 된다 |
| 5-3 | [3-7 순서 모델 · 오토인코더](https://adminmrobo.github.io/AI_Model_Review/3-7_sequence_models.html#ae) | 신경망으로 만든 인코더·디코더 |
| 5-4 | [3-5 텍스트](https://adminmrobo.github.io/AI_Model_Review/3-5_text.html), [3-8 어텐션·트랜스포머](https://adminmrobo.github.io/AI_Model_Review/3-8_attention_transformer.html) | 단어 주머니보다 좋은 텍스트 인코더 |
| 5-5 | [3-3 이미지와 CNN](https://adminmrobo.github.io/AI_Model_Review/3-3_image_cnn.html) | 영상 생성 모델이 그림을 다루는 바탕 |

## 데이터와 이미지

- 연구실 식구들(박사·조수·초파리 연구원·연구실 로봇), 막대 인형 캐릭터 시트, 장면 그림, 조수 캐릭터 시트·표정 시트, 컷 시트, 춤 영상은 저자가 직접 만든 것입니다.
- 막대 인형 동작(넣기·던지기·지나가기·손 흔들기·줍기·떨어뜨리기·춤추기)과 동작 설명 문장은 모두 **합성 데이터**입니다. 관절 각도를 시간에 따라 바꿔 만들었고, 실제 사람을 촬영한 데이터는 쓰지 않았습니다.
- 페이지 속 계산(동작 생성, 특징, 인코더·디코더, 대조 학습, 일치율)은 Colab 코드와 같은 계산입니다. 브라우저에서 난수를 다시 뽑는 실습은 숫자가 조금 다를 수 있으며, 표의 숫자는 코드를 실제로 실행한 결과입니다.
- 일부 그림과 값은 설명용 모형입니다. 각 편 푸터의 "설명용 모형인 것"에 무엇이 실제 계산이고 무엇이 예시인지 적어 두었습니다.

| 편 | 설명용 모형인 것 |
|---|---|
| 5-1 | 검출 상자의 확신도(0.94 등)는 예시값, 관절 좌표는 그림에서 읽어 옮긴 값 |
| 5-3 | 손잡이 별명은 저자의 해석 |
| 5-5 | 노이즈 그림은 완성된 프레임에 노이즈를 섞어 보인 것. 일치율 실험은 설명용 안무로 계산한 것이며, 영상 속 76.5%를 다시 계산한 것이 아님 |

## 용어 표기

이 시리즈는 잠재 변수(latent variable)를 **손잡이(잠재 변수)** 라고 부릅니다. 돌리면 데이터 전체가 함께 바뀌는 소수의 숫자라는 비유이며, 영어권 해설에서도 잠재 공간의 각 차원을 "knob(손잡이)", "dial(다이얼)", "slider(슬라이더)"라고 부르곤 합니다. 논문의 정식 용어는 잠재 변수이고, 5-3에서 데이터가 찾은 손잡이 하나하나는 주성분(principal component)입니다.

## 라이선스

이 저작물은 [크리에이티브 커먼즈 저작자표시-비영리 4.0 국제 라이선스(CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/deed.ko)로 공개합니다.
비상업적 목적에 한해 자유롭게 공유하고 고쳐 쓸 수 있으며, **출처는 반드시 표기**해야 합니다.

출처 표기 예: 안상선, 「AI는 동작을 어떻게 알아보고 만들까? · 5-1 CCTV 쓰레기 투기」, AI Model Review.

---

<a id="en"></a>

# How Does AI Recognize and Create Motion?

An interactive explainer series that follows motion AI from recognition all the way to generation, through five emergency missions that begin with an alley CCTV camera at 2 a.m.
It starts by turning a person who throws litter into a stick figure to catch them, then flips those features around to create motion, folds and unfolds motion with an encoder and decoder, places words and motion on the same map, and finally shows how a single word, "Dance!", becomes a video of the Assistant dancing.

**View online:** https://adminmrobo.github.io/motion_ai_series_01/index.en.html

Written by Ahn Sangsun (CEO, M-Robo Co., Ltd.)

## Languages

Korean is the default, and every page is also available in English, Chinese, Japanese, Uzbek and Russian.

- **Choose yourself:** use the 🌐 language selector in the menu at the top of each page, or the 🌐 banner in the bottom-right corner. Your browser remembers the language you choose.
- **Automatic switching:** the first time you open a Korean page, you are automatically taken to the translated page that matches your browser language (unsupported languages stay in Korean).
- **Set it in the address:** add something like `?lang=en` to the end of the address to open the page in that language (`ko`, `en`, `zh`, `ja`, `uz`, `ru`).
- 5-4 works with a toy model built from 40 Korean word pieces, so in every language the example sentences and word pieces fed into the model stay in Korean, with their meaning added in parentheses.

| Language | File names | View online |
|---|---|---|
| 한국어 (default) | `index.html`, `5-1_cctv_litter.html` … | https://adminmrobo.github.io/motion_ai_series_01/ |
| English | `index.en.html`, `5-1_cctv_litter.en.html` … | https://adminmrobo.github.io/motion_ai_series_01/index.en.html |
| 中文 | `*.zh.html` | https://adminmrobo.github.io/motion_ai_series_01/index.zh.html |
| 日本語 | `*.ja.html` | https://adminmrobo.github.io/motion_ai_series_01/index.ja.html |
| Oʻzbekcha | `*.uz.html` | https://adminmrobo.github.io/motion_ai_series_01/index.uz.html |
| Русский | `*.ru.html` | https://adminmrobo.github.io/motion_ai_series_01/index.ru.html |

## Contents

| Part | Title | Topics | Level |
|---|---|---|---|
| [5-1](https://adminmrobo.github.io/motion_ai_series_01/5-1_cctv_litter.en.html) | CCTV Littering — Turning People into Stick Figures to Catch Them | The screen is numbers, object detection and pose estimation, 13 joints, 4 motion features, rules vs. learning, the live control room and abstaining ("no call") | ★☆☆☆☆ |
| [5-2](https://adminmrobo.github.io/motion_ai_series_01/5-2_recognize_to_generate.en.html) | From Recognizing to Creating — Flipping the Arrow of the Feature Table | Discriminative and generative models, motion is a table (46 × 26), averaging coordinates vs. averaging angles, data distributions, four generators scored by the Evaluator | ★★☆☆☆ |
| [5-3](https://adminmrobo.github.io/motion_ai_series_01/5-3_encoder_decoder.en.html) | Encoder · Decoder — Folding and Unfolding Motion | Linear autoencoder (PCA), bottleneck size, the latent map and knobs (latent variables), removing jitter and restoring occlusion, detection with little data, generating in latent space | ★★★☆☆ |
| [5-4](https://adminmrobo.github.io/motion_ai_series_01/5-4_text_to_motion.en.html) | From Words to Motion — Placing Words and Gestures on the Same Map | Bag of words, contrastive learning, the shared map, finding, making and stitching motion from sentences, limits of the bag of words | ★★★★☆ |
| [5-5](https://adminmrobo.github.io/motion_ai_series_01/5-5_prompt_to_dance.en.html) | From "Dance!" to a Dance Video — How a Prompt Becomes the Assistant’s Dance | Six steps from prompt to video, pose maps and pose-guided generation, the video player and side-by-side view, measuring the motion match score, series wrap-up | ★★★★★ |

We recommend reading in order. Each part reuses the stick figures and numbers from the previous one, but every part can also be read on its own.

## The stick figure's journey

The output of one part becomes the input of the next.

| Part | Goes in | Comes out | Question passed to the next part |
|---|---|---|---|
| 5-1 | CCTV screen (6,220,800 numbers) | 26 joints → 4 features → "Littering / Normal" | If we use these features in reverse, can we create motion? |
| 5-2 | The label "throw" | A motion made of 1,196 numbers | Where do the knobs (latent variables) needed for generation come from? |
| 5-3 | A motion of 1,196 numbers | 16 knobs → back to 1,196 | Could we choose the motion we want with words? |
| 5-4 | The sentence "Dance!" | A point on the shared map → a stick-figure dance | Can we dress the stick figure up as a person? |
| 5-5 | The stick-figure dance + a reference image of the Assistant | A video of the Assistant dancing | — |

## Key numbers from each part

All of them are results from actually running each part's Colab code.

| Part | Number | Meaning |
|---|---|---|
| 5-1 | 60.7% → 99.7% | Test accuracy of the rule "a fast wrist means littering" → 4 features + logistic regression |
| 5-2 | 44.2% → 0.0% | Bone-length error of a generator that rolls dice for every coordinate → a generator that samples from 3 knobs |
| 5-3 | 99.8% | Movement that remains even after folding 1,196 numbers into 16 (explained variance) |
| 5-4 | 1.90 → 0.01 | Pair-matching loss over 400 steps of contrastive learning |
| 5-5 | 77.6% → 100% | Match score for the same dance performed 1 second late → match score after aligning in time |

## What each part includes

- Hands-on interactive exercises and animated diagrams
- Beginner-friendly explanations and check questions for each section
- **2 Colab code notebooks** — with Copy, Download `.py` and Download notebook (`.ipynb`). They use only Colab's built-in libraries, and the page shows the actual run results.
- AI prompts for applications (finding application areas, a 48-hour hackathon plan, a draft competition proposal, designing experiments for a paper)
- Glossary (the same dictionary as the dotted-underline tooltips in the text), a collection of analogies and where the analogy breaks, references
- Tips for educators (three lesson plans, teaching points for each section, Top 5 common misconceptions, check questions, Colab assignments)

The main hands-on exercises in each part are:

| Part | Main exercises |
|---|---|
| 5-1 | Viewing the CCTV screen as numbers, toggling detection boxes, joints and privacy mode, playing six scenes, experimenting with rule thresholds, the live control room |
| 5-2 | Flipping the discriminative/generative arrow, exploring the motion table (46 × 26), blending two motions (coordinates vs. angles), the distribution of 100 throws, scoring four generators |
| 5-3 | Folding and unfolding while changing the bottleneck size, the latent map and four knobs, restoring jitter and occlusion, generator E |
| 5-4 | Viewing the bag of words, replaying contrastive learning as tangled lines find their pairs, the shared map, moving a stick figure with a sentence |
| 5-5 | The six-step pipeline, drawing the Assistant out of noise, the video player (side-by-side view, offset, mirror flip), motion match score experiments |

## Colab code

| Part | Code 1 | Code 2 | Libraries | Run time (CPU) |
|---|---|---|---|---|
| 5-1 | Building stick-figure scenes and extracting 4 features | Rules vs. learning: comparing five littering detectors | numpy, matplotlib, scikit-learn | under 1 s / about 20 s |
| 5-2 | Motion is a table — why does blending break it? | Four motion generators and the Evaluator's score sheet | numpy, matplotlib | under 1 s / about 10 s |
| 5-3 | Folding and unfolding motion into k numbers (linear autoencoder) | Improving littering detection and motion generation with the folded numbers | numpy, matplotlib, scikit-learn | about 3 s / about 40 s |
| 5-4 | Bag of words and contrastive learning | Put words in, get motion out (find · make · stitch) | numpy | about 5 s / about 5 s |
| 5-5 | How do we measure the motion match score? (time alignment, DTW) | Taking a video apart into numbers | numpy, OpenCV | about 5 s / about 3 s |

5-5 Code 2 needs the video file `match_score_video.mp4`. Upload the video from the `colab/` folder to the file panel on the left side of Colab, then run it.

## Files

```
index.html                       Series list (five missions)
5-1_cctv_litter.html             CCTV Littering
5-2_recognize_to_generate.html   From Recognizing to Creating
5-3_encoder_decoder.html         Encoder · Decoder
5-4_text_to_motion.html          From Words to Motion
5-5_prompt_to_dance.html         From "Dance!" to a Dance Video (includes video)
*.en.html *.zh.html *.ja.html   English, Chinese and Japanese versions of the same pages
*.uz.html *.ru.html              Uzbek and Russian versions of the same pages
colab/                           (optional) the 10 Colab code files and the video for 5-5 analysis
```

Each HTML file contains its images, video, data and scripts inside the file, so there is no build step. Just open the file in a browser (fonts are loaded from Google Fonts, so without an internet connection the default fonts are shown). Links between parts and language switching work only when all files are in the same folder, so do not rename the files. The translated versions simply add one file per language; their sizes are the same as the Korean versions.

| File | Size | Notes |
|---|---|---|
| index.html | about 0.4MB | |
| 5-1 ~ 5-4 | 0.9 ~ 1.3MB each | |
| 5-5_prompt_to_dance.html | about 4.4MB | The dance video (10 s, H.264 + AAC) is embedded in the file, so there is no need to upload the video separately |

Links in the text to earlier series go directly to each series' site and open in a new tab. The 3-x parts are [Deep Learning A to Z (AI_Model_Review)](https://adminmrobo.github.io/AI_Model_Review/), and the 4-x parts are [How Does AI Tell Images Apart? (AI_image_classification)](https://adminmrobo.github.io/AI_image_classification/).

## Recommended background reading

This series follows [Deep Learning A to Z](https://adminmrobo.github.io/AI_Model_Review/) (3-x) and [How Does AI Tell Images Apart?](https://adminmrobo.github.io/AI_image_classification/) (4-x).

| This series | Recommended reading first | Why |
|---|---|---|
| 5-1 | [4-2 Cat vs. Human](https://adminmrobo.github.io/AI_image_classification/4-2_cat_human.html) | How a photo becomes a matrix of numbers |
| 5-1 | [3-7 Sequence Models](https://adminmrobo.github.io/AI_Model_Review/3-7_sequence_models.html) | The stick figure becomes data ordered in time (a time series) |
| 5-3 | [3-7 Sequence Models · Autoencoder](https://adminmrobo.github.io/AI_Model_Review/3-7_sequence_models.html#ae) | Encoders and decoders built with neural networks |
| 5-4 | [3-5 Text](https://adminmrobo.github.io/AI_Model_Review/3-5_text.html), [3-8 Attention · Transformer](https://adminmrobo.github.io/AI_Model_Review/3-8_attention_transformer.html) | Text encoders better than the bag of words |
| 5-5 | [3-3 Images and CNNs](https://adminmrobo.github.io/AI_Model_Review/3-3_image_cnn.html) | The foundation for how video generation models handle images |

## Data and images

- The lab crew (the Doctor, the Assistant, the Fruit Fly Researcher, the Lab Robot), the stick-figure character sheet, scene illustrations, the Assistant's character sheet and expression sheet, cut sheets and the dance video were all created by the author.
- The stick-figure motions (putting in, throwing, walking past, waving, picking up, dropping, dancing) and the motion description sentences are all **synthetic data**. They were made by changing joint angles over time; no footage of real people was used.
- The calculations on the pages (motion generation, features, encoder · decoder, contrastive learning, match score) are the same calculations as in the Colab code. Exercises that draw new random numbers in the browser may give slightly different numbers; the numbers in the tables are results from actually running the code.
- Some images and values are illustrative mock-ups. The "what is an illustrative mock-up" note in each part's footer explains what is a real calculation and what is an example.

| Part | What is an illustrative mock-up |
|---|---|
| 5-1 | Detection-box confidence scores (0.94, etc.) are example values; joint coordinates were read off the illustrations |
| 5-3 | The knob nicknames are the author's interpretation |
| 5-5 | The noise images show noise mixed into the finished frames. The match score experiment is computed on an illustrative choreography and is not a recalculation of the 76.5% in the video |

## Terminology

This series calls latent variables **knobs (latent variables)**. The analogy is a small set of numbers that, when turned, change the whole piece of data together; English-language explanations also often call each dimension of a latent space a "knob", "dial" or "slider". The formal term in papers is latent variable, and each knob the data finds in 5-3 is a principal component.

## License

This work is released under the [Creative Commons Attribution-NonCommercial 4.0 International License (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/deed.en).
You may freely share and adapt it for non-commercial purposes only, and **you must give attribution**.

Example attribution: Ahn Sangsun, "How Does AI Recognize and Create Motion? · 5-1 CCTV Littering", AI Model Review.

---

<a id="zh"></a>

# AI 如何识别动作，又如何生成动作？

这是一个交互式讲解系列：从凌晨两点小巷 CCTV 里开始的五个紧急任务出发，带你从零走完从动作识别到动作生成的全过程。
从把乱扔垃圾的人变成火柴人抓住开始，再把这些特征反过来用于生成动作，用编码器·解码器把动作折叠再展开，把语言和动作放在同一张地图上，最后一直讲到一句“跳舞！”如何变成助手的舞蹈视频。

**在线查看：** https://adminmrobo.github.io/motion_ai_series_01/index.zh.html

作者 · Ahn Sangsun（M-Robo 株式会社代表）

## 语言

默认语言为韩语，所有页面也提供英语、中文、日语、乌兹别克语和俄语版本。

- **手动选择：** 在每个页面顶部菜单的 🌐 语言选择框，或右下角的 🌐 横幅中选择。浏览器会记住所选语言。
- **自动切换：** 首次进入韩语页面时，会自动跳转到与浏览器语言对应的翻译页面（不支持的语言则保持韩语）。
- **通过网址指定：** 在网址后加上 `?lang=en` 这样的参数，即可以该语言打开（`ko`、`en`、`zh`、`ja`、`uz`、`ru`）。
- 5-4 讲的是用 40 个韩语词语片段构建的玩具模型，因此无论以哪种语言浏览，输入模型的韩语例句和词语片段都保留韩语，并在括号中附上含义。

| 语言 | 文件名 | 在线查看 |
|---|---|---|
| 한국어（默认） | `index.html`, `5-1_cctv_litter.html` … | https://adminmrobo.github.io/motion_ai_series_01/ |
| English | `index.en.html`, `5-1_cctv_litter.en.html` … | https://adminmrobo.github.io/motion_ai_series_01/index.en.html |
| 中文 | `*.zh.html` | https://adminmrobo.github.io/motion_ai_series_01/index.zh.html |
| 日本語 | `*.ja.html` | https://adminmrobo.github.io/motion_ai_series_01/index.ja.html |
| Oʻzbekcha | `*.uz.html` | https://adminmrobo.github.io/motion_ai_series_01/index.uz.html |
| Русский | `*.ru.html` | https://adminmrobo.github.io/motion_ai_series_01/index.ru.html |

## 构成

| 篇 | 标题 | 主要内容 | 难度 |
|---|---|---|---|
| [5-1](https://adminmrobo.github.io/motion_ai_series_01/5-1_cctv_litter.zh.html) | CCTV 乱扔垃圾 —— 把人变成火柴人来抓 | 画面就是数字，目标检测与姿态估计，13 个关节点，4 个动作特征，规则 vs 学习，实时监控室与暂不判定 | ★☆☆☆☆ |
| [5-2](https://adminmrobo.github.io/motion_ai_series_01/5-2_recognize_to_generate.zh.html) | 从识别到生成 — 把特征表的箭头反过来 | 判别模型与生成模型，动作是一张表（46 × 26），坐标平均 vs 角度平均，数据分布，四个生成器与评审员的评分 | ★★☆☆☆ |
| [5-3](https://adminmrobo.github.io/motion_ai_series_01/5-3_encoder_decoder.zh.html) | 编码器·解码器 — 把动作折叠再展开 | 线性自编码器（PCA），瓶颈大小，潜在地图与旋钮（潜变量），去除抖动与遮挡恢复，用少量数据检测，在潜在空间中生成 | ★★★☆☆ |
| [5-4](https://adminmrobo.github.io/motion_ai_series_01/5-4_text_to_motion.zh.html) | 从词语到动作 — 把语言和动作放在同一张地图上 | 词袋，对比学习，共享地图，用句子查找 · 生成 · 拼接动作，词袋的局限 | ★★★★☆ |
| [5-5](https://adminmrobo.github.io/motion_ai_series_01/5-5_prompt_to_dance.zh.html) | 从“跳舞！”到舞蹈视频 — 提示词如何变成助手的舞蹈 | 从提示词到视频的六个步骤，姿态图与基于姿态的生成，视频播放器与并排查看，测量动作一致率，系列总结 | ★★★★★ |

建议按顺序阅读。后一篇会接着使用前一篇的火柴人和数字，但每一篇也可以单独阅读。

## 火柴人走过的路

每一篇的结果都会成为下一篇的材料。

| 篇 | 输入 | 输出 | 留给下一篇的问题 |
|---|---|---|---|
| 5-1 | CCTV 画面（6,220,800 个数字） | 26 个关节 → 4 个特征 → “乱扔 / 正常” | 把这些特征反过来用，能生成动作吗？ |
| 5-2 | 标签“扔” | 由 1,196 个数字组成的动作 | 生成所需的旋钮（潜变量）从哪里来？ |
| 5-3 | 动作的 1,196 个数字 | 16 个旋钮 → 再还原为 1,196 个 | 能不能用语言挑选想要的动作？ |
| 5-4 | 句子“跳舞！” | 共享地图上的点 → 火柴人的舞蹈 | 能不能给火柴人穿上人的样子？ |
| 5-5 | 火柴人的舞蹈 + 助手参考图像 | 助手的舞蹈视频 | — |

## 各篇的关键数字

以下均为实际运行各篇 Colab 代码得到的结果。

| 篇 | 数字 | 含义 |
|---|---|---|
| 5-1 | 60.7% → 99.7% | “手腕快就是乱扔”规则 → 4 个特征 + 逻辑回归的测试准确率 |
| 5-2 | 44.2% → 0.0% | 每个坐标都掷骰子的生成器 → 从 3 个旋钮中抽样的生成器的骨长误差 |
| 5-3 | 99.8% | 把 1,196 个数字折叠成 16 个后仍保留的运动（解释方差） |
| 5-4 | 1.90 → 0.01 | 对比学习 400 步过程中的配对损失 |
| 5-5 | 77.6% → 100% | 晚 1 秒跟跳同一支舞的一致率 → 对齐时间后的一致率 |

## 每篇包含的内容

- 可亲手操作的练习和动态示意图
- 面向初学者的讲解和各小节的练习题
- **2 段 Colab 代码** —— 支持复制、下载 `.py`、下载笔记本（`.ipynb`）。只使用 Colab 自带的库，页面中附有实际运行结果。
- AI 应用提示词（寻找应用领域、黑客松 48 小时计划、竞赛策划书初稿、论文实验设计）
- 术语表（与正文中虚线下划线气泡相同的词典）、比喻合集与比喻失效之处、参考文献
- 教师指南（三种课程方案、各小节教学要点、常见误解 Top 5、练习题、Colab 作业）

各篇的主要练习如下。

| 篇 | 主要练习 |
|---|---|
| 5-1 | 把 CCTV 画面看成数字，开关检测框 · 关节 · 隐私模式，播放六个场景，规则阈值实验，实时监控室 |
| 5-2 | 反转判别 · 生成箭头，探索动作表（46 × 26），混合两个动作（坐标 vs 角度），100 个“扔”的分布，为四个生成器评分 |
| 5-3 | 改变瓶颈大小来折叠再展开，潜在地图与四个旋钮，抖动 · 遮挡恢复，生成器 E |
| 5-4 | 查看词袋，播放缠在一起的线条找到配对的对比学习过程，共享地图，用句子让火柴人动起来 |
| 5-5 | 六步流水线，从噪声中画出助手，视频播放器（并排查看 · 错位 · 左右翻转），动作一致率实验 |

## Colab 代码

| 篇 | 代码 1 | 代码 2 | 库 | 运行时间（CPU） |
|---|---|---|---|---|
| 5-1 | 生成火柴人场景并提取 4 个特征 | 规则 vs 学习，比较五个乱扔垃圾检测器 | numpy, matplotlib, scikit-learn | 不到 1 秒 / 约 20 秒 |
| 5-2 | 动作是一张表，为什么一混合就会散架 | 四个动作生成器与评审员的评分表 | numpy, matplotlib | 不到 1 秒 / 约 10 秒 |
| 5-3 | 把动作折叠成 k 个数字再展开（线性自编码器） | 用折叠后的数字提升乱扔检测与动作生成 | numpy, matplotlib, scikit-learn | 约 3 秒 / 约 40 秒 |
| 5-4 | 词袋与对比学习 | 输入语言就输出动作（查找 · 生成 · 拼接） | numpy | 约 5 秒 / 约 5 秒 |
| 5-5 | 动作一致率怎么测（时间对齐，DTW） | 把视频拆成数字来看 | numpy, OpenCV | 约 5 秒 / 约 3 秒 |

5-5 的代码 2 需要视频文件 `match_score_video.mp4`。请先把 `colab/` 文件夹中的视频上传到 Colab 左侧的文件窗格，再运行。

## 文件

```
index.html                       系列目录（五个任务）
5-1_cctv_litter.html             CCTV 乱扔垃圾
5-2_recognize_to_generate.html   从识别到生成
5-3_encoder_decoder.html         编码器·解码器
5-4_text_to_motion.html          从词语到动作
5-5_prompt_to_dance.html         从“跳舞！”到舞蹈视频（含视频）
*.en.html *.zh.html *.ja.html   同一页面的英语 · 中文 · 日语版
*.uz.html *.ru.html              同一页面的乌兹别克语 · 俄语版
colab/                           （可选）各篇的 10 段 Colab 代码和 5-5 分析用视频
```

每个 HTML 文件都把图片、视频、数据和脚本包含在文件内部，无需构建。只要用浏览器打开文件即可（字体从 Google Fonts 加载，没有网络时会以默认字体显示）。篇与篇之间的链接和语言切换只有在所有文件位于同一文件夹时才能正常工作，所以请不要修改文件名。翻译版只是每种语言多出一个文件，大小与韩语版相同。

| 文件 | 大小 | 备注 |
|---|---|---|
| index.html | 约 0.4MB | |
| 5-1 ~ 5-4 | 各 0.9 ~ 1.3MB | |
| 5-5_prompt_to_dance.html | 约 4.4MB | 舞蹈视频（10 秒，H.264 + AAC）包含在文件内，无需另外上传视频 |

正文中指向前面系列的链接会直接连到各系列的网站，并在新标签页中打开。3-x 篇是 [深度学习 A to Z (AI_Model_Review)](https://adminmrobo.github.io/AI_Model_Review/)，4-x 篇是 [AI 如何区分图像？ (AI_image_classification)](https://adminmrobo.github.io/AI_image_classification/)。

## 建议先读的篇目

本系列承接 [深度学习 A to Z](https://adminmrobo.github.io/AI_Model_Review/)（3-x）和 [AI 如何区分图像？](https://adminmrobo.github.io/AI_image_classification/)（4-x）。

| 本系列 | 建议先读的篇目 | 理由 |
|---|---|---|
| 5-1 | [4-2 猫 vs 人](https://adminmrobo.github.io/AI_image_classification/4-2_cat_human.html) | 照片如何变成数字矩阵 |
| 5-1 | [3-7 序列模型](https://adminmrobo.github.io/AI_Model_Review/3-7_sequence_models.html) | 火柴人变成带有时间顺序的数据（时间序列） |
| 5-3 | [3-7 序列模型 · 自编码器](https://adminmrobo.github.io/AI_Model_Review/3-7_sequence_models.html#ae) | 用神经网络构建的编码器·解码器 |
| 5-4 | [3-5 文本](https://adminmrobo.github.io/AI_Model_Review/3-5_text.html), [3-8 注意力 · Transformer](https://adminmrobo.github.io/AI_Model_Review/3-8_attention_transformer.html) | 比词袋更好的文本编码器 |
| 5-5 | [3-3 图像与 CNN](https://adminmrobo.github.io/AI_Model_Review/3-3_image_cnn.html) | 视频生成模型处理图像的基础 |

## 数据与图像

- 研究室成员（博士 · 助手 · 果蝇研究员 · 研究室机器人）、火柴人角色设定图、场景插图、助手角色设定图 · 表情设定图、分镜图和舞蹈视频均由作者亲自制作。
- 火柴人动作（放入 · 扔 · 路过 · 挥手 · 捡起 · 掉落 · 跳舞）和动作描述句子全部是**合成数据**。它们是通过让关节角度随时间变化生成的，没有使用任何实际拍摄真人的数据。
- 页面中的计算（动作生成、特征、编码器·解码器、对比学习、一致率）与 Colab 代码中的计算相同。在浏览器中重新抽取随机数的练习，数字可能略有不同；表格中的数字是实际运行代码得到的结果。
- 部分插图和数值是仅供说明的示意。各篇页脚的“仅供说明的示意部分”中写明了哪些是实际计算、哪些是示例。

| 篇 | 仅供说明的示意部分 |
|---|---|
| 5-1 | 检测框的置信度（0.94 等）为示例值，关节坐标是从插图中读取后转录的数值 |
| 5-3 | 旋钮的昵称是作者的解读 |
| 5-5 | 噪声图是在完成的帧上混入噪声来展示的。一致率实验是用说明用的编舞计算的，并不是重新计算视频中的 76.5% |

## 术语说明

本系列把潜变量（latent variable）称为**旋钮（潜变量）**。这个比喻是指：只要转动少数几个数字，整份数据就会一起变化。英语圈的讲解中也常把潜在空间的每个维度称为“knob（旋钮）”“dial（拨盘）”“slider（滑块）”。论文中的正式术语是潜变量，而 5-3 中由数据找到的每一个旋钮就是主成分（principal component）。

## 许可协议

本作品以[知识共享 署名-非商业性使用 4.0 国际许可协议（CC BY-NC 4.0）](https://creativecommons.org/licenses/by-nc/4.0/deed.zh-hans)发布。
仅限非商业用途，可自由分享和改编，但**必须注明出处**。

出处标注示例：Ahn Sangsun，《AI 如何识别动作，又如何生成动作？ · 5-1 CCTV 乱扔垃圾》，AI Model Review。

---

<a id="ja"></a>

# AIは動作をどう見分け、どう作り出すのか？

午前2時の路地のCCTVから始まる5つの緊急ミッションで、動作認識から動作生成までを一から追いかけるインタラクティブ解説シリーズである。
ゴミを投げ捨てる人を棒人間に変えてとらえるところから出発し、その特徴を逆にたどって動作を作り、エンコーダ・デコーダで畳んでは広げ、言葉と動作を同じ地図に置き、最後には「踊って」のひと言が助手のダンス動画になるまでを扱う。

**すぐに見る:** https://adminmrobo.github.io/motion_ai_series_01/index.ja.html

文・アン・サンソン（株式会社M-Robo代表）

## 言語

韓国語が基本で、すべてのページを英語・中国語・日本語・ウズベク語・ロシア語でも読める。

- **自分で選ぶ:** 各ページ最上部のメニューにある 🌐 言語選択ボックス、または右下の 🌐 バナーから選ぶ。選んだ言語はブラウザが記憶する。
- **自動切り替え:** 韓国語ページに初めてアクセスすると、ブラウザの言語に合った翻訳ページへ自動的に移動する（対応していない言語の場合は韓国語のまま）。
- **アドレスで指定:** アドレスの後ろに `?lang=en` のように付けると、その言語で開く（`ko`, `en`, `zh`, `ja`, `uz`, `ru`）。
- 5-4は韓国語の単語のかけら40個で作ったおもちゃのモデルを扱うため、どの言語で見ても、モデルに入れる例文と単語のかけらは韓国語のままにし、意味を括弧で添えている。

| 言語 | ファイル名 | すぐに見る |
|---|---|---|
| 한국어 (기본) | `index.html`, `5-1_cctv_litter.html` … | https://adminmrobo.github.io/motion_ai_series_01/ |
| English | `index.en.html`, `5-1_cctv_litter.en.html` … | https://adminmrobo.github.io/motion_ai_series_01/index.en.html |
| 中文 | `*.zh.html` | https://adminmrobo.github.io/motion_ai_series_01/index.zh.html |
| 日本語 | `*.ja.html` | https://adminmrobo.github.io/motion_ai_series_01/index.ja.html |
| Oʻzbekcha | `*.uz.html` | https://adminmrobo.github.io/motion_ai_series_01/index.uz.html |
| Русский | `*.ru.html` | https://adminmrobo.github.io/motion_ai_series_01/index.ru.html |

## 構成

| 編 | タイトル | 扱う内容 | 難易度 |
|---|---|---|---|
| [5-1](https://adminmrobo.github.io/motion_ai_series_01/5-1_cctv_litter.ja.html) | CCTVとゴミの投棄 — 人を棒人間に変えてとらえる | 画面は数字、物体検出と姿勢推定、関節13点、動作の特徴4つ、ルール対学習、ライブ管制室と判定保留 | ★☆☆☆☆ |
| [5-2](https://adminmrobo.github.io/motion_ai_series_01/5-2_recognize_to_generate.ja.html) | 見分けることから作ることへ — 特徴表の矢印を逆にする | 識別モデルと生成モデル、動作は表（46 × 26）、座標の平均対角度の平均、データ分布、4つの生成器と審査官の採点 | ★★☆☆☆ |
| [5-3](https://adminmrobo.github.io/motion_ai_series_01/5-3_encoder_decoder.ja.html) | エンコーダ・デコーダ — 動作を畳んで広げる | 線形オートエンコーダ（PCA）、ボトルネックの大きさ、潜在マップとつまみ（潜在変数）、揺れの除去と隠れの復元、少ないデータでの検出、潜在空間での生成 | ★★★☆☆ |
| [5-4](https://adminmrobo.github.io/motion_ai_series_01/5-4_text_to_motion.ja.html) | 単語から動作へ — 言葉と身ぶりを同じ地図に置く | 単語袋（バッグ・オブ・ワーズ）、対照学習、共有マップ、文で動作を探す・作る・つなぐ、単語袋の限界 | ★★★★☆ |
| [5-5](https://adminmrobo.github.io/motion_ai_series_01/5-5_prompt_to_dance.ja.html) | 「踊って」からダンス動画へ — プロンプトが助手のダンスになるまで | プロンプトから動画までの6段階、ポーズマップとポーズに基づく生成、動画プレーヤーと並べて見る、動作一致率の測り方、シリーズのまとめ | ★★★★★ |

順番どおりに読むことを勧める。前の編の棒人間と数字を次の編が引き継いで使うが、各編は単独でも読める。

## 棒人間がたどってきた道

ある編の結果が、次の編の材料になる。

| 編 | 入るもの | 出てくるもの | 次の編へ渡す問い |
|---|---|---|---|
| 5-1 | CCTV画面（数字6,220,800個） | 関節26個 → 特徴4つ → 「投棄 / 正常」 | この特徴を逆向きに使えば動作を作れるだろうか？ |
| 5-2 | ラベル「投げる」 | 数字1,196個からなる動作 | 生成に必要なつまみ（潜在変数）はどこから来るのか？ |
| 5-3 | 動作の数字1,196個 | つまみ16個 → 再び1,196個 | 言葉で望む動作を選べないだろうか？ |
| 5-4 | 文「춤춰」（踊って） | 共有マップ上の点 → 棒人間のダンス | 棒人間に人の姿を着せられるだろうか？ |
| 5-5 | 棒人間のダンス + 助手の参照画像 | 助手のダンス動画 | — |

## 各編のカギとなる数字

すべて各編のColabコードを実際に実行した結果である。

| 編 | 数字 | 意味 |
|---|---|---|
| 5-1 | 60.7% → 99.7% | 「手首が速ければ投棄」というルール → 特徴4つ + ロジスティック回帰のテスト正解率 |
| 5-2 | 44.2% → 0.0% | 座標ごとにサイコロを振った生成器 → つまみ3つから取り出した生成器の骨の長さの誤差 |
| 5-3 | 99.8% | 1,196個の数字を16個に畳んでも残る動き（説明された分散） |
| 5-4 | 1.90 → 0.01 | 対照学習400ステップの間のペア合わせ損失 |
| 5-5 | 77.6% → 100% | 同じダンスを1秒遅れて踊った場合の一致率 → 時間を合わせた後の一致率 |

## 各編に含まれているもの

- 自分で操作する実習と動くダイアグラム
- 初心者向けの解説とセクションごとの確認問題
- **Colabコード2つ** — コピー、`.py` のダウンロード、ノートブック（`.ipynb`）のダウンロードに対応している。Colabの標準ライブラリだけを使い、ページには実際の実行結果を載せている。
- AI応用プロンプト（応用分野探し、ハッカソン48時間計画、コンテスト企画書の草案、論文の実験設計）
- 用語集（本文の点線の下線の吹き出しと同じ辞書）、たとえ集とたとえが外れるところ、参考文献
- 教育者向けTIP（運営案3つ、セクションごとの運営ポイント、よくある誤解 Top 5、確認問題、Colab課題）

編ごとの主な実習は次のとおりである。

| 編 | 主な実習 |
|---|---|
| 5-1 | CCTV画面を数字で見る、検出ボックス・関節・プライバシーモードのオン/オフ、6つの場面の再生、ルールのしきい値の実験、ライブ管制室 |
| 5-2 | 識別・生成の矢印を逆にする、動作の表（46 × 26）の探索、2つの動作を混ぜる（座標対角度）、投げる動作100個の分布、4つの生成器の採点 |
| 5-3 | ボトルネックの大きさを変えながら畳んで広げる、潜在マップと4つのつまみ、揺れ・隠れの復元、生成器E |
| 5-4 | 単語袋を見る、絡まった線がペアを見つける対照学習の再生、共有マップ、文で棒人間を動かす |
| 5-5 | 6段階のパイプライン、ノイズから助手を描く、動画プレーヤー（並べて見る・ずれ・左右反転）、動作一致率の実験 |

## Colabコード

| 編 | コード1 | コード2 | ライブラリ | 実行時間（CPU） |
|---|---|---|---|---|
| 5-1 | 棒人間の場面を作り、特徴を4つ取り出す | ルール対学習、5つの投棄検出器の比較 | numpy, matplotlib, scikit-learn | 1秒未満 / 約20秒 |
| 5-2 | 動作は表である、混ぜるとなぜ壊れるのか | 4つの動作生成器と審査官の採点表 | numpy, matplotlib | 1秒未満 / 約10秒 |
| 5-3 | 動作をk個の数字に畳んで広げる（線形オートエンコーダ） | 畳んだ数字で投棄検出と動作生成を改善する | numpy, matplotlib, scikit-learn | 約3秒 / 約40秒 |
| 5-4 | 単語袋と対照学習 | 言葉を入れると動作が出てくる（探す・作る・つなぐ） | numpy | 約5秒 / 約5秒 |
| 5-5 | 動作一致率はどう測るのか（時間合わせ、DTW） | 動画を数字で分解してみる | numpy, OpenCV | 約5秒 / 約3秒 |

5-5のコード2には動画ファイル `match_score_video.mp4` が必要である。`colab/` フォルダの動画をColab左側のファイル欄にアップロードしてから実行すること。

## ファイル

```
index.html                       シリーズ一覧（5つのミッション）
5-1_cctv_litter.html             CCTVとゴミの投棄
5-2_recognize_to_generate.html   見分けることから作ることへ
5-3_encoder_decoder.html         エンコーダ・デコーダ
5-4_text_to_motion.html          単語から動作へ
5-5_prompt_to_dance.html         「踊って」からダンス動画へ（動画を含む）
*.en.html *.zh.html *.ja.html   同じページの英語・中国語・日本語版
*.uz.html *.ru.html              同じページのウズベク語・ロシア語版
colab/                           （任意）各編のColabコード10個と5-5の分析用動画
```

各HTMLは画像・動画・データ・スクリプトをファイルの中に含んでいるため、ビルド作業は不要である。ファイルをブラウザで開くだけでよい（フォントはGoogle Fontsから読み込むため、インターネットに接続していない場合は標準フォントで表示される）。編どうしをつなぐリンクと言語の切り替えは、すべてのファイルが同じフォルダにあるときに動作するので、ファイル名を変えないこと。翻訳版は言語ごとにファイルが1つずつ増えるだけで、サイズは韓国語版と同じである。

| ファイル | サイズ | 備考 |
|---|---|---|
| index.html | 約0.4MB | |
| 5-1 ~ 5-4 | 各0.9 ~ 1.3MB | |
| 5-5_prompt_to_dance.html | 約4.4MB | ダンス動画（10秒、H.264 + AAC）をファイルの中に含んでいる。動画を別にアップロードする必要はない |

本文から前のシリーズへのリンクは、それぞれのシリーズのサイトに直接つながり、新しいタブで開く。3-x編は [ディープラーニング A to Z (AI_Model_Review)](https://adminmrobo.github.io/AI_Model_Review/)、4-x編は [AIは画像をどう見分けるのか？ (AI_image_classification)](https://adminmrobo.github.io/AI_image_classification/) である。

## 先に読んでおくとよい編

このシリーズは [ディープラーニング A to Z](https://adminmrobo.github.io/AI_Model_Review/)（3-x）と [AIは画像をどう見分けるのか？](https://adminmrobo.github.io/AI_image_classification/)（4-x）に続く編である。

| このシリーズ | 先に読んでおくとよい編 | 理由 |
|---|---|---|
| 5-1 | [4-2 猫 vs 人](https://adminmrobo.github.io/AI_image_classification/4-2_cat_human.html) | 写真が数字の行列になる過程 |
| 5-1 | [3-7 順序モデル](https://adminmrobo.github.io/AI_Model_Review/3-7_sequence_models.html) | 棒人間が時間の順序を持つデータ（時系列）になる |
| 5-3 | [3-7 順序モデル・オートエンコーダ](https://adminmrobo.github.io/AI_Model_Review/3-7_sequence_models.html#ae) | ニューラルネットワークで作るエンコーダ・デコーダ |
| 5-4 | [3-5 テキスト](https://adminmrobo.github.io/AI_Model_Review/3-5_text.html), [3-8 アテンション・トランスフォーマー](https://adminmrobo.github.io/AI_Model_Review/3-8_attention_transformer.html) | 単語袋より優れたテキストエンコーダ |
| 5-5 | [3-3 画像とCNN](https://adminmrobo.github.io/AI_Model_Review/3-3_image_cnn.html) | 動画生成モデルが画像を扱う土台 |

## データと画像

- 研究室の仲間たち（博士・助手・ショウジョウバエ研究員・研究室ロボット）、棒人間のキャラクターシート、場面のイラスト、助手のキャラクターシート・表情シート、カットシート、ダンス動画は著者が自分で作ったものである。
- 棒人間の動作（入れる・投げる・通り過ぎる・手を振る・拾う・落とす・踊る）と動作の説明文はすべて**合成データ**である。関節の角度を時間に沿って変えて作ったもので、実際の人を撮影したデータは使っていない。
- ページ内の計算（動作生成、特徴、エンコーダ・デコーダ、対照学習、一致率）はColabコードと同じ計算である。ブラウザで乱数を引き直す実習では数字が少し異なることがあり、表の数字はコードを実際に実行した結果である。
- 一部の図と値は説明用の模型である。各編のフッターの「説明用の模型であるもの」に、何が実際の計算で何が例示なのかを書いてある。

| 編 | 説明用の模型であるもの |
|---|---|
| 5-1 | 検出ボックスの確信度（0.94など）は例示値、関節の座標はイラストから読み取って移した値 |
| 5-3 | つまみのニックネームは著者の解釈 |
| 5-5 | ノイズの図は完成したフレームにノイズを混ぜて見せたもの。一致率の実験は説明用の振り付けで計算したもので、動画内の76.5%を計算し直したものではない |

## 用語の表記

このシリーズでは、潜在変数（latent variable）を**つまみ（潜在変数）**と呼ぶ。回すとデータ全体がいっしょに変わる少数の数字というたとえであり、英語圏の解説でも潜在空間の各次元を「knob（つまみ）」「dial（ダイヤル）」「slider（スライダー）」と呼ぶことがある。論文での正式な用語は潜在変数であり、5-3でデータが見つけたつまみの一つひとつは主成分（principal component）である。

## ライセンス

この著作物は [クリエイティブ・コモンズ 表示-非営利 4.0 国際ライセンス（CC BY-NC 4.0）](https://creativecommons.org/licenses/by-nc/4.0/deed.ja) のもとで公開している。
非営利目的に限り自由に共有・改変できるが、**出典は必ず表記**しなければならない。

出典表記の例: アン・サンソン「AIは動作をどう見分け、どう作り出すのか？・5-1 CCTVとゴミの投棄」、AI Model Review。

---

<a id="uz"></a>

# AI harakatni qanday taniydi va yaratadi?

Tungi soat ikkida xiyobondagi CCTV kamerasidan boshlanadigan beshta shoshilinch missiya orqali harakatni tanib olishdan harakat yaratishgacha boʻlgan yoʻlni boshidan oxirigacha bosib oʻtadigan interaktiv tushuntirish seriyasi.
Chiqindi tashlayotgan odamni chiziqcha odamga aylantirib ushlashdan boshlab, oʻsha belgilarni teskari ishlatib harakat yaratamiz, enkoder·dekoder bilan uni buklab, qayta yoyamiz, soʻz va harakatni bitta xaritaga joylaymiz va oxirida birgina "Raqsga tush!" soʻzi Yordamchining raqs videosiga aylanguncha boʻlgan jarayonni koʻrib chiqamiz.

**Hoziroq koʻrish:** https://adminmrobo.github.io/motion_ai_series_01/index.uz.html

Muallif · Ahn Sangsun (M-Robo kompaniyasi rahbari)

## Til

Asosiy til — koreys tili; barcha sahifalarni ingliz, xitoy, yapon, oʻzbek va rus tillarida ham koʻrish mumkin.

- **Oʻzingiz tanlang:** har bir sahifaning yuqori menyusidagi 🌐 til tanlash roʻyxatidan yoki pastki oʻng burchakdagi 🌐 bannerdan tanlang. Tanlangan tilni brauzer eslab qoladi.
- **Avtomatik almashish:** koreyscha sahifaga birinchi marta kirganingizda, brauzeringiz tiliga mos tarjima sahifasiga avtomatik oʻtasiz (qoʻllab-quvvatlanmaydigan tillarda sahifa koreyscha qoladi).
- **Manzil orqali belgilash:** manzil oxiriga `?lang=en` kabi qoʻshsangiz, sahifa oʻsha tilda ochiladi (`ko`, `en`, `zh`, `ja`, `uz`, `ru`).
- 5-4-qism 40 ta koreyscha soʻz boʻlagidan tuzilgan oʻyinchoq modelga bagʻishlangan. Shuning uchun qaysi tilda oʻqimang, modelga kiritiladigan misol jumlalar va soʻz boʻlaklari koreyscha qoldirilgan, ma’nosi esa qavs ichida berilgan.

| Til | Fayl nomi | Hoziroq koʻrish |
|---|---|---|
| 한국어 (asosiy) | `index.html`, `5-1_cctv_litter.html` … | https://adminmrobo.github.io/motion_ai_series_01/ |
| English | `index.en.html`, `5-1_cctv_litter.en.html` … | https://adminmrobo.github.io/motion_ai_series_01/index.en.html |
| 中文 | `*.zh.html` | https://adminmrobo.github.io/motion_ai_series_01/index.zh.html |
| 日本語 | `*.ja.html` | https://adminmrobo.github.io/motion_ai_series_01/index.ja.html |
| Oʻzbekcha | `*.uz.html` | https://adminmrobo.github.io/motion_ai_series_01/index.uz.html |
| Русский | `*.ru.html` | https://adminmrobo.github.io/motion_ai_series_01/index.ru.html |

## Tuzilishi

| Qism | Sarlavha | Mazmuni | Qiyinlik |
|---|---|---|---|
| [5-1](https://adminmrobo.github.io/motion_ai_series_01/5-1_cctv_litter.uz.html) | CCTV va chiqindi tashlash — odamni chiziqcha odamga aylantirib ushlaymiz | Ekran — bu raqamlar, obyektlarni aniqlash va pozani baholash, 13 ta boʻgʻim nuqtasi, 4 ta harakat belgisi, qoida va oʻrganish, jonli nazorat xonasi va qaror kechiktirildi | ★☆☆☆☆ |
| [5-2](https://adminmrobo.github.io/motion_ai_series_01/5-2_recognize_to_generate.uz.html) | Tanib olishdan yaratishga — belgilar jadvalidagi strelkani teskari aylantiramiz | Diskriminativ model va generativ model, harakat — bu jadval (46 × 26), koordinatalar oʻrtachasi va burchaklar oʻrtachasi, ma’lumotlar taqsimoti, toʻrtta generator va Nazoratchining baholashi | ★★☆☆☆ |
| [5-3](https://adminmrobo.github.io/motion_ai_series_01/5-3_encoder_decoder.uz.html) | Enkoder·dekoder — harakatni buklab, qayta yoyamiz | Chiziqli avtoenkoder (PCA), tor boʻgʻiz (bottleneck) oʻlchami, yashirin xarita va dastalar (yashirin oʻzgaruvchilar), titrashni yoʻqotish va toʻsilgan qismni tiklash, oz ma’lumot bilan aniqlash, yashirin fazoda yaratish | ★★★☆☆ |
| [5-4](https://adminmrobo.github.io/motion_ai_series_01/5-4_text_to_motion.uz.html) | Soʻzdan harakatga — soʻz va imo-ishorani bitta xaritaga joylaymiz | Soʻzlar xaltasi, kontrastiv oʻrganish, umumiy xarita, jumla orqali harakatni topish · yaratish · ulash, soʻzlar xaltasining cheklovlari | ★★★★☆ |
| [5-5](https://adminmrobo.github.io/motion_ai_series_01/5-5_prompt_to_dance.uz.html) | "Raqsga tush!" buyrugʻidan raqs videosigacha — prompt Yordamchining raqsiga aylanguncha | Promptdan videogacha oltita bosqich, poza xaritasi va pozaga asoslangan generatsiya, video pleyer va yonma-yon koʻrish, harakat mosligini oʻlchash, seriya xulosasi | ★★★★★ |

Qismlarni tartib bilan oʻqish tavsiya etiladi. Keyingi qism oldingi qismdagi chiziqcha odam va raqamlardan foydalanadi, ammo har bir qismni alohida oʻqish ham mumkin.

## Chiziqcha odam bosib oʻtgan yoʻl

Bir qismning natijasi keyingi qism uchun xomashyo boʻladi.

| Qism | Kirish | Chiqish | Keyingi qismga oʻtadigan savol |
|---|---|---|---|
| 5-1 | CCTV ekrani (6 220 800 ta raqam) | 26 ta boʻgʻim → 4 ta belgi → "Tashlash / Normal" | Bu belgilarni teskari ishlatsak, harakat yarata olamizmi? |
| 5-2 | "Otish" yorligʻi | 1 196 ta raqamdan iborat harakat | Generatsiya uchun kerak boʻlgan dastalar (yashirin oʻzgaruvchilar) qayerdan olinadi? |
| 5-3 | Harakatning 1 196 ta raqami | 16 ta dasta → yana 1 196 ta | Kerakli harakatni soʻz bilan tanlab boʻlmaydimi? |
| 5-4 | "Raqsga tush!" jumlasi | Umumiy xaritadagi nuqta → chiziqcha odamning raqsi | Chiziqcha odamga inson qiyofasini kiydira olamizmi? |
| 5-5 | Chiziqcha odamning raqsi + Yordamchining namuna rasmi | Yordamchining raqs videosi | — |

## Har bir qismning asosiy raqamlari

Barchasi har bir qismdagi Colab kodini haqiqatan ishga tushirib olingan natijalar.

| Qism | Raqam | Ma’nosi |
|---|---|---|
| 5-1 | 60.7% → 99.7% | "Bilak tez harakatlansa — tashlash" qoidasi → 4 ta belgi + logistik regressiyaning test aniqligi |
| 5-2 | 44.2% → 0.0% | Har bir koordinata uchun zar tashlaydigan generator → 3 ta dastadan tanlaydigan generatorning suyak uzunligi xatosi |
| 5-3 | 99.8% | 1 196 ta raqamni 16 tagacha buklaganda ham saqlanib qoladigan harakat (tushuntirilgan dispersiya) |
| 5-4 | 1.90 → 0.01 | Kontrastiv oʻrganishning 400 qadami davomidagi juftlash yoʻqotishi |
| 5-5 | 77.6% → 100% | Bir xil raqsni 1 soniya kechikib takrorlagandagi moslik → vaqt moslashtirilgandan keyingi moslik |

## Har bir qismda nimalar bor

- Oʻzingiz boshqaradigan amaliy mashqlar va harakatlanuvchi diagrammalar
- Yangi boshlovchilar uchun tushuntirishlar va har bir boʻlim boʻyicha nazorat savollari
- **2 ta Colab kodi** — nusxalash, `.py` yuklab olish va notebook (`.ipynb`) yuklab olish imkoniyati bor. Faqat Colabning standart kutubxonalari ishlatiladi, sahifada esa haqiqiy ishga tushirish natijalari keltirilgan.
- AI uchun amaliy promptlar (qoʻllanish sohalarini topish, 48 soatlik xakaton rejasi, tanlov loyihasi taklifining qoralamasi, ilmiy maqola uchun tajriba dizayni)
- Atamalar lugʻati (matndagi nuqtali tagchiziqli izoh oynalari bilan bir xil lugʻat), oʻxshatishlar toʻplami va oʻxshatish notoʻgʻri boʻladigan joylar, manbalar
- Oʻqituvchilar uchun maslahatlar (uchta dars rejasi, har bir boʻlim boʻyicha asosiy jihatlar, eng keng tarqalgan 5 ta notoʻgʻri tushuncha, nazorat savollari, Colab topshiriqlari)

Har bir qismdagi asosiy amaliy mashqlar quyidagilar.

| Qism | Asosiy amaliy mashqlar |
|---|---|
| 5-1 | CCTV ekranini raqamlar sifatida koʻrish, aniqlash ramkalari · boʻgʻimlar · maxfiylik rejimini yoqish va oʻchirish, oltita sahnani ijro etish, qoida chegara qiymatlari bilan tajriba, jonli nazorat xonasi |
| 5-2 | Diskriminativ · generativ strelkani teskari aylantirish, harakat jadvalini (46 × 26) oʻrganish, ikki harakatni aralashtirish (koordinatalar va burchaklar), 100 ta otish harakatining taqsimoti, toʻrtta generatorni baholash |
| 5-3 | Tor boʻgʻiz oʻlchamini oʻzgartirib buklash va yoyish, yashirin xarita va toʻrtta dasta, titrash · toʻsilishni tiklash, E generatori |
| 5-4 | Soʻzlar xaltasini koʻrish, chalkash chiziqlar juftini topadigan kontrastiv oʻrganishni ijro etish, umumiy xarita, jumla orqali chiziqcha odamni harakatlantirish |
| 5-5 | Oltita bosqichli pipeline, shovqindan Yordamchini chizish, video pleyer (yonma-yon koʻrish · siljish · chap-oʻngga aylantirish), harakat mosligi tajribasi |

## Colab kodi

| Qism | 1-kod | 2-kod | Kutubxonalar | Ishlash vaqti (CPU) |
|---|---|---|---|---|
| 5-1 | Chiziqcha odam sahnalarini yaratish va 4 ta belgini ajratib olish | Qoida va oʻrganish: beshta tashlash detektorini solishtirish | numpy, matplotlib, scikit-learn | 1 soniyadan kam / taxm. 20 soniya |
| 5-2 | Harakat — bu jadval: aralashtirganda nega buziladi | Toʻrtta harakat generatori va Nazoratchining baholash varaqasi | numpy, matplotlib | 1 soniyadan kam / taxm. 10 soniya |
| 5-3 | Harakatni k ta raqamga buklash va qayta yoyish (chiziqli avtoenkoder) | Buklangan raqamlar bilan tashlashni aniqlash va harakat yaratishni yaxshilash | numpy, matplotlib, scikit-learn | taxm. 3 soniya / taxm. 40 soniya |
| 5-4 | Soʻzlar xaltasi va kontrastiv oʻrganish | Soʻz kiritilsa, harakat chiqadi (topish · yaratish · ulash) | numpy | taxm. 5 soniya / taxm. 5 soniya |
| 5-5 | Harakat mosligi qanday oʻlchanadi (vaqtni moslashtirish, DTW) | Videoni raqamlarga ajratib tahlil qilish | numpy, OpenCV | taxm. 5 soniya / taxm. 3 soniya |

5-5-qismning 2-kodi uchun `match_score_video.mp4` video fayli kerak. `colab/` papkasidagi videoni Colabning chap tomonidagi fayllar paneliga yuklang, soʻng kodni ishga tushiring.

## Fayllar

```
index.html                       Seriya roʻyxati (beshta missiya)
5-1_cctv_litter.html             CCTV va chiqindi tashlash
5-2_recognize_to_generate.html   Tanib olishdan yaratishga
5-3_encoder_decoder.html         Enkoder·dekoder
5-4_text_to_motion.html          Soʻzdan harakatga
5-5_prompt_to_dance.html         "Raqsga tush!" buyrugʻidan raqs videosigacha (video bilan)
*.en.html *.zh.html *.ja.html   Shu sahifalarning inglizcha · xitoycha · yaponcha talqini
*.uz.html *.ru.html              Shu sahifalarning oʻzbekcha · ruscha talqini
colab/                           (ixtiyoriy) Har bir qismning 10 ta Colab kodi va 5-5 tahlili uchun video
```

Har bir HTML fayl rasmlar, video, ma’lumotlar va skriptlarni oʻz ichiga oladi, shuning uchun build jarayoni kerak emas. Faylni brauzerda ochishning oʻzi kifoya (shriftlar Google Fonts’dan yuklanadi, shuning uchun internet boʻlmasa standart shriftda koʻrinadi). Qismlar orasidagi havolalar va tilni almashtirish barcha fayllar bitta papkada boʻlgandagina ishlaydi, shuning uchun fayl nomlarini oʻzgartirmang. Tarjima talqinlari har bir til uchun yana bittadan qoʻshimcha fayl boʻlib, hajmi koreyscha talqin bilan bir xil.

| Fayl | Hajmi | Izoh |
|---|---|---|
| index.html | taxm. 0.4MB | |
| 5-1 ~ 5-4 | har biri 0.9 ~ 1.3MB | |
| 5-5_prompt_to_dance.html | taxm. 4.4MB | Raqs videosi (10 soniya, H.264 + AAC) fayl ichiga joylangan. Videoni alohida yuklash shart emas |

Matndagi oldingi seriyalarga olib boradigan havolalar toʻgʻridan-toʻgʻri oʻsha seriyalarning saytiga ulanadi va yangi tabda ochiladi. 3-x qismlar — [Chuqur oʻrganish A dan Z gacha (AI_Model_Review)](https://adminmrobo.github.io/AI_Model_Review/), 4-x qismlar — [AI rasmlarni qanday ajratadi? (AI_image_classification)](https://adminmrobo.github.io/AI_image_classification/).

## Avval oʻqish tavsiya etiladigan qismlar

Bu seriya [Chuqur oʻrganish A dan Z gacha](https://adminmrobo.github.io/AI_Model_Review/) (3-x) va [AI rasmlarni qanday ajratadi?](https://adminmrobo.github.io/AI_image_classification/) (4-x) seriyalarining davomidir.

| Ushbu seriya | Avval oʻqish tavsiya etiladigan qism | Sababi |
|---|---|---|
| 5-1 | [4-2 Mushuk va odam](https://adminmrobo.github.io/AI_image_classification/4-2_cat_human.html) | Rasm raqamlar matritsasiga aylanish jarayoni |
| 5-1 | [3-7 Ketma-ketlik modellari](https://adminmrobo.github.io/AI_Model_Review/3-7_sequence_models.html) | Chiziqcha odam vaqt tartibiga ega ma’lumotga (vaqt qatoriga) aylanadi |
| 5-3 | [3-7 Ketma-ketlik modellari · avtoenkoder](https://adminmrobo.github.io/AI_Model_Review/3-7_sequence_models.html#ae) | Neyron tarmoq yordamida qurilgan enkoder·dekoder |
| 5-4 | [3-5 Matn](https://adminmrobo.github.io/AI_Model_Review/3-5_text.html), [3-8 Attention · Transformer](https://adminmrobo.github.io/AI_Model_Review/3-8_attention_transformer.html) | Soʻzlar xaltasidan yaxshiroq matn enkoderi |
| 5-5 | [3-3 Rasm va CNN](https://adminmrobo.github.io/AI_Model_Review/3-3_image_cnn.html) | Video generatsiya modellari rasmlar bilan ishlashining asosi |

## Ma’lumotlar va rasmlar

- Laboratoriya jamoasi (Doktor · Yordamchi · Drozofila tadqiqotchisi · Laboratoriya roboti), chiziqcha odam personaj varaqlari, sahna rasmlari, Yordamchining personaj varagʻi va mimika varagʻi, kadrlar varagʻi hamda raqs videosi muallifning oʻzi tomonidan yaratilgan.
- Chiziqcha odam harakatlari (solish · otish · oʻtib ketish · qoʻl silkitish · terib olish · tushirib yuborish · raqs tushish) va harakat tavsifi jumlalari — barchasi **sintetik ma’lumotlar**. Ular boʻgʻim burchaklarini vaqt boʻyicha oʻzgartirish orqali yaratilgan; haqiqiy odamlarni suratga olgan ma’lumotlar ishlatilmagan.
- Sahifalardagi hisob-kitoblar (harakat yaratish, belgilar, enkoder·dekoder, kontrastiv oʻrganish, moslik) Colab kodidagi hisob-kitoblar bilan bir xil. Brauzerda tasodifiy sonlarni qaytadan tanlaydigan mashqlarda raqamlar biroz farq qilishi mumkin; jadvallardagi raqamlar esa kodni haqiqatan ishga tushirib olingan natijalardir.
- Ayrim rasmlar va qiymatlar tushuntirish uchun maketlardir. Har bir qismning pastki qismidagi "Tushuntirish uchun maket boʻlgan narsalar" boʻlimida nima haqiqiy hisob-kitob va nima misol ekanligi yozib qoʻyilgan.

| Qism | Tushuntirish uchun maket boʻlgan narsalar |
|---|---|
| 5-1 | Aniqlash ramkalarining ishonch darajasi (0.94 va h.k.) — misol qiymatlar; boʻgʻim koordinatalari rasmdan oʻqib olingan qiymatlar |
| 5-3 | Dastalarning laqablari — muallifning talqini |
| 5-5 | Shovqinli rasmlar tayyor kadrlarga shovqin qoʻshib koʻrsatilgan. Moslik tajribasi tushuntirish uchun tuzilgan xoreografiya asosida hisoblangan va videodagi 76.5% qiymatini qayta hisoblash emas |

## Atamalar

Bu seriyada yashirin oʻzgaruvchi (latent variable) **dasta (yashirin oʻzgaruvchi)** deb ataladi. Bu — burasangiz butun ma’lumot birgalikda oʻzgaradigan bir nechta raqam degan oʻxshatish; ingliz tilidagi tushuntirishlarda ham yashirin fazoning har bir oʻlchami koʻpincha "knob" (dasta), "dial" (burama tugma), "slider" (surgich) deb ataladi. Ilmiy maqolalardagi rasmiy atama — yashirin oʻzgaruvchi; 5-3-qismda ma’lumotlardan topilgan har bir dasta esa bosh komponent (principal component) hisoblanadi.

## Litsenziya

Ushbu asar [Creative Commons Attribution-NonCommercial 4.0 International litsenziyasi (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/deed.en) asosida ochiq e’lon qilingan.
Faqat notijorat maqsadlarda erkin tarqatish va oʻzgartirib foydalanish mumkin, biroq **manbani albatta koʻrsatish** shart.

Manbani koʻrsatish namunasi: Ahn Sangsun, «AI harakatni qanday taniydi va yaratadi? · 5-1 CCTV va chiqindi tashlash», AI Model Review.

---

<a id="ru"></a>

# Как ИИ распознаёт движения и как их создаёт?

Интерактивная серия объяснений из пяти срочных миссий, которые начинаются с камеры видеонаблюдения в переулке в два часа ночи: путь от распознавания движений до их генерации с самого начала.
Мы начнём с того, что превратим человека, выбрасывающего мусор, в человечка-палочку и поймаем его; затем перевернём признаки и будем создавать движения, сжимать и разворачивать их кодировщиком и декодером, положим речь и движения на одну карту, а в конце пройдём весь путь, на котором одно слово «Танцуй» превращается в видео с танцем Ассистента.

**Открыть сайт:** https://adminmrobo.github.io/motion_ai_series_01/index.ru.html

Автор · Ан Сансон (генеральный директор M-Robo Co., Ltd.)

## Язык

Основной язык — корейский; все страницы также доступны на английском, китайском, японском, узбекском и русском языках.

- **Выбор вручную:** выберите язык в поле 🌐 в меню вверху каждой страницы или на баннере 🌐 в правом нижнем углу. Браузер запоминает выбранный язык.
- **Автоматическое переключение:** при первом заходе на корейскую страницу вы автоматически попадаете на перевод, соответствующий языку браузера (если язык не поддерживается, остаётся корейская версия).
- **Через адрес:** добавьте к адресу, например, `?lang=en`, и страница откроется на этом языке (`ko`, `en`, `zh`, `ja`, `uz`, `ru`).
- Часть 5-4 посвящена игрушечной модели, построенной на 40 корейских фрагментах слов, поэтому на любом языке примеры предложений и фрагменты слов, которые подаются в модель, остаются на корейском, а их значение дано в скобках.

| Язык | Имена файлов | Открыть |
|---|---|---|
| 한국어 (основной) | `index.html`, `5-1_cctv_litter.html` … | https://adminmrobo.github.io/motion_ai_series_01/ |
| English | `index.en.html`, `5-1_cctv_litter.en.html` … | https://adminmrobo.github.io/motion_ai_series_01/index.en.html |
| 中文 | `*.zh.html` | https://adminmrobo.github.io/motion_ai_series_01/index.zh.html |
| 日本語 | `*.ja.html` | https://adminmrobo.github.io/motion_ai_series_01/index.ja.html |
| Oʻzbekcha | `*.uz.html` | https://adminmrobo.github.io/motion_ai_series_01/index.uz.html |
| Русский | `*.ru.html` | https://adminmrobo.github.io/motion_ai_series_01/index.ru.html |

## Содержание

| Часть | Название | О чём | Сложность |
|---|---|---|---|
| [5-1](https://adminmrobo.github.io/motion_ai_series_01/5-1_cctv_litter.ru.html) | Выброс мусора на камере видеонаблюдения — превращаем человека в человечка-палочку и ловим | Изображение — это числа, обнаружение объектов и оценка позы, 13 суставов, 4 признака движения, правила против обучения, живая диспетчерская и воздержание от решения | ★☆☆☆☆ |
| [5-2](https://adminmrobo.github.io/motion_ai_series_01/5-2_recognize_to_generate.ru.html) | От распознавания к созданию — переворачиваем стрелку таблицы признаков | Дискриминативная и генеративная модели, движение — это таблица (46 × 26), усреднение координат против усреднения углов, распределение данных, четыре генератора и оценки Эксперта | ★★☆☆☆ |
| [5-3](https://adminmrobo.github.io/motion_ai_series_01/5-3_encoder_decoder.ru.html) | Кодировщик и декодер — сжать и развернуть движение | Линейный автокодировщик (PCA), размер узкого места, латентная карта и ручки (латентные переменные), устранение дрожания и восстановление перекрытий, обнаружение по малому объёму данных, генерация в латентном пространстве | ★★★☆☆ |
| [5-4](https://adminmrobo.github.io/motion_ai_series_01/5-4_text_to_motion.ru.html) | От слов к движению — речь и жесты на одной карте | Мешок слов, контрастивное обучение, общая карта, найти · создать · склеить движение по предложению, ограничения мешка слов | ★★★★☆ |
| [5-5](https://adminmrobo.github.io/motion_ai_series_01/5-5_prompt_to_dance.ru.html) | От «Танцуй» к видео с танцем — как промпт стал танцем Ассистента | Шесть этапов от промпта до видео, карта позы и генерация по позе, видеоплеер и просмотр бок о бок, измерение процента совпадения движений, итоги серии | ★★★★★ |

Рекомендуем читать по порядку. Следующая часть продолжает работать с человечками-палочками и числами из предыдущей, но каждую часть можно читать и отдельно.

## Путь человечка-палочки

Результат одной части становится материалом для следующей.

| Часть | Что на входе | Что на выходе | Вопрос для следующей части |
|---|---|---|---|
| 5-1 | Кадр камеры видеонаблюдения (6 220 800 чисел) | 26 суставов → 4 признака → «Выброс / Норма» | Можно ли создать движение, если использовать эти признаки в обратную сторону? |
| 5-2 | Метка «бросок» | Движение из 1 196 чисел | Откуда берутся ручки (латентные переменные), нужные для генерации? |
| 5-3 | Движение из 1 196 чисел | 16 ручек → снова 1 196 чисел | Нельзя ли выбрать нужное движение словами? |
| 5-4 | Предложение «Танцуй» | Точка на общей карте → танец человечка-палочки | Можно ли придать человечку-палочке облик человека? |
| 5-5 | Танец человечка-палочки + референсное изображение Ассистента | Видео с танцем Ассистента | — |

## Ключевые числа каждой части

Всё это результаты реального запуска кода Colab из каждой части.

| Часть | Число | Смысл |
|---|---|---|
| 5-1 | 60.7% → 99.7% | Точность на тесте: правило «быстрое запястье — значит, выброс» → 4 признака + логистическая регрессия |
| 5-2 | 44.2% → 0.0% | Ошибка длины костей: генератор, бросающий кубик для каждой координаты → генератор, выбирающий из 3 ручек |
| 5-3 | 99.8% | Доля движения, которая сохраняется, даже если сжать 1 196 чисел до 16 (объяснённая дисперсия) |
| 5-4 | 1.90 → 0.01 | Функция потерь подбора пар за 400 шагов контрастивного обучения |
| 5-5 | 77.6% → 100% | Процент совпадения для того же танца, повторённого с опозданием на 1 секунду → после выравнивания по времени |

## Что есть в каждой части

- Практические упражнения с прямым управлением и анимированные диаграммы
- Пояснения для начинающих и проверочные вопросы к каждому разделу
- **2 фрагмента кода Colab** — можно копировать, скачать `.py` и скачать ноутбук (`.ipynb`). Используются только стандартные библиотеки Colab, а на странице приведены реальные результаты запуска.
- Промпты для применения ИИ (поиск областей применения, план хакатона на 48 часов, черновик заявки на конкурс, план эксперимента для статьи)
- Глоссарий (тот же словарь, что и во всплывающих подсказках у подчёркнутых пунктиром слов в тексте), подборка аналогий и того, где аналогия не работает, источники
- Советы преподавателям (три варианта проведения занятия, ключевые моменты по разделам, топ-5 частых заблуждений, проверочные вопросы, задания в Colab)

Основные практические упражнения в каждой части:

| Часть | Основные упражнения |
|---|---|
| 5-1 | Увидеть кадр камеры как числа, включать и выключать рамки обнаружения, суставы и режим конфиденциальности, воспроизведение шести сцен, эксперимент с порогом правила, живая диспетчерская |
| 5-2 | Перевернуть стрелку «распознавание — генерация», исследовать таблицу движения (46 × 26), смешать два движения (координаты против углов), распределение 100 бросков, оценка четырёх генераторов |
| 5-3 | Сжимать и разворачивать, меняя размер узкого места, латентная карта и четыре ручки, восстановление после дрожания и перекрытия, генератор E |
| 5-4 | Посмотреть на мешок слов, воспроизведение контрастивного обучения, в котором спутанные линии находят свои пары, общая карта, управление человечком-палочкой с помощью предложения |
| 5-5 | Конвейер из шести этапов, рисование Ассистента из шума, видеоплеер (просмотр бок о бок · рассинхрон · зеркальное отражение), эксперимент с процентом совпадения движений |

## Код Colab

| Часть | Код 1 | Код 2 | Библиотеки | Время работы (CPU) |
|---|---|---|---|---|
| 5-1 | Создать сцены с человечками-палочками и извлечь 4 признака | Правила против обучения: сравнение пяти детекторов выброса мусора | numpy, matplotlib, scikit-learn | меньше 1 с / около 20 с |
| 5-2 | Движение — это таблица: почему оно ломается при смешивании | Четыре генератора движений и оценочный лист Эксперта | numpy, matplotlib | меньше 1 с / около 10 с |
| 5-3 | Сжать движение до k чисел и развернуть обратно (линейный автокодировщик) | Улучшить обнаружение выброса мусора и генерацию движений с помощью сжатых чисел | numpy, matplotlib, scikit-learn | около 3 с / около 40 с |
| 5-4 | Мешок слов и контрастивное обучение | Подаём слова — получаем движение (найти · создать · склеить) | numpy | около 5 с / около 5 с |
| 5-5 | Как измерить процент совпадения движений (выравнивание по времени, DTW) | Разбираем видео на числа | numpy, OpenCV | около 5 с / около 3 с |

Для кода 2 из части 5-5 нужен видеофайл `match_score_video.mp4`. Загрузите видео из папки `colab/` в панель файлов слева в Colab, а затем запустите код.

## Файлы

```
index.html                       список серии (пять миссий)
5-1_cctv_litter.html             выброс мусора на камере видеонаблюдения
5-2_recognize_to_generate.html   от распознавания к созданию
5-3_encoder_decoder.html         кодировщик и декодер
5-4_text_to_motion.html          от слов к движению
5-5_prompt_to_dance.html         от «Танцуй» к видео с танцем (с видео)
*.en.html *.zh.html *.ja.html   те же страницы на английском, китайском, японском
*.uz.html *.ru.html              те же страницы на узбекском и русском
colab/                           (необязательно) 10 фрагментов кода Colab и видео для анализа в 5-5
```

Каждый HTML-файл содержит внутри себя изображения, видео, данные и скрипты, поэтому сборка не нужна. Достаточно открыть файл в браузере (шрифты загружаются из Google Fonts, поэтому без интернета текст отображается шрифтом по умолчанию). Ссылки между частями и переключение языков работают, когда все файлы лежат в одной папке, поэтому не переименовывайте файлы. Для каждого языка перевода просто добавляется по одному файлу на страницу, а размер такой же, как у корейской версии.

| Файл | Размер | Примечание |
|---|---|---|
| index.html | около 0.4 МБ | |
| 5-1 ~ 5-4 | каждый 0.9 ~ 1.3 МБ | |
| 5-5_prompt_to_dance.html | около 4.4 МБ | Видео с танцем (10 секунд, H.264 + AAC) встроено в файл. Загружать видео отдельно не нужно |

Ссылки из текста на предыдущие серии ведут прямо на сайты этих серий и открываются в новой вкладке. Части 3-x — это [Глубокое обучение от A до Z (AI_Model_Review)](https://adminmrobo.github.io/AI_Model_Review/), части 4-x — [Как ИИ различает изображения? (AI_image_classification)](https://adminmrobo.github.io/AI_image_classification/).

## Что полезно прочитать заранее

Эта серия продолжает серии [Глубокое обучение от A до Z](https://adminmrobo.github.io/AI_Model_Review/) (3-x) и [Как ИИ различает изображения?](https://adminmrobo.github.io/AI_image_classification/) (4-x).

| Эта серия | Что полезно прочитать заранее | Почему |
|---|---|---|
| 5-1 | [4-2 Кошка или человек](https://adminmrobo.github.io/AI_image_classification/4-2_cat_human.html) | Как фотография превращается в матрицу чисел |
| 5-1 | [3-7 Последовательные модели](https://adminmrobo.github.io/AI_Model_Review/3-7_sequence_models.html) | Человечек-палочка становится данными, упорядоченными во времени (временным рядом) |
| 5-3 | [3-7 Последовательные модели · автокодировщик](https://adminmrobo.github.io/AI_Model_Review/3-7_sequence_models.html#ae) | Кодировщик и декодер на нейронной сети |
| 5-4 | [3-5 Текст](https://adminmrobo.github.io/AI_Model_Review/3-5_text.html), [3-8 Внимание и трансформер](https://adminmrobo.github.io/AI_Model_Review/3-8_attention_transformer.html) | Текстовые кодировщики лучше мешка слов |
| 5-5 | [3-3 Изображения и CNN](https://adminmrobo.github.io/AI_Model_Review/3-3_image_cnn.html) | Основа того, как модели генерации видео работают с изображениями |

## Данные и изображения

- Команда лаборатории (Доктор, Ассистент, Исследователь-дрозофила, Робот лаборатории), лист персонажа-человечка-палочки, иллюстрации сцен, лист персонажа и лист эмоций Ассистента, раскадровки и видео с танцем созданы автором.
- Движения человечка-палочки (положить, бросить, пройти мимо, помахать рукой, поднять, уронить, танцевать) и предложения с описаниями движений — это **синтетические данные**. Они созданы изменением углов суставов во времени; съёмки реальных людей не использовались.
- Вычисления на страницах (генерация движений, признаки, кодировщик и декодер, контрастивное обучение, процент совпадения) те же, что и в коде Colab. В упражнениях, где браузер заново генерирует случайные числа, значения могут немного отличаться, а числа в таблицах — результаты реального запуска кода.
- Некоторые иллюстрации и значения — иллюстративные макеты. В разделе «Что здесь — иллюстративный макет» в нижней части каждой страницы указано, что является реальным вычислением, а что — примером.

| Часть | Что здесь — иллюстративный макет |
|---|---|
| 5-1 | Уверенность рамок обнаружения (0.94 и т. п.) — примерные значения, координаты суставов считаны с рисунков |
| 5-3 | Прозвища ручек — интерпретация автора |
| 5-5 | Изображения с шумом получены добавлением шума к готовым кадрам. Эксперимент с процентом совпадения рассчитан на иллюстративной хореографии и не является пересчётом значения 76.5% из видео |

## Термины

В этой серии латентная переменная (latent variable) называется **ручкой (латентной переменной)**. Это аналогия: небольшое число чисел, при повороте которых меняются сразу все данные; в англоязычных объяснениях каждое измерение латентного пространства тоже часто называют «knob» (ручка), «dial» (регулятор) или «slider» (ползунок). Официальный термин в статьях — латентная переменная, а каждая ручка, которую данные находят в части 5-3, — это главная компонента (principal component).

## Лицензия

Это произведение распространяется по [лицензии Creative Commons «Атрибуция — Некоммерческое использование» 4.0 Международная (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/deed.ru).
Его можно свободно распространять и изменять только в некоммерческих целях, при этом **обязательно указывать источник**.

Пример указания источника: Ан Сансон, «Как ИИ распознаёт движения и как их создаёт? · 5-1 Выброс мусора на камере видеонаблюдения», AI Model Review.
