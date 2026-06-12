# Average-cost Bellman equation and differential value function

This is an Markdown sample of a qualified math explaination conversation.

## Metadata

- Language: Vietnamese
- Scope: visible current chat excerpt only
- Internal/system/developer messages: excluded

## Conversation

### Turn u1 - user

The user provides an image containing the following formulation:

For the average cost, let \(h \in \mathbb{R}^{\mathcal{X}}\) be a vector and \(\lambda \in \mathbb{R}\) a scalar. The Bellman operator for average cost is

\[
Lh(x) \overset{\mathrm{def}}{=} \min_{a\in[A]}\left[\ell(x,a)+\sum_{x'\in\mathcal{X}}P_{(x,a),x'}h(x')\right],
\]

and \(h\) and \(\lambda\) correspond to an optimal policy if they satisfy

\[
\lambda+h(x)=Lh(x)\quad \forall x.
\]

User asks: formulation này khá dị, bạn giải thích được không

### Turn a1 - assistant

Formulation này “dị” vì average-cost Bellman equation <strong>không phải fixed point thường</strong> \(h=Lh\), mà là <strong>additive eigenvalue problem</strong>:

\[
Lh = h + \lambda \mathbf{1}.
\]

Ở đây \(\lambda\) là <strong>optimal long-run average cost per step</strong>, còn \(h(x)\) là <strong>bias / relative value / differential value</strong> của state \(x\). Nó đo chi phí transient phụ thêm khi bắt đầu từ \(x\), sau khi đã trừ đi tốc độ tăng tuyến tính \(\lambda\).

Cụ thể, objective average cost thường là

\[
J^\pi(x)=\limsup_{T\to\infty}\frac{1}{T}\mathbb{E}_x^\pi\left[\sum_{t=0}^{T-1}\ell(X_t,A_t)\right].
\]

Trong discounted MDP, value hữu hạn vì có \(\gamma<1\), nên ta có fixed point:

\[
V(x)=\min_a\left[\ell(x,a)+\gamma \sum_{x'}P(x'|x,a)V(x')\right].
\]

Nhưng với average cost, tổng chi phí dài hạn tăng xấp xỉ tuyến tính theo horizon:

\[
V_T(x)\approx T\lambda+h(x).
\]

Finite-horizon DP có recursion

\[
V_{T+1}(x)=\min_a\left[\ell(x,a)+\sum_{x'}P(x'|x,a)V_T(x')\right].
\]

Thay ansatz \(V_T(x)\approx T\lambda+h(x)\) vào:

\[
(T+1)\lambda+h(x)=\min_a\left[\ell(x,a)+\sum_{x'}P(x'|x,a)(T\lambda+h(x'))\right].
\]

Vì \(\sum_{x'}P(x'|x,a)=1\), vế phải chứa \(T\lambda\). Khử \(T\lambda\), ta được

\[
\lambda+h(x)=\min_a\left[\ell(x,a)+\sum_{x'}P(x'|x,a)h(x')\right].
\]

Đó chính là phương trình trong ảnh.

Điểm quan trọng: \(h\) <strong>không phải value tuyệt đối</strong>. Nó chỉ xác định tới một hằng số cộng thêm. Nếu \(h\) là nghiệm thì \(h+c\mathbf{1}\) cũng là nghiệm, còn \(\lambda\) không đổi:

\[
L(h+c\mathbf{1})=Lh+c\mathbf{1}=h+\lambda\mathbf{1}+c\mathbf{1}.
\]

Vì vậy trong LP hoặc thuật toán, người ta thường fix gauge như \(h(x_0)=0\) hoặc \(\sum_x h(x)=0\).

Liên hệ với LP: phương trình optimality tương đương với hệ bất đẳng thức dual

\[
\lambda+h(x)\le \ell(x,a)+\sum_{x'}P(x'|x,a)h(x')\qquad \forall x,a,
\]

và ta maximize \(\lambda\) trong dual của primal occupancy LP cho bài toán minimization. Action tối ưu là action đạt dấu bằng:

\[
a^*(x)\in\arg\min_a\left[\ell(x,a)+\sum_{x'}P(x'|x,a)h(x')\right].
\]

Một lưu ý kỹ thuật: phát biểu “\(h\) và \(\lambda\) correspond to an optimal policy” thường cần giả thiết finite MDP và dạng unichain/communicating. Nếu MDP multichain, average cost có thể phụ thuộc vào initial state, lúc đó một scalar \(\lambda\) toàn cục có thể không đủ.

### Turn u2 - user

tôi chưa từng gặp differential value function. Tôi hiểu chắc là reward có thể sai khác hằng số cộng thì policy vẫn không đổi, do đó ta chuẩn hóa h, đúng không?

### Turn a2 - assistant

Gần đúng, nhưng cần tách hai ý.

<strong>Ý chính:</strong> differential value function \(h\) không được chuẩn hóa vì reward/cost sai khác một hằng số, mà vì trong average-cost Bellman equation, \(h\) tự nó chỉ xác định tới một hằng số cộng.

Với một policy cố định \(\pi\), phương trình là

\[
\lambda^\pi+h^\pi(x)=\ell_\pi(x)+\sum_{x'}P_\pi(x,x')h^\pi(x').
\]

Ở đây \(\lambda^\pi\) là average cost dài hạn, còn \(h^\pi(x)\) là <strong>relative cost-to-go</strong>: bắt đầu từ state \(x\) thì trong transient phase ta tốn nhiều hơn hay ít hơn bao nhiêu so với mức trung bình dài hạn \(\lambda^\pi\).

Một cách hiểu tốt là

\[
h^\pi(x)\approx \mathbb{E}_x^\pi\left[\sum_{t\ge 0}\bigl(\ell(X_t,A_t)-\lambda^\pi\bigr)\right],
\]

nhưng biểu thức vô hạn này cần điều kiện ergodic hoặc cần định nghĩa qua reference state. Nếu chọn một state mốc \(x_0\), có thể viết kiểu

\[
h^\pi(x)=\mathbb{E}_x^\pi\left[\sum_{t=0}^{\tau_{x_0}-1}\bigl(\ell(X_t,A_t)-\lambda^\pi\bigr)\right],
\]

với \(\tau_{x_0}\) là thời điểm chạm lại \(x_0\). Cách này ngầm đặt \(h^\pi(x_0)=0\).

Lý do phải chuẩn hóa là do bất biến sau:

\[
h \mapsto h+c\mathbf{1}.
\]

Thật vậy,

\[
\ell(x,a)+\sum_{x'}P(x'|x,a)(h(x')+c)=\ell(x,a)+\sum_{x'}P(x'|x,a)h(x')+c.
\]

Do đó nếu

\[
\lambda+h(x)=\min_a\left[\ell(x,a)+Ph(x,a)\right],
\]

thì \(h+c\mathbf{1}\) cũng là nghiệm với cùng \(\lambda\). Policy cũng không đổi vì argmin không đổi.

Còn chuyện <strong>reward/cost cộng thêm hằng số</strong> là một invariance khác. Nếu dùng cost và thay

\[
\ell'(x,a)=\ell(x,a)+c,
\]

thì average cost đổi thành

\[
\lambda'=\lambda+c,
\]

còn \(h\) có thể giữ nguyên, trừ gauge. Policy tối ưu không đổi vì mọi action đều bị cộng cùng một lượng tại mỗi bước.

Vậy kết luận ngắn gọn:

\[
\text{reward shift affects } \lambda,\qquad \text{value gauge affects } h.
\]

Differential value \(h\) là phần “lệch tương đối theo state” sau khi đã tách tốc độ tăng tuyến tính dài hạn \(\lambda\). Chuẩn hóa \(h\) là fix gauge, ví dụ \(h(x_0)=0\) hoặc \(\sum_x h(x)=0\), chứ không phải trực tiếp do reward có thể cộng hằng số.

## Tags

- `topic: average-cost MDP`
- `concept: differential value function`
- `concept: additive eigenvalue problem`
- `concept: Bellman optimality equation`
- `invariance: value gauge`
- `invariance: reward shift`
