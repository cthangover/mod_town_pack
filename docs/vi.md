# Town Pack — nền thị trấn, ngôi nhà và quán bar cùng âm thanh quán bar

Town Pack là bối cảnh dựng sẵn cho câu chuyện diễn ra ở một thị trấn nhỏ. Gói gồm ba tấm nền vẽ tay — góc phố ở lối vào thị trấn, tiền sảnh ngôi nhà và quán bar về đêm — cùng vòng lặp âm thanh không khí quán bar. Không có cốt truyện, cảnh quay hay nhân vật nào bên trong: hình nào xuất hiện ở đâu do game quyết định.

Hai game có sẵn đã dùng chung gói này. **Cthangover** lấy lối vào thị trấn và tiền sảnh; mẫu **My Novel** dùng cả ba tấm nền và âm thanh quán bar. Vì cả hai game lấy đúng những tệp này từ mod, một bản sửa hay một hình đẹp hơn trong Town Pack sẽ đến với cả hai.

## Bên trong có gì

Lối vào thị trấn, `town/town_entry`: góc phố lát đá với những mái hiên sọc của các cửa hàng.

![Nền lối vào thị trấn: tòa nhà góc phố với mái hiên xanh và trắng trên con đường lát đá.](assets/town_entry.jpg)

Tiền sảnh ngôi nhà, `home/vestibule`: sảnh có cầu thang, ghế bành và một bức tranh.

![Nền tiền sảnh: cầu thang gỗ, ghế bành, ghế dài và bức tranh đóng khung trong sảnh ánh sáng ấm.](assets/vestibule.jpg)

Quán bar, `bar/bar`: những bàn có đèn lồng, quầy bar và kệ đầy chai rượu.

![Nền quán bar: bàn dưới ánh đèn lồng, quầy bar và kệ chai rượu dưới trần nhà có dầm gỗ.](assets/bar.jpg)

Âm thanh quán bar, `bar/bar_ambient`: vòng lặp Ogg Vorbis với không khí quán bar cho kênh âm thanh Ambience.

Cả ba tấm ảnh đều cỡ 1920 × 1024. Mỗi tấm có một tệp đi kèm màu xám cùng tên với hậu tố `_depth`:

![Tệp độ sâu của lối vào thị trấn: phiên bản xám của cùng bố cục.](assets/town_entry_depth.jpg)

Bạn không bao giờ thấy tấm ảnh độ sâu trực tiếp. Khi hiển thị nền, game cũng tải `<name>_depth` và chuyển cho hệ thống ánh sáng, hệ thống này dùng nó cho những nguồn sáng đặt lên cảnh. Nền không có ảnh độ sâu vẫn hiển thị bình thường.

## Bạn sẽ thấy nó ở đâu

- **Cthangover:** cảnh `town_entry` (lối vào thị trấn) và cảnh `home_vestibule`.
- **Mẫu My Novel:** `my_novel_town`, `my_novel_home` và `my_novel_bar`. Cảnh quán bar cũng phát `bar/bar_ambient`.

Cùng lối vào thị trấn đó trong mẫu My Novel, nơi nó mở màn game bằng một dòng dẫn truyện:

![Cảnh đầu của My Novel: nền lối vào thị trấn phía sau dòng "Thị trấn lúc chiều tối. Đèn đường đã sáng và một làn gió mát lùa dọc những viên đá lát".](assets/reuse-my-novel.jpg)

Còn trong Cthangover, một câu chuyện khác lại đưa ra các lựa chọn riêng trên cùng bức tranh:

![Lối vào thị trấn trong Cthangover: cùng nền với các lựa chọn "Về nhà" và "Xem xét con hẻm".](assets/reuse-cthangover.jpg)

Town Pack nằm trong bộ sưu tập của cả hai game nên được nạp cùng chúng. Cài nó không tự thêm những địa điểm này vào một game khác: game phải tự dùng các nền trong cảnh của mình.

## Dùng các nền trong game của bạn

1. Thêm `town_pack>=1` vào danh sách `depends` của mod nội dung.
2. Thêm `town_pack>=1` vào bộ sưu tập của game, như mẫu My Novel làm trong khối **Assets**.
3. Tham chiếu tài nguyên theo tên dưới đây. Tên tính từ `backgrounds/` và `sounds/` và không có phần mở rộng.

```jsonc
// mods/my_game/manifest.json — thêm vào danh sách có sẵn
"depends": ["town_pack>=1"]
```

Một cảnh hiện quán bar và phát âm thanh nền, lấy từ cảnh `my_novel_bar` của mẫu:

```json
{
  "name": "my_bar",
  "defaultBackground": "bar/bar",
  "defaultAmbient": "bar/bar_ambient"
}
```

Kịch bản cũng có thể đổi hình giữa chừng hội thoại:

```scenario
background town/town_entry
text "Giờ này phố vắng tanh."
```

Các tên có sẵn là:

```text
town/town_entry     backgrounds/town/town_entry.png
home/vestibule      backgrounds/home/vestibule.png
bar/bar             backgrounds/bar/bar.png
bar/bar_ambient     sounds/bar/bar_ambient.ogg
```

## Thay một bức tranh cho game của bạn

Để đổi hình mà không đụng đến Town Pack, hãy đặt vào mod của bạn một tệp trùng tên tương đối, ví dụ `backgrounds/bar/bar.png`, và khai báo `town_pack>=1` trong `depends` của mod đó. Mod phụ thuộc vào chủ sở hữu được nạp sau và thắng. Khi thay nền, hãy kèm luôn tệp `_depth` cùng tên: nếu không, game vẫn tìm thấy ảnh độ sâu gốc của Town Pack và ánh sáng sẽ bám theo bố cục của bức cũ.

Không có khai báo phụ thuộc, hai mod cùng cung cấp một tên sẽ không có thứ tự xác định; công cụ bản đồ tài nguyên báo đây là lỗi.

## Nếu có thứ còn thiếu

1. Nền đen hoặc không hiện thường là do gõ sai tên. Tên phân biệt chữ hoa chữ thường và dùng `/`.
2. Kiểm tra Town Pack đã được đưa vào game bạn vừa chạy, chứ không chỉ được cài.
3. Không có tiếng quán bar: xem `defaultAmbient` của cảnh đã là `bar/bar_ambient` chưa và kênh **Ambience** đã bật trong **Settings → Sound** chưa. Việc phát âm thanh do mod Audio Engine đảm nhận.
