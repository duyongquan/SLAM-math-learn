<center><font color='green' size='8'>   四元数简介  </font></center>

## 1 四元数表示

### 1.1 定义

$$
\mathbf{q} = q_w + q_x + q_y + q_z
$$

## 2 四元数性质

### 2.1 四元数的和

$$
\mathbf{p} + \mathbf{q} = 
\begin{bmatrix}
p_w \\
\mathbf{p}_v
\end{bmatrix} + 

\begin{bmatrix}
q_w \\
\mathbf{q}_v
\end{bmatrix} = 

\begin{bmatrix}
p_w + q_w \\
\mathbf{p}_v + \mathbf{q}_v
\end{bmatrix} = 

\begin{bmatrix}
p_w + q_w  \\
\mathbf{p}_x + \mathbf{q}_x \\
\mathbf{p}_y + \mathbf{q}_y \\
\mathbf{p}_z + \mathbf{q}_z
\end{bmatrix}
$$

对应的元素直接相加即可。

### 2.2 四元数的乘积

$$
\mathbf{p} \otimes \mathbf{q} =

\begin{bmatrix}
	p_w & \mathbf{p}_x & \mathbf{p}_y & \mathbf{p}_z
\end{bmatrix} 

\begin{bmatrix}
	q_w & \mathbf{q}_x & \mathbf{q}_y & \mathbf{q}_z
\end{bmatrix} = 

\begin{bmatrix}
	p_w q_w  -p_x q_x - p_y q_y  -p_z q_z \\
	p_w q_x  +p_x q_w + p_y q_z  -p_z q_y \\
	p_w q_y  -p_x q_y + p_y q_w  +p_z q_x \\
	p_w q_z  +p_x q_z - p_y q_x  +p_z q_w \\
\end{bmatrix}
$$

写成标量和向量形式：
$$
\mathbf{p} \otimes \mathbf{q} =

\begin{bmatrix}
	q_w & \mathbf{q}_x & \mathbf{q}_y & \mathbf{q}_z
\end{bmatrix} = 

\begin{bmatrix}
	p_w q_w  - \mathbf{p}^T_v\mathbf{q}_v \\
	p_w \mathbf{q}_v  + q_w \mathbf{p}_v +\mathbf{p}_v \times \mathbf{q}_v
\end{bmatrix}
$$
<font color='red'> 四元数不满足交换律 </font>:
$$
\mathbf{p} \otimes \mathbf{q} \ne \mathbf{q} \otimes \mathbf{p}
$$
结合律：
$$
(\mathbf{p} \otimes \mathbf{q}) \otimes \mathbf{r}=  \mathbf{q} \otimes (\mathbf{p} \otimes \mathbf{r})
$$

### 2.3 矩阵形式

$$
\mathbf{q}_1 \otimes \mathbf{q}_2 = \mathbf{Q}^{+}\mathbf{q}_2 \\
\mathbf{q}_1 \otimes \mathbf{q}_2 = \mathbf{Q}^{-}\mathbf{q}_1
$$

其中：
$$
\mathbf{Q}^{+} =
q_w\mathbf{I} + 

\begin{bmatrix}  0 & -\mathbf{q}_v^{T} \\ 
\mathbf{q}_v & [\mathbf{q}_v]_{\times}

\end{bmatrix}  &&&

\mathbf{Q}^{-} =

q_w\mathbf{I} + 
\begin{bmatrix}  
	0 		      & -\mathbf{q}_v^{T} \\ 
	\mathbf{q}_v  & -[\mathbf{q}_v]_{\times}

\end{bmatrix}
$$


### 2.4 单位四元数

$$
\mathbf{q}_{1} = 1 =

\begin{bmatrix}
	1 \\
    \mathbf{0}_x 
\end{bmatrix}
$$

### 2.5 四元数共轭

共轭的定义：
$$
\mathbf{q}^{\star} \triangleq  q_w - \mathbf{q}_v =

\begin{bmatrix}
	q_w \\
    - \mathbf{q}_v
\end{bmatrix}
$$

### 2.6 四元数的模

$$
\| \mathbf{q}\| = \sqrt{q_w^2 + q_x^2 + q_y^2 + q_z^2}
$$

### 2.7 四元数的逆

$$
\mathbf{q} \otimes \mathbf{q}^{-1} = \mathbf{q}^{-1}  \otimes \mathbf{q} = \mathbf{q}_{1}
$$



## 3 四元数恒等式

### 3.1 旋转表示

$$
\mathbf{q}\{\theta\} = 

\cos{\frac{\theta}{2}} + \mathbf{u}\sin{\frac{\theta}{2}} = 

\begin{bmatrix}
	cos{\frac{\theta}{2}}\\
    \mathbf{u}\sin{\frac{\theta}{2}}
\end{bmatrix}
$$

### 3.2 向量旋转

$$
\begin{bmatrix}
	0 \\
    \mathbf{v}^{\prime}
\end{bmatrix} =

\mathbf{q} \otimes

\begin{bmatrix}
	0 \\
    \mathbf{v}
\end{bmatrix} \otimes

\mathbf{q}^{\star}
$$

### 3.3 旋转矩阵

$$
\mathbf{v}^{\prime} = \mathbf{R}\mathbf{v}
$$

其中：
$$
\mathbf{R}\{q\} = 
\begin{bmatrix}
	q_w^2 + q_x^2 - q_y^2 - q_z^2 & 2(q_xq_y - q_wq_z) & 2(q_xq_z + q_wq_y) \\
    2(q_xq_y + q_wq_z)            & q_w^2 - q_x^2 + q_y^2 - q_z^2 & 2(q_yq_z - q_wq_x) \\
    2(q_xq_z - q_wq_y)            & 2(q_yq_z + q_wq_x) & q_w^2 - q_x^2 - q_y^2 + q_z^2 
\end{bmatrix}
$$

### 3.4 导数

$$
\mathbf{\dot{q}} = \frac{1}{2} \mathbf{q} \otimes \mathbf{w}
$$

