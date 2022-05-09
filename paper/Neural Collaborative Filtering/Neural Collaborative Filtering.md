# [논문 리뷰] Neural Collaborative Filtering
- 16 Aug 2017

## 개요
- 본 논문은 user와 item간의 관계를 학습함에 있어 기존의 liner 방식에 기반한 MF의 한계를 지적
- Neural Net 기반의 architecture인 Neural Collaborative Filtering(NCF)를 제시함
-  이를 통해 보다 유연한 방식으로 두 관계를 표현할 수 있는 일반화된 MF 모델을 제안

	- MF 방식의 한계점
		- MF방식은 linear한 방식이기 때문에 user와 item간의 복잡한 관계를 표현하기에는 어려움이 있다. 이러한 한계를 해결하기 위하여 non-linear한 DNN의 multi-layer구조를 사용함

## Learning from implicit data
![image](https://user-images.githubusercontent.com/78646691/167337415-97e8175d-4df4-40da-812b-d4eff22767b7.png)
