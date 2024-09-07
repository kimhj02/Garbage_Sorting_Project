# Garbage_Sorting_Project
## 1. Purpose
기술이 발전함에 따라, 일회용 쓰레기 및 여러가지 종류의 쓰레기들이 발생하고 있다. 이렇게 다양한 쓰레기가 발생하면서 쓰레기 재활용에도 어려움을 겪고 있다. 현재, 우리나라의 경우 개인이 쓰레기를 배출할 때, 분리하여 버리는걸로 되어있지만, 이러한 분류 과정에서 불편함을 느껴 쓰레기를 분류하지 않고 버리는 사람들이 존재한다. 그렇다면 이러한 문제를 해결하기 위해 어떤 방법이 있을까
## 2. Solution 
개인이 쓰레기를 종류에 상관없이 배출했을 때, 이러한 쓰레기를 자동으로 분류해준다면 분리수거가 되지 않는 문제를 막을 수 있을 것이다. 그렇다면 이러한 자동 분류는 어떻게 진행해야하는가?
### 2_1. 쓰레기를 받기 위한 컨베이어 시스템
컨베이어 시스템을 실제로 구성하기 위해서는 2개의 강력한 dc모터가 필요하다. 하지만 이러한 dc모터는 가격이 비싸기 때문에 우리는 이러한 강력한 모터가 아닌 작은 모터 2개를 pvc파이프로 연장 한 후, 벨트로 pvc파이프 2개를 연결하여 컨베이어 벨트를 만들 것이다. 이렇게 만든 컨베이어 벨트 위에 물체가 올라간 것을 초음파 센서로 감지하고, 카메라로 촬영하기위한 위치까지 벨트를 이동시킨다.
### 2_2. 쓰레기를 받아 어떤 종류인지 판별하는 학습 모델
분류는 cnn 모델을 이용한다. <br>
https://github.com/standfsk/waste_classification <br>
해당 모델을 이용하여 ai허브에 있는 생활 폐기물 이미지 데이터셋을 이용한다. <br>
https://www.aihub.or.kr/aihubdata/data/view.do?currMenu=&topMenu=&aihubDataSe=data&dataSetSn=140 <br>
331GB의 데이터를 모드 사용하기에는 너무 많은 시간이 필요할 수 있으므로, 데이터의 수를 줄이고 Epoch 수를 늘리는 방향을 선택한다. <Br>
data_set은 train_set 80% test_set 20% 정도로 사용한다. 이러한 모델은 결과치에 따라 유동적으로 변환하여 사용할 수 있다.<br>
### 2_3. 어떤 종류의 쓰레기인지 판별한 후, 쓰레기를 이동시키는 엑츄에이터
이렇게 판별된 결과에 따라 쓰레기를 이동시켜 분류한다. 분류하는 방법은 2가지 방법 중 하나로 사용한다.
#### Sol1 리니어 액추에이터를 이용한 분류
- 장점
1. 강력한 힘: 리니어 액추에이터는 큰 힘을 필요로 하는 무거운 쓰레기를 분류할 때 유리하다.
2. 정확한 직선 운동: 액추에이터는 직선 운동을 제공하므로 쓰레기를 일정한 방향으로 밀거나 이동시키기에 적합하다.
3. 내구성: 견고하게 설계된 리니어 액추에이터는 오래 사용할 수 있으며, 물리적인 충격에도 강하다.
4. 안정적인 작동: 부하가 걸려도 안정적으로 작동할 수 있어 큰 물체나 다양한 종류의 쓰레기를 처리하는 데 유리하다.
- 단점
1. 비용: 리니어 액추에이터는 서보 모터에 비해 상대적으로 비싸고, 더 복잡한 시스템을 요구할 수 있다.
2. 속도: 리니어 액추에이터는 상대적으로 동작 속도가 느릴 수 있어 대량의 쓰레기를 빠르게 분류하는 데 제한이 있을 수 있다.
3. 복잡한 설치: 직선 운동을 요구하는 시스템에서는 설치가 더 복잡하고, 관리도 까다로울 수 있다. <br>
   
#### Sol2 서버 모터를 이용한 분류
- 장점
1. 정밀 제어: 서보 모터는 각도와 위치를 매우 정확하게 제어할 수 있어, 작은 쓰레기들을 세밀하게 분류하는 작업에 적합하다.
2. 유연성: 서보 모터는 다양한 동작 패턴을 지원할 수 있으며, 필요한 곳에 정확한 움직임을 제공할 수 있다.
3. 속도: 서보 모터는 리니어 액추에이터에 비해 동작 속도가 빠르며, 더 빠르게 쓰레기를 분류할 수 있다.
4. 비용: 서보 모터는 상대적으로 저렴하며, 시스템에 따라 더 경제적인 선택일 수 있다.
- 단점
1. 힘의 제한: 서보 모터는 리니어 액추에이터에 비해 힘이 약해, 무거운 쓰레기를 처리하는 데는 적합하지 않을 수 있다.
2. 제한된 움직임: 서보 모터는 회전 운동을 주로 하므로, 직선 운동이 필요한 분류 작업에는 추가적인 메커니즘이 필요할 수 있다.
3. 내구성 문제: 과도한 부하가 걸리면 내구성이 떨어질 수 있으며, 고장 확률이 증가할 수 있다.

  
