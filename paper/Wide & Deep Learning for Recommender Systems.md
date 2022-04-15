## Abstract
- Memorization에 특화된 Wide모델과, Generalization에 특화된 Deep 모델을 결합한 Wide and deep모델을 제안
- 각 모델의 장점을 통하여 더 좋은 모델을 만들어 냄

	|	방법			|		장점	  |		단점|
	|		---			|			---			|		-------		|
	| Wide Model | Memorization  |  발견하지 못한 부분에 대해서는 무지	 |
	| Deep Model | Generalization |  세부적으로 기억하지 못함  |
	
	- ex)
	- 참새는 날 수 있다. 까치는 날 수 있다. 펭귄은 날지 못한다. 등 -> Wide  / Memorization
	- 날개를 가진 모든 새들은 날 수 있다. -> Deep / Generalization
	- 모든 날개를 가진 새들은 날 수 있지만 펭귄, 등 예외인 동물이 있다. -> Wide & Deep

## Introduction
### Wide
	- Wide Model은 Feature들 간의 모든 경우의 수를 고려하기 때문에 좌우로 Wide한 형태를 띔

구글 플레이의 예를 통해 모델을 이해
- Wide에서 사용되는 input은  User가 설치한 앱 Feature와, 열람한 Feature간의 interaction

![image](https://user-images.githubusercontent.com/78646691/163551466-95e0518c-3d9b-4e0f-9eae-e0e42f75150f.png)



	- User가 해당 앱을 설치했으면 1, 아니면 0  
	- User가 해당 앱을 봤으면 1, 아니면 0 
	- 위의 결과를 바탕으로 결과를 단순히 곱하여 input으로 사용
![image](https://user-images.githubusercontent.com/78646691/163551797-230283f3-3190-4177-8e51-25f24b14d914.png)

- 위의 그림을 보면 나올 수 있는 모든 경우의 수 9가지 중, input이 1이 나오는 경우는 4가지이다.

- 장점
	- 해당 방식은 1이 되는 모든 경우의 수를 학습하기 때문에 Memorization에 강함
	 - User의 특이 취향이 반영된 Niche(논문에서 ‘주변환경’의 의미로 쓰임) Combination을 학습하기에 탁월 
	 - ex) 여행과 관련된 Airbnb앱을 깔았고, 야놀자, 여기어때 등의 앱을 본 기록이 있다면 해당 사용자는 여행에 관심이 있다는 것을 쉽게 알 수 있음
- 단점
	- 0이 되는 pair는 학습이 불가능

### Deep
	- 학습을 하는 과정에서 딥러닝 MLP기법을 사용함
	
![image](https://user-images.githubusercontent.com/78646691/163553993-807de1f9-a83b-4b38-b1a5-8f46de9de9e7.png)

구글 플레이의 예를 통해 모델을 이해

- Deep 모델은 A, B, C 앱을 동일한 임베딩 공간에 표현. (단순히 해당 값을 임베딩하여 input으로 넣음)
- 장점 
	- wide에서의 단점인 pair가 없는 관계 또한 학습이 가능
	- 즉, Generalization에 강점을 가지고 있음
- 단점 
	- pair가 없었던, 이런 앱들은 다른 앱과의 관계를 제대로 표현하지 못한 임베딩 벡터를 가질 가능성이 큼
	- 희소한 앱들은 학습이 잘 안되기 때문에 전혀 관계없는 아이템들이 추천될 수도 있음
