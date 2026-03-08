# Steam Recommend System and Massive DataMining

## 1. Chuẩn bị & clone mã nguồn từ Github

```bash
git clone https://github.com/vukhai248/Steam-Recommend-System-and-Massive-DataMining.git
cd Steam-Recommend-System-and-Massive-DataMining
```

## 2. Cài đặt môi trường và cá thư viện cần thiết thông qua conda

```bash
conda env create -f environment.yml
```

## 3. Kích hoạt môi trường

```bash
conda activate SteamRS
```


## 4. Giới thiệu về dataset

Bộ dữ liệu Steam Games Metadata and Player Reviews (2020–2024) cung cấp một tập hợp toàn diện và có cấu trúc về siêu dữ liệu trò chơi điện tử và đánh giá của người dùng từ nền tảng Steam, do Valve Corporation vận hành.

Dữ liệu bao phủ giai đoạn từ tháng 01/2020 đến tháng 12/2024, gồm 23000+ trò chơi được phát hành vào năm 2020 trở đi và hơn 31 triệu lượt đánh giá người dùng. Bộ dataset được xây dựng nhằm phục vụ nghiên cứu về mối quan hệ giữa các thuộc tính của trò chơi.

Cấu trúc thư mục dataset gồm:
```bash
Steam Games Metadata and Player Reviews (2020–2024)
├── Game Reviews
│   ├── Gồm nhiều file .csv chứa các thông tin về đánh giá của người dùng với game theo mã ID
├── Game Metadata
│   ├── Gồm file JSON chứa thông tin metadata của game
```

Link tải dataset: [Steam Games Metadata and Player Reviews (2020–2024)](https://data.mendeley.com/datasets/jxy85cr3th/2)


#### 4.1. Game Reviews

File CSV chứa các thông tin về review của người dùng với game theo mã ID, được thiết kế theo cấu trúc {gameId}_{reviewCount}, gồm các trường thông tin:
- `user`: Username
- `playtime`: Giờ chơi tại thởi điểm review
- `post_date`: Ngày đăng review
- `helpfulness`: Số vote "hữu ích" từ cộng đồng cho review
- `review`: Nội dung review
- `recommend`: Đánh giá tích cực hay tiêu cực
- `early_access_review`: Có phải review Early Access hay không

#### 4.2. Game Metadata

File JSON chứa thông tin metadata của game, gồm các thông tin cơ bản của game:

- Thông tin cơ bản:
  - `gameID`: ID của game
  - `name`: Tên của game 
  - `release_date`: Ngày phát hành
  - `required_age`: Giới hạn độ tuổi
  - `price`: Giá bán game (USD)
  - `discount`: % Giảm giá hiện tại

- Mô tả nội dung:
  - `detailed_description`: Mô tả chi tiết đầy đủ
  - `about_the_game`: Mô tả gameplay
  - `short_description`: Mô tả ngắn

- Phân loại:
  - `supported_languages`: Ngôn ngữ hỗ trợ của game
  - `full_audio_languages`: Ngôn ngữ có voice của game
  - `categories`: Tính năng game (Single player,...)
  - `genres`: Thể loại của game
  - `tags`: Community tags & vote count

- Đánh giá:
  - `positive`: Số review tích cực
  - `negative`: Số review tiêu cực
  - `estimated_owners`: Ước lượng số người sở hữu
  - `peak_ccu`: Số người chơi lớn nhất vào thời kỳ đỉnh 

- Thông tin giờ chơi:
  - `average_playtime_forever`: Trung bình giờ chơi (phút) tổng
  - `average_playtime_2weeks`: Trung bình giờ chơi 2 tuần gần nhất
  - `median_playtime_forever`: Median giờ chơi tổng
  - `median_playtime_2weeks`: Median giờ chơi 2 tuần