# Jenkins là gì?
- Jenkins là nguồn mở được sử dụng thực hiện chức năng liên tục và xây dựng tự động hoá tác vụ
- Nó tích hợp mã nguồn mở của các thành viên trong đội nhanh chóng liên tục, theo dõi thực thi và trạng thái thông qua bước kiểm thử ( kiểm thử tích hợp,kiểm thử đơn vị). Tất cả đều nhằm giúp sản phẩm chạy ổn đinh.
![Minh hoạ](https://topdev.vn/blog/wp-content/uploads/2019/05/CICD.png "ảnh minh hoạ")
![CICD](CICD.png"ảnh mình hoạ CICD")
- CI là viết tắt của Continuous Intergration
  - là tích hợp liên tục, nhằm liên tục tích hợp các source code của các thành viên trong team lại một cách nhanh chóng.
- Chu trình làm việc
  1. Bước đầu tiên, các thành viên trong dev sẽ bắt đầu pull code mới nhất từ repo về branch để thực hiện các yêu cầu chức năng nhất định
  2. Tiếp đó là quá trình lập trình và test code để đảm bảo chất lượng của chức năng cũng như toàn bộ source code.
  3. Thành viên code xong thì sẵn sàng cho việc commit vào branch develop của team.
  4. Thành viên cập nhật code mới từ repo về local repo
  5. Merge code và giải quyết conflict
  6. Build và đảm bảo code pass qua tests dưới local.
  7. Commit code lên repo
  8. Máy chủ CI lắng nghe các thay đổi code từ repository và có thể tự động build/test, sau đó đưa ra thông báo(pass/failure) cho các thành viên.

- CD là viết tắt của Continuous Delivery
  -Continuous Delivery là chuyển giao liên tục, là 1 tập hợp các kĩ thuật để triển khai tích hợp source code trên môi trường staging(một môi trường rất giống với môi trường production )