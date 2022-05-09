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

- M 과 N은 각각 user와 item 개수이고 Y는 user-item 행렬
- yu,i=1은 user u 와 item i 간의 상호작용이 있음을 나타냄  
- 	
	상호작용?
	- user가 item을 열람했거나, 구매했거나 등의 implicit한 정보를 의미  
	- 주의할 점은 이것이 explicit한 선호를 뜻하진 않는다는 것.  
	- 따라서 yu,i=0yu,i=0은 해당 item에 대한 user의 선호를 나타내는 것은 아님

- user의 item에 대한 선호를 분명하게 알지 못한다는 것이 문제점이 됨
- ex) user가 특정 item을 좋아할 수 있더라도 해당 item을 모른다면 값은 0이 됨
- 결국 user가 모르는 item중에서 user가 좋아할 것이라고 생각되는 item을 예측하는 문제가 됨

## Matrix Factorization
행렬 Y의 y_ui를 예측하기 위한 방법 중 하나는 MF를 이용하는 것.
![image](https://user-images.githubusercontent.com/78646691/167338865-9b473dbb-7b48-44f0-ae22-f2a721d4ed1a.png)
