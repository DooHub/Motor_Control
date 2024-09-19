# 1. Transform
--> BLDC 3상 모터를 제어하기 위해 알아야한 기본 배경 지식으로 Park와 Clark Transform에 대해서 알아 본다.  
--> 3상 모터는 AC로 제어해야 하기 때문에 시변을 고려할 경우 복잡하다. Tranform을 통해 AC제어를 DC로 제어 할 수 있다.  
--> 단계는 3상 전류 -> Alpha와 Beta 직교 좌표 변환(Clark Transform) -> Id와 Iq 직교 회전 좌표로 변환(Park Trnasform)

# 2. 기본 배경
### 1) 3상 모터의 구조 : Y 결선 구조로 되어 있고 각 상을 U, V, W 혹은 a, b, c라고 한다.
### 2) KCL 법칙 : Y결선에 구조로 들어온 전류와 나간 전류의 합은 '0'이 되어야 한다.

# 3. Clark Transform
### 3상에 흐르는 전류 벡터를 Alpha와 Belta의 직교 좌표로 변환 한다.
