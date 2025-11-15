# wavelet-deepONet
Scrutinize every DeepONet associated with wavelet systems!

# Physics Informed Neural Networks

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

---------

# Operator Learning

## [2025LanthalerLiStuart]Nonlocality_and_nonlinearity_implies_universality_in_OL

- Neural operator계의 뉴클래식, 뉴 Cybenko, Hornik 결과
- Neural operator에서의 UAT를 주기 위해서의 최소한의 nonlocality와 nonlinearity를 규명함
	- Nonlocality: operator는 입력함수의 값이 전역에 영향을 주기 때문에 nonlocality를 필수적으로 가져야 함
	$\Rightarrow$ integral (averaging)로 나타냄, 이 논문에서는 averaging 하나 정도면 UAT에는 충분하다를 보임
	- Nonlinearity: 이건 뭐 말모...
	$\Rightarrow$ Channel수로 조절, 이 논문에서는 lifting operator의 채널수로 제시를 하고 shallow로도 UAT보이기엔 충분하다고 주장
- Experiments 
	- parameter수 (channel수 * mode수)가 늘수록 error가 낮아짐 (당연)
	- 하지만 최적의 mode수는 문제마다 다름. 아직은 뭔가가 필요함 ([29] 논문에서는 mode는 고정하고 채널 수(nonlinearity)가 중요하다고 했던 것 같은데 꼭 그런것만은 아닐지도?)
- See [this](https://chatgpt.com/share/69181e5b-569c-8011-a2b4-799af9cc19ab)
	
## [2023ICLR]Lanthaler_Nonlinear_reconstruction_for_operator_learning_of_PDEs_with_discontinuities

- 위 논문의 [29]번 레퍼런스
- 전통적으로 푸리에의 주파수 basis (mode)를 늘리면 더 나은 퍼포먼스를 얻을 수 있다고 알려져 있었는데, 실제 실험을 하다보면 그게 아닌거라.
- 그래서 실제로 mode는 제한하고 nonlinearity를 늘렸을 때 더 나았다는 것을 이론과 실험으로 보였다고 함.
- 기존의 DeepONet은 linear하기 때문에 그걸 nonlinear하게 할 수 있도록 shift-DeepONet를 도입하고 (여기선 mode가 등장하는 건 아닌듯),
FNO는 실제로 mode와 nonlinearity(channel수)를 활용.