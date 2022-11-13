# 개요

개인이 머신 러닝을 활용하여 TTS를 제작할 때, 가장 큰 문제들을 정리해 보면
다음과 같습니다.

- **선행 지식 필요**: 실제 머신 러닝 기술을 활용하기 위해서는 컴퓨터와 머신
러닝 관련 지식이 필요한데, 다른 분들이 작성한 코드를 활용하는 수준까지 필요한
지식의 양이 꽤 많습니다.
- **한국어 지원 부족**: 대부분의 과정에 필요한 문서들은 영어로만 제공되고,
한국어로 작성된 문서가 거의 없습니다. 또한, 대부분의 TTS 머신러닝 모델은 영어
중심으로 구현되어, 한국어를 지원하도록 직접 수정해야 합니다.
- **음성 데이터 확보**: 머신 러닝을 통해 TTS를 만들기 위해서는 수 시간 분량의
음성 데이터가 필요합니다. 게다가, 무작정 목소리만 녹음하는 것이 아니라
머신러닝에 사용할 수 있도록 정형화된 형태로 가공해야 합니다.
- **고성능 컴퓨터**: 머신 러닝을 통해 TTS를 만들기 위해서는 TTS 모델을
학습시켜야 합니다. 모델을 학습시키는 데에는 고성능 GPU로도 많은 시간이
필요합니다.
- **느린 음성 합성 속도**: 실제로 음성 합성이 가능하더라도, 한 문장을 음성으로
합성하는데 너무 긴 시간이 필요하면 안됩니다. TTS를 잘 활용하기 위해서는 거의
실시간으로 동작하는 TTS 모델을 찾아 사용해야 합니다.

SCE-TTS에서는 다음과 같은 방법으로 이러한 문제들을 해결하고자 합니다.

- **즉시 활용 가능한 프로그램**: [입력한 텍스트를 음성으로 재생](/v2/uses?id=입력한-텍스트를-음성으로-듣기)하거나
[Twip 도네이션 메시지 TTS 대체](/v2/uses?id=twip-도네이션-메시지-tts-대체) 등의
기능을 지원하는 TTS 서버 프로그램을 제공하고, 사용법을 안내합니다.
- **한국어 지원**: 한국어를 지원하도록 수정한 TTS 모델을 사용하며, 모든 내용을
한국어로 정리하여 설명합니다.
- **음성 데이터 수집 및 사전 학습 모델 제공**: Mimic Recording Studio를 사용한
음성 녹음 방법을 소개하고 실제 모델 학습을 위해 데이터를 가공할 수 있도록
안내합니다. 또한 모델 학습에 필요한 음성 데이터량과 시간을 줄이기 위해 사전
학습 모델을 제공합니다.
- **Google Colab 사용**: 모델 학습을 위해 [Google Colab](https://colab.research.google.com/)을
사용하여 번거로운 학습 환경 구축 과정을 없애고, 고성능 컴퓨터 없이도 빠르게
모델을 학습시킬 수 있습니다.
- **추론 성능을 고려한 TTS 모델 선택**: GPU가 아닌 CPU 성능만으로 음성 합성을
수행할 수 있도록, 추론 성능을 고려한 TTS 및 보코더 모델을 선택했습니다.


## 설명 순서

SCE-TTS는 다음과 같은 순서로 내용을 설명합니다.

1. Mimic Recording Studio를 사용하여 자신의 목소리를 녹음하고, 모델 학습을
위한 형태로 변환합니다.
1. 녹음한 음성 데이터를 사용하여 Google Colab에서 TTS 모델들을 학습시킵니다.
1. 학습시킨 모델들을 간단하게 테스트 해볼 수 있는 방법을 소개합니다.
1. 학습시킨 모델들 활용하기 위한 TTS 서버를 사용하는 방법을 설명합니다.

각각의 과정들은 독립되어 있으며, 언제든지 전 단계로 되돌아가서 다시 진행할 수
있습니다. 결과물이 마음에 들지 않으면 음성 녹음을 더 많이 해보거나, TTS 모델을
더 많이 학습시켜 다시 테스트 해볼 수 있습니다.


## 예상 소요 시간

저는 약 3,000 문장을 직접 읽어 3시간 가량의 음성 데이터를 녹음했고, 이 음성
데이터를 통해 SCE-TTS를 통해 학습을 진행했습니다. 녹음은 하루에 2시간씩 총
3일간 녹음했습니다.

TTS 모델들의 학습 소요 시간은 예측하기 어렵습니다. 아무리 빠르게 학습시킨다고
하더라도 각각 최소 1시간 이상은 반드시 소요될 것이며, 어쩌면 3일 이상이 걸릴
수도 있습니다.


## 필요한 것

SCE-TTS에서 소개하는 내용을 따라하기 위한 준비 사항은 다음과 같습니다.

- 음성 녹음을 위한 마이크
- 64비트 Windows 10
- Google 계정
- Google 크롬 브라우저
- 파일 압축 프로그램([반디집](https://kr.bandisoft.com/bandizip/) 추천!)

---

?> :memo: 각 문서의 하단에는 댓글을 사용할 수 있도록 해두었습니다.  
문서의 내용을 따라하면서 문제가 발생했을 때, 댓글의 내용을 참고하세요.