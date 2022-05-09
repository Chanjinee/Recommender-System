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
![image](https://user-images.githubusercontent.com/78646691/167338865-9b473dbb-7b48-44f0-ae22-f2a721d4ed1a.png)

- 행렬 Y의 y_ui를 예측하기 위한 방법 중 하나는 MF를 이용하는 것.
- Y를 인수 분해하여 P와 Q의 latent factor를 구함.
- y_ui의 경우 P와 Q의 내적을 통해 추정하게 됨.

### The limitation of Matrix Factorization
![image](https://user-images.githubusercontent.com/78646691/167339155-4701e672-44c5-4dbd-8220-c2355e34c95b.png)

- 이 논문에서는 linear한 방법인 내적을 통해서는 user와 item간의 복잡한 관계를 표현하기가 어렵다고 설명함. 
- 왼쪽의 그림과 같은 행렬이 있고, s_ji는 user j와 i 의 유사도를 나타낸다.
- s_23(0.66)>s_12(0.50)>s_13(0.40) 인 관계가 성립하고 이를 기하학적인 그림으로 표현할 때, 오른쪽의 그림과 같이 표현됨.
- 이때, linear space의 한계는 user4에서 발생. 
- s_41(0.60)>s_43(0.40)>s_42(0.20)의 관계일 때, 4와 1을 가장 가깝게 하는 동시에 4와 2를 가장 멀게하는 p4벡터를 찾을 수 없는 문제가 발생. 

linear한 기존의 CF방식은 이와 같은 문제점을 가짐  
따라서 저자는 조금 더 유연한( linear의 문제점을 해결 ) DNN모델을 사용하여 해결하고자함

## Neural Collaborative Filtering
![image](https://user-images.githubusercontent.com/78646691/167341613-8d86981b-f5f8-4c1d-9fd5-ea3db873323d.png)

**1)Input Layer(sparse)**
- input layer에는 user와 item이 각각 따로 들어가게 됨.
- 각각의 벡터는 user한명, item한개를 one-hot encoding한 형태로 들어가게 됨.
- 즉, 0이 매우 많은 sparse한 형태를 갖게됨.

**2)Embedding Layer** 
- Embedding layer는  sparse한  input vector를  Dense하게 바꿔주는 역할을 함.
- 일반적인 임베딩 방법과 동일하게 fully-connected layer가 사용됩니다.
- Embedding Matrix를 통하여 M,N 차원의 user,item vector를 K차원의 latent space에 표현한 것으로도 생각해 볼 수 있음.

![image](https://user-images.githubusercontent.com/78646691/167342006-a0e09e2a-91c3-433b-8cfc-89cad7320adf.png)

- 이 P 행렬의 각 행은 각 user를 표현하는 저차원의 dense 벡터가 되고 이를 user latent vector로 사용하게 된다.
- 즉, one-hot encoding된 각각의 user는 embedding layer를 거쳐 P로 임베딩 된다.

**3)Neural CF Layers**
- 층에 들어갈 때, User latent vector와 Item latent vector를  concat한 벡터가 들어감
- 이후 각각의 층을 거치며 인공신경망을 통해 non-linear 관계를 학습할 수 있음.

**4)Output Layer**
- Output layer에서는 NCF layer의 hidden vector를 input으로 받아 predictive score y_hat_ui를 예측하며, Target인 y_ui와의 비교를 통해 학습이 진행됨.


