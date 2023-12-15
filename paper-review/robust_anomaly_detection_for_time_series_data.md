# Abstract
시계열 데이터에서 Anomaly를 예측하는 Task는 데이터에서 나타나는 여러가지 패턴과 시계열적 특성에 많은 영향을 받게 됩니다.

이러한 이유로, 해당 논문에서는 `Negative Selection, Unthresholded Recurrence Plot, Extreme learning machine autoencoder` 등의 강점을 결합해 **Robust한 시계열 Anomaly Detection** 방법론을 제안합니다.

# Introduction
정상으로 간주되는 패턴이 모든 경우에서 항상 일정하게 나타나는 것은 아니기 때문에, Anomaly를 탐지하는데에 있어서, 해당 task에 대해 (대부분이 정상인)주어진 데이터에 의존할 수 밖에 없습니다.

Data Label의 유무에 따라, 데이터를 정상과 비정상 데이터로 구분해 모델을 학습시켜 이를 구분하도록 할 수도 있지만,

Anomaly는 전체 데이터 중 매우 적은 부분을 구성하고 있으며, 다양한 종류의 anomaly가 존재하기 때문에 전체 anomaly를 아우르는 Universal한 특성을 뽑아내는 것은 어렵다고 할 수 있습니다.

그렇기 때문에, 대부분의 경우에는 데이터 라벨이 요구되지 않는 `Unsupervised Learning` 방식을 채택하고 있으며, 학습된 정상 패턴과 다르게 나타나는 부분을 감지해 이상치로 분류하는 메커니즘으로 작동합니다.

Anomaly Detection에 적용할 수 있는 방법은 `Feature based Classification`, `Pattern based Classification`으로 구분할 수 있습니다.
- Feature based Classification
    - 데이터의 통계값이나, 수학적 머신러닝 기법을 통해 추출된 Feature를 활용해 정상과 이상 데이터를 구분
- Pattern based Classification
    - 데이터로부터 가공된 feature를 활용하는 것이 아니라, 데이터 그 자체로부터의 패턴을 학습해 정상과 이상 데이터를 구분

이를 활용한 다양한 방법이 개발되었지만, 해당 논문에서는 4가지의 주요한 문제점이 아직 존재하다고 지적하고 있습니다.
1. Unbalanced Pattern Distribution
    - 이상 데이터의 수는 정상 데이터에 비해 매우 작지만, 그 와중에 이상 데이터 간의 패턴도 다양함
2. Existence of multiple normal patterns
    - 정상 패턴이 다양하고 변화하기 때문에 이에 대처해야함(Data Drift)
3. Difficulty in representing dynamical features
5. Difficulty in parameter setting

이러한 문제점을 개선하기 위해, 'abnormal pattern recognition assumption'에 따라, 해당 논문에서는 주어진 데이터를 효과적으로 사용하기 위해 `Negative Selection`개념을 적용시켰습니다. 

Negative Selection Detector는 정상 데이터인 'self-set'과 비교해 일치하지 않는 데이터에 대해서 abnormal로 인지하게 되지만, 기존의 detector는 학습에 사용되지 않은 새로운 패턴에 대해서는 잘못 평가하게 될 가능성이 높습니다.

그렇기 때문에, 해당 논문에서는 'Unthresholded Recurrence Plot(URP)'을 활용해 시계열 데이터를 phase space에 Mapping시킴으로서, 표현적으로 드러나는 특성 보다는 데이터의 내면적 특성을 활용할 수 있는 방향으로 개선된 Negative Selection Detector를 제안하고 있습니다. 

URP(Unthresholded Recurrence Plot)이란, 시간의 변화에 따라 Phase Space Trajectory를 계산하고(Recurrence Plot), Phase Space Trajectory간의 거리를 계산할 때 사용되는 binary transformation의 threshold를 제거(Unthresholded)함으로서, 동적으로 변화하는 시스템(Dynamic System)을 분석하는 기법입니다.

Recurrence Plot에 대한 자세한 내용은 해당 포스트를 참고하시면 이해에 도움이 되실 것입니다.

[Recurrence Plot]()

결론적으로 해당 논문에서는, `Negative Selection, URP, Extreme Learning Machine Autoencoder(ELM-AE)`를 활용한 Anomaly Detection 방법론인 Robust Anomaly Detection for Time-series Data(RADTD)를 소개하게 될 것입니다.

# Related Work

## Negative Selection
Reference : [Negative Selection](https://m.blog.naver.com/irisfullip/60041797957)

Negative Selection은 생물학이나 유전학 등에서 차용된 방법으로,  
간단히 설명하자면(~~저도 잘모르지만...~~), T-cell이 항원을 인식할 때 T-cell의 수용체에서 self-MHC와 결합이 이루어져야만 항원을 인식할 수 있는데, 이때 이 결합이 이루어 지는 경우만 골라내고 나머지는 도태시키는 것이 `Positive Selection`,  
그리고 결합은 이루어지지만, 너무 강하게 일어나(Strong Bind) 떨어지지 않는 세포들을 도태시키는 것을 `Negative Selection`이라고 합니다.

해당 논문에서는 self-set(Positive Data)와의 결합이 너무 강하게 일어나 Anomaly를 찾아내지 못하고 Positive Data에 Overfitting된 경우를 솎아내고, 그렇지 않은 경우만을 골라내는 것을 `Negative Selection`의 개념으로 사용한 것으로 추측됩니다.

## Unthresholded Recurrnece Plot
RP(Recurrence Plot)은 역학(Dynamic System)적 관점에서 시계열 데이터를 2D이미지화 한 것입니다.