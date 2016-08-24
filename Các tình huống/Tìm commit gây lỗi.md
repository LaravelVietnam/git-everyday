### Tình huống
Bạn commit một số tính năng lên. Sản phẩm chạy một thời gian, bỗng phía người dùng báo có lỗi phát sinh. Lúc này, việc cần làm là tìm commit nào gây ra lỗi để khoanh vùng và sửa lỗi.

## git bisect
Git cung cấp một công cụ khá tốt để khoanh vùng lỗi là `git bisect`. Trước khi biết `git bisect`, tôi khoanh vùng bằng cách phỏng đoán lỗi phát sinh từ commit nào, checkout commit đó. Sau đó test xem có lỗi hay không. Nếu không thì checkout một commit mới hơn, rồi test lại. Nếu có nhiều commit quá sẽ checkout ngắt quãng, nếu có lỗi thì checkout commit cũ hơn. Mục đích cuối cùng là xác định 2 commit có lỗi và không lỗi nằm kế nhau. Từ đó xem code bị thay đổi những gì để debug.

`git bisect` theo tôi thấy cũng làm tương tự, nhưng nó tự động việc checkout. Ta chỉ cần chỉ ra commit có lỗi gần nhất mà mình có thể biết, và commit không có lỗi. Sau đó `git bisect` sẽ lần lượt checkout các commit và cuối cùng sẽ chỉ ra commit đầu tiên phát sinh lỗi.

## Các bước thực hiện
Bắt đầu bằng lệnh

```
git bisect start
git bisect bad # xác định version hiện tại có bug
git bisect good v2.6.13-rc2 # xác định version v2.6.13-rc2 chưa phát sinh lỗi
```

Sau đó, git sẽ tự chọn một commit và checkout. Việc của bạn là mở ứng dụng ra để test lỗi. Nếu có lỗi, dùng lệnh sau:

```
git bisect bad
```

Nếu không có lỗi:

```
git bisect good
```

Git sẽ báo là còn bao nhiêu commit có thể phải check nữa. Cứ tiến hành dần đến khi git khoang vùng được commit cuối cùng, và thông báo với hash của commit đó.
Lúc này cần thao tác thêm:

```
git bisect reset
```

để phục hồi project về trạng thái trước khi tiến hành kiểm lỗi.

### Sửa lỗi, cần làm gì
Để an toàn cho code, nên tạo một branch mới trước khi bắt đầu sửa lỗi.

```
git branch fix-f-cking-bug
git checkout fix-f-cking-bug
```

Sau đó có thể quay lại commit đã tìm được ở trên để so sánh code, test các kiểu.

Khi đã fix được lỗi, quay về branch trước đó để merge. Xem thêm https://github.com/LaravelVietnam/git-everyday/blob/draft-0.1/Basic/Merge%20branch%20an%20to%C3%A0n.md
