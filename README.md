# wavelet-deepONet
Scrutinize every DeepONet associated with wavelet systems!

## [2019JSHK]PINN

- 기본적으로 미분방정식의 해 $u_p$를 neural network의 output $z = u_N(t,x)$와 같이 놓고 그걸 해에 근사할 수 있게 훈련하는 방식
- loss는 기본적으로 **governing eqution**, **initial condition**, **boundary condition**에 대해 정의하고 inverse problem의 경우에는 **parameter**에 대한 에러까지 추가
	- Forward problem: PDE와 물리적 파라미터 $p$가 주어졌을 때 PDE의 해 $u(t,x)$를 찾는 문제 $\rightarrow$ $p$는 고정
	- Inverse problem: PDE의 해나 관측 데이터가 주어졌을 때 그로부터 물리적 파라미터 $p$를 추정하는 문제 $\rightarrow$ $p$도 미지수
- Forward Problem Results (see `Section 3.1`):

	- `Theorem 3.2`: 미분 방정식이 smooth analytic solution $u_p$ 가 있을 때, loss를 임의로 작게 만드는 DNN의 파라미터가 존재한다.
	- `Theorem 3.3`: loss를 최소화하는 DNN의 파라미터로부터 만들어지는 $u_j$가 결과적으로 analytic solution $u_p$로 수렴하게 된다 (실제로는 analytic solution을 직접 알기 어렵기 때문에 유의미한 결과!).
- Inverse Problem Results (see `Section 3.2`)
	- `Theorem 3.4`
	
- See [this](https://chatgpt.com/share/690482b2-8478-8011-a701-022f0241ac97).