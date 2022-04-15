## 개요
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

## Wide & Deep
### Wide
	- Wide Model은 Feature들 간의 모든 경우의 수를 고려하기 때문에 좌우로 Wide한 형태를 띔

구글 플레이의 예를 통해 모델을 이해
- Wide에서 사용되는 input은  User가 설치한 앱 Feature와, 열람한 Feature간의 interaction

<img src="./img/image.png" width="800" height="100"/>
