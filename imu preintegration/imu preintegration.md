<center><font color='green' size='8'> IMU Preintegration</font> </center>

## 1 IMU 传感器传感器

IMU传感器是输出：

<img src="./image/imu_sensor.bmp" alt="imu_sensor(1)" style="zoom: 15%;" />

其中：
$$
\begin{align}
\mathbf{a}_m &= \mathbf{R}_t^{T}(\mathbf{a}_t - \mathbf{g}_t) + \mathbf{a}_{bt} + \mathbf{a}_n \\
\mathbf{w}_m &= \mathbf{w}_t + \mathbf{w}_{bt} + \mathbf{w}_n
\end{align}
$$

* IMU传感器输出的<font color='red'>测量角速度 $\mathbf{w}_m$</font> ：毋庸置疑是角速度的真实值$\mathbf{w}_t$、角速度零偏$\mathbf{w}_{bt}$和高斯噪声$\mathbf{w}_n$组成。
* IMU传感器输出的<font color='red'>测量加速度 $\mathbf{a}_m$</font>  ：多出一个矩阵转换$\mathbf{R}_t^{T}$(惯性坐标系到IMU坐标系之间的转换)，去掉重力加速的影响$\mathbf{g_t} = [0\quad 0\quad-0.98]^{T}$、加速度零偏$\mathbf{a}_{bt}$和高斯噪声$\mathbf{a}_n$组成。

IMU输出的<font color='green'>理论真值</font>：
$$
\begin{align}
\mathbf{a}_t &= \mathbf{R}_t(\mathbf{a}_m - \mathbf{b}_t - \mathbf{a}_n) + \mathbf{g}_{t} \\
\mathbf{w}_t &= \mathbf{w}_m - \mathbf{w}_{bt} - \mathbf{w}_n
\end{align}
$$

## 2 运动学系统

### 2.1 匀速运动(constant velocity)

$$
\begin{align}
\dot{\mathbf{p}_t} &= \mathbf{v}_t \\
\dot{\mathbf{q}_t} &= \frac{1}{2}\mathbf{q}_t \otimes \mathbf{w}_t \\
\end{align}
$$

其离散形式：
$$
\begin{align}
\mathbf{p}_{n+1} &= p_n + \mathbf{v} \delta{t} \\
\mathbf{v}_{n+1} &= v_n 					   \\
\mathbf{q}_{n+1} &= q_n \otimes \mathbf{q}\{\mathbf{w}\delta{t}\} \\
\mathbf{w}_{n+1} &= w_n 
\end{align}
$$

### 2.2 匀加速运动(constant acceleration)

$$
\begin{align}
\dot{\mathbf{p}_t} &= \mathbf{v}_t \\
\dot{\mathbf{v}_t} &= \mathbf{a}_t \\
\dot{\mathbf{q}_t} &= \frac{1}{2}\mathbf{q}_t \otimes \mathbf{w}_t \\
\dot{\mathbf{a}_{bt}} &= \mathbf{a}_w \\
\dot{\mathbf{w}_{bt}} &= \mathbf{w}_w \\
\dot{\mathbf{g}_{t}} &= \mathbf{0} \\
\end{align}
$$

其离散形式：
$$
\begin{align}
\mathbf{p}_{n+1} &= p_n + \mathbf{v}_n \delta{t} + \frac{1}{2} \mathbf{a}_n \delta{t}^2\\
\mathbf{v}_{n+1} &= v_n + \mathbf{a}_n \delta{t} \\
\mathbf{a}_{n+1} &= a_n \\
\mathbf{q}_{n+1} &= q_n \otimes \mathbf{q}\{\mathbf{w}\delta{t} + \frac{1}{2} \alpha \delta{t}^2\} \\
\mathbf{w}_{n+1} &= w_n \\
\mathbf{\alpha}_{n+1} &= \mathbf{\alpha}_n
\end{align}
$$

## 3 李代数形式的位姿表示

