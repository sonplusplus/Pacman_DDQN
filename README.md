<a id="readme-top"></a>


<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/username/pacman-double-dqn">
    <img src="https://hoanghamobile.com/tin-tuc/wp-content/uploads/2024/03/pac-man-thumb.jpg" alt="Logo" width="80" height="80">
  </a>

<h3 align="center">Pacman Double DQN</h3>

  <p align="center">
    Dự án huấn luyện AI chơi Pacman sử dụng Double Deep Q-Learning
    <br />
    <a href="https://github.com/username/pacman-double-dqn"><strong>Khám phá tài liệu »</strong></a>
    <br />
    <br />
    <a href="https://github.com/username/pacman-double-dqn">Xem Demo</a>
    &middot;
    <a href="https://github.com/username/pacman-double-dqn/issues/new?labels=bug">Báo lỗi</a>
    &middot;
    <a href="https://github.com/username/pacman-double-dqn/issues/new?labels=enhancement">Đề xuất tính năng</a>
  </p>
</div>

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Mục lục</summary>
  <ol>
    <li>
      <a href="#giới-thiệu">Giới thiệu</a>
      <ul>
        <li><a href="#xây-dựng-bằng">Xây dựng bằng</a></li>
      </ul>
    </li>
    <li>
      <a href="#bắt-đầu">Bắt đầu</a>
      <ul>
        <li><a href="#yêu-cầu">Yêu cầu</a></li>
        <li><a href="#cài-đặt">Cài đặt</a></li>
      </ul>
    </li>
    <li><a href="#cách-sử-dụng">Cách sử dụng</a></li>
    <li><a href="#lộ-trình">Lộ trình</a></li>
    <li><a href="#đóng-góp">Đóng góp</a></li>
    <li><a href="#giấy-phép">Giấy phép</a></li>
    <li><a href="#liên-hệ">Liên hệ</a></li>
    <li><a href="#lời-cảm-ơn">Lời cảm ơn</a></li>
  </ol>
</details>

<!-- ABOUT THE PROJECT -->

## Giới thiệu

![Pacman Screenshot][product-screenshot]

Dự án này sử dụng thuật toán Double Deep Q-Learning Network (Double DQN) để huấn luyện agent chơi trò chơi Pacman.
Double DQN là một phiên bản cải tiến của DQN giúp giảm thiểu hiện tượng overestimation bias trong học tăng cường.

Đặc điểm chính của dự án:

* Sử dụng Double DQN để huấn luyện agent chơi Ms. Pacman
* Xử lý frame hình và kỹ thuật frame stacking để tăng hiệu suất học tập
* Theo dõi quá trình học thông qua Tensorboard
* Tính năng ghi lại gameplay dưới dạng GIF
* Xây dựng trên nền tảng Gymnasium và PyTorch

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Xây dựng bằng

* [![Python][Python.org]][Python-url]
* [![PyTorch][PyTorch.org]][PyTorch-url]
* [![Gymnasium][Gymnasium.org]][Gymnasium-url]
* [![TensorBoard][TensorBoard.org]][TensorBoard-url]
* [![OpenCV][OpenCV.org]][OpenCV-url]

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- GETTING STARTED -->

## Bắt đầu

Để thiết lập một bản sao của dự án này trên máy tính cục bộ của bạn, hãy làm theo các bước đơn giản sau.

### Yêu cầu

* Python 3.7+
* CUDA (tùy chọn, nhưng được khuyến nghị cho huấn luyện nhanh hơn)

### Cài đặt

1. Clone repository
   ```sh
   git clone https://github.com/username/pacman-double-dqn.git
   cd pacman-double-dqn
   ```
2. Tạo môi trường ảo (tùy chọn nhưng được khuyến nghị)
   ```sh
   python -m venv venv
   # Trên Windows
   venv\Scripts\activate
   # Trên Linux/Mac
   source venv/bin/activate
   ```
3. Cài đặt các gói cần thiết
   ```sh
   pip install -r requirements.txt
   ```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- USAGE EXAMPLES -->

## Cách sử dụng

### Cấu trúc dự án

```
pacman-double-dqn/
├── agent.py           # Các lớp agent Double DQN
├── configs.py         # Cấu hình và hyperparameters
├── env.py             # Wrapper cho môi trường Pacman
├── list_envs.py       # Liệt kê các môi trường có sẵn
├── main.py            # Điểm vào chính của chương trình
├── model.py           # Định nghĩa mạng neural
├── replay_buffer.py   # Bộ nhớ đệm replay
├── train.py           # Mã huấn luyện
├── test.py            # Mã kiểm thử
├── utils.py           # Các tiện ích
├── requirements.txt   # Danh sách các gói phụ thuộc
├── checkpoints/       # Thư mục để lưu các model được huấn luyện
├── logs/              # Logs cho Tensorboard
└── videos/            # Ghi lại gameplay
```

### Huấn luyện model

Để huấn luyện model với các cài đặt mặc định:

```sh
python main.py --mode train
```

Tùy chỉnh các hyperparameters:

```sh
python main.py --mode train --args --env ale_py:ALE/MsPacman-v5 --lr 0.0001 --gamma 0.99 --stack-frames 4 --train-steps 500000
```

Các tham số chính:

- `--env`: Tên môi trường Pacman (mặc định: "ale_py:ALE/MsPacman-v5")
- `--lr`: Learning rate (mặc định: 2e-4)
- `--gamma`: Hệ số discount (mặc định: 0.99)
- `--eps-start`: Epsilon khởi đầu (mặc định: 1.0)
- `--eps-final`: Epsilon cuối cùng (mặc định: 0.1)
- `--eps-decay`: Tốc độ giảm epsilon (mặc định: 45000)
- `--train-steps`: Tổng số bước huấn luyện (mặc định: 500000)
- `--batch-size`: Kích thước batch (mặc định: 32)
- `--buffer-size`: Kích thước replay buffer (mặc định: 50000)
- `--target-update`: Số bước giữa các lần cập nhật target network (mặc định: 450)
- `--device`: Thiết bị để huấn luyện ("cuda" hoặc "cpu")

### Kiểm thử model

Chạy một model đã huấn luyện:

```sh
python main.py --mode test --args --model-path checkpoints/timestamp/model_best.pt --episodes 10 --render
```

Tham số:

- `--model-path`: Đường dẫn đến model đã lưu (bắt buộc)
- `--episodes`: Số episode để chạy (mặc định: 10)
- `--render`: Hiển thị gameplay (flag)
- `--record`: Ghi lại gameplay dưới dạng GIF (flag)

### Theo dõi quá trình huấn luyện

Sử dụng TensorBoard để theo dõi quá trình huấn luyện:

```sh
tensorboard --logdir logs
```

Sau đó, mở trình duyệt tại `http://localhost:6006`

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- ROADMAP -->

## Lộ trình

- [x] Xây dựng Double DQN Agent cơ bản
- [x] Tích hợp visualizations và tracking quá trình học
- [x] Thêm chức năng ghi lại gameplay
- [ ] Thử nghiệm với các biến thể khác của môi trường Pacman
- [ ] Tối ưu hóa hyperparameters
- [ ] Tích hợp và so sánh với các thuật toán khác
    - [ ] Dueling DQN
    - [ ] Prioritized Experience Replay

[//]: # (Xem [open issues]&#40;https://github.com/username/pacman-double-dqn/issues&#41; để biết danh sách đầy đủ các tính năng đề xuất &#40;và các vấn đề đã biết&#41;.)

<p align="right">(<a href="#readme-top">back to top</a>)</p>






