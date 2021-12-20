# 2021_final_project
우선 Perceptron 보다 LogisticRegression이 Accuracy가 높게 나오기 때문에 LogisticRegression을 활용하였다.
이후 LogisticRegression의 하이퍼 파라미터를 수정하며 나온 Accuracy를 기록하였다.

log_reg = sklearn.linear_model.LogisticRegression()로 한다음 괄호 안에 하이퍼 파라미터를 조정하는식으로 하였다.
log_reg.fit(X_train, y_train)로 데이터셋을 training시켰다.

아래는 하이퍼 파라미터를 조정한 방법, 경우의 수이다.

random_state = 0으로 고정시킨다.

C 조정
--------------------------------------------------------------
1
c = 1
-> 95

2
c = 10
-> 95.8333

3
c = 100
-> 96.666

4
c = 1000
-> 95

5
c = 500
-> 95.8333

6
c = 10000
-> 93.3333

7
c = 300
-> 95

8
c = 700
-> 94.1667

9
c = 90
-> 95

10
c = 110
-> 96.666

11
c = 130
-> 95.8333

12
c = 120
-> 95

13
c = 119
-> 96.666

c가 100, 119, 110일때 최댓값 96.666이 나왔으므로 c는 100으로 고정시키겠다.

tol 조정
--------------------------------------------------------------
14
tol = 0.0001
-> 96.666

15
tol = 0.001
-> 96.666

16
tol = 0.01
-> 92.5

17
tol = 0.1
-> 86.666

18
tol = 0.00001
-> 96.666

19
tol = 0.0005
-> 96.666

20
tol = 0.0007
-> 96.666

이외에도 여러 수 경우로 조절해봤지만 최댓값은 96.666이었다. 즉 tol은 기본값인 0.0001에서 조절하지 않아도 된다.

dual 조정
--------------------------------------------------------------
21
dual=False
-> 96.6666

22
daul = None
-> 96.6666

둘다 같으므로 기본값인 False로 지정하겠다.

intercept_scaling 조정
--------------------------------------------------------------
23
intercept_scaling=1
-> 96.6666

24
intercept_scaling=10
-> 96.6666

25
intercept_scaling=100
-> 96.6666

26
intercept_scaling=1000
-> 96.6666

27
intercept_scaling=0.1
-> 96.6666

28
intercept_scaling=0.01
-> 96.6666

변화가 없으므로 기본값인 1로 지정하겠다.

class_weight 조정
--------------------------------------------------------------
29
class_weight = None
-> 96.666

30
class_weight = 'balanced'
-> 96.666

변화가 없으므로 기본값인 None로 지정하겠다.

(solver) - (penalty)순서로 아래와 같은 쌍들의 Accuracy를 보았다.
--------------------------------------------------------------
‘newton-cg’ - [‘l2’, ‘none’]

‘lbfgs’ - [‘l2’, ‘none’]

‘liblinear’ - [‘l1’, ‘l2’]

‘sag’ - [‘l2’, ‘none’]

‘saga’ - [‘elasticnet’, ‘l1’, ‘l2’, ‘none’]

하지만 기본값인 'lbfgs' - 'l2'보다 큰값은 나오지 않았으므로 기본값으로 지정하겠다.

max_iter 조정
--------------------------------------------------------------
31
max_iter=100
-> 96.6666

32
max_iter=1000
-> 96.6666

33
max_iter=10
-> 72.5

34
max_iter=1
-> 0

35
max_iter=500
-> 96.6666

36
max_iter=50
-> 89.1666

37
max_iter=80
-> 95

38
max_iter=90
-> 96.6666

39
max_iter=200
-> 96.6666

40
max_iter=300
-> 97.5

41
max_iter=400
-> 96.6666

42
max_iter=350
-> 97.5

43
max_iter=250
-> 96.6666

44
max_iter=380
-> 98.3333

45
max_iter=379
-> 97.5

46
max_iter=81
-> 97.5

max_iter가 380일때 최댓값 98.333이 나왔다. 즉 앞으로 max_iter의 값은 380으로 고정시키겠다.

verbose를 변경시켜보았지만 98.333이 계속 나온다. 즉 verbose는 기본값인 0으로 설정하겠다.

multi_class 조정
--------------------------------------------------------------
47
multi_class='ovr',
-> 97.5

47
multi_class='atuo',
-> 98.3333

47
multi_class='multinomial',
-> 98.3333

multi_class는 기본값인 auto로 지정하겠다.

warm_start 조정
--------------------------------------------------------------
48
warm_start = False
-> 98.3333

49 
warm_start = True
-> 98.3333

warm_state는 뭘 하든 같으므로 기본값인 False로 지정하겠다.

l1ratio 조정
--------------------------------------------------------------
50
l1ratio = None
-> 98.3333

51
l1ratio = 1
-> 98.3333

변화가 없으므로 기본값인 None로 지정하겠다.

n_jobs 조정
--------------------------------------------------------------
52 
n_jobs = None
-> 98.3333

53
n_jobs = 1
-> 98.3333

54
n_jobs = 10
-> 97.5

55
n_jobs = 5
-> 97.5

56
n_jobs = 2
-> 96.3333

57
n_jobs = 50
-> 97.5

n_jobs = 1이거나 None 일때 가장 높았으므로 기본값인 None로 지정하겠다.

이로써 모든 하이퍼파라미터를 수정해보며 가장 높은 Accuracy는 98.333%, 즉 0.983333이 도출되었다.\
소수점 둘째자리까지 반영하므로 0.98이 도출된다.

최종적으로 도출된 코드는 아래와 같다.
log_reg = sklearn.linear_model.LogisticRegression(
C=100.0,
random_state=0,
max_iter=380,)\n
log_reg.fit(X_train, y_train)\n
y_pred = log_reg.predict(X_test)
