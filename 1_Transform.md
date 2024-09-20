<a href ="https://zin9.tistory.com/16">참고사이트</a>
# 1. Transform
--> BLDC 3상 모터를 제어하기 위해 알아야한 기본 배경 지식으로 Park와 Clark Transform에 대해서 알아 본다.  
--> 3상 모터는 AC로 제어해야 하기 때문에 시변을 고려할 경우 복잡하다. Tranform을 통해 AC제어를 DC로 제어 할 수 있다.  
--> 단계는 3상 전류 -> Alpha와 Beta 직교 좌표 변환(Clark Transform) -> Id와 Iq 직교 회전 좌표로 변환(Park Trnasform)

# 2. 기본 배경
### 1) 3상 모터의 구조 : Y 결선 구조로 되어 있고 각 상을 U, V, W 혹은 a, b, c라고 한다.
### 2) KCL 법칙 : Y결선에 구조로 들어온 전류와 나간 전류의 합은 '0'이 되어야 한다.

# 3. Clarke Transform
### 3상에 흐르는 전류 벡터를 Alpha와 Belta의 직교 좌표로 변환 한다.
### U상을 기준으로 V와 W는 120도의 위상차를 가지고 있다.  
### Alpha좌표는 U상과 동기화 되어 있는 상태로 Transformd을 진행 한다.
<img src="https://github.com/user-attachments/assets/92082801-c3d8-4632-bf23-e9c9066b46c7">  

### 1) $i_\alpha = i_ucos(0^{\circ})+i_vcos(120^{\circ})+i_wcos(-120^{\circ})=i_u+\frac{-1}{2}i_v+\frac{-1}{2}i_w=i_u+\frac{-1}{2}(i_v+i_w)$
### 2) $i_\beta = i_usin(0^{\circ})+i_vsin(120^{\circ})+i_wsin(-120^{\circ})=i_u\times0+\frac{\sqrt{3}}{2}i_v+\frac{-\sqrt{3}}{2}i_w=\frac{\sqrt{3}}{2}(i_v-i_w)$
### 3) $i_{0} = i_u+i_v+i_w=0$

---
### 3)의 식을 1)과 2)적용하여 다음과 같이 간단히 식을 정리 할 수 있다.
### $i_\alpha =i_u+\frac{-1}{2}(i_v+i_w)=\frac{3}{2}i_u$  
### $i_\beta = \frac{\sqrt{3}}{2}(i_v-i_w)=\frac{\sqrt{3}}{2}(2i_v+i_u)$  
### 위 내용을 행렬로 표시하면  

$$\begin{bmatrix}
i_\alpha \\
i_\beta
\end{bmatrix}
=\begin{bmatrix}
\frac{3}{2} & 0 & 0 \\
\frac{\sqrt{3}}{2}&\frac{2\sqrt{3}}{2}  & 0
\end{bmatrix}
\begin{bmatrix}
i_u \\
i_v \\
i_w
\end{bmatrix}$$

### Alpha가 U상과 같은 크기를 가지게 하기 위해 $\frac{2}{3}$을 곱해서 위식을 다시 정리하면  

$$\begin{bmatrix}
i_\alpha \\
i_\beta
\end{bmatrix}
=\begin{bmatrix}
1 & 0 & 0 \\
\frac{1}{\sqrt{3}}&\frac{2}{\sqrt{3}}  & 0
\end{bmatrix}
\begin{bmatrix}
i_u \\
i_v \\
i_w
\end{bmatrix}$$

# 4. Park Transform
### Alpha와 Beta는 여전히 상수가 아닌 Phase전류 변환에 따라 값이 바뀐다. 따라서 고정된 축을 만들고 이를 회전하는 방법을 적용 할 필요가 있다.
### d와 q축을 만들고 축이 Alpha축을 중심으로 시계 반대 방향으로 회전 한다고 할 때 d와 q를 구해 보자
## Alpha와 d축 사이의 각 Theta는 각속도를 나타낸다.

<img src="https://github.com/user-attachments/assets/eed56246-489b-46c7-8372-3983f8a14962">

### 1) $i_d=i_\alpha\times cos\theta + i_\beta \times sin\theta$
### 2) $i_q=i_\alpha\times -cos(\frac{\pi}{2}-\theta) + i_\beta \times sin(\frac{\pi}{2}-\theta)=i_\alpha\times -sin\theta + i_\beta \times cos\theta$

### 상기 내용을 Matrix로 표현하면 다음과 같다.  

$$\begin{bmatrix}
i_d \\
i_q
\end{bmatrix}
=\begin{bmatrix}
cos\theta & sin\theta \\
-sin\theta & cos\theta 
\end{bmatrix}
\begin{bmatrix}
i_\alpha \\
i_\beta
\end{bmatrix}$$

# 5. 최종정리
### Clarke 와 Park Transform을 정리하여 표현하면 다음과 같다.  

$$\begin{bmatrix}
i_d \\
i_q
\end{bmatrix}=
\begin{bmatrix}
cos\theta & sin\theta \\
-sin\theta & cos\theta 
\end{bmatrix}
\begin{bmatrix}
1 & 0 & 0 \\
\frac{1}{\sqrt{3}} & \frac{2}{\sqrt{3}} & 0
\end{bmatrix}
\begin{bmatrix}
i_u \\
i_v \\
i_w
\end{bmatrix}=
\begin{bmatrix}
 cos\theta+\frac{sin\theta}{\sqrt{3}}& \frac{2sin\theta}{\sqrt{3}} & 0 \\
 -sin\theta+\frac{cos\theta}{\sqrt{3}}&\frac{2cos\theta}{\sqrt{3}}  & 0 
\end{bmatrix}
\begin{bmatrix}
i_u \\
i_v \\
i_w
\end{bmatrix}$$
### id와 iq는 iu와 iv로 정리 할 수 있다.
### $\bullet i_d= (cos\theta+\frac{sin\theta}{\sqrt{3}})i_u+\frac{2sin\theta}{\sqrt{3}}iv$
### $\bullet i_q= (-sin\theta+\frac{cos\theta}{\sqrt{3}})i_u+\frac{2cos\theta}{\sqrt{3}}iv$
----
### Alpha와 Beta로 변환 시 에너지 보존 법칙을 위배 되는 현상이 있기 때문에 이부분에 대한 보안이 필요 하다.
