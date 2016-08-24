Khi đã fix lỗi xong, hoặc hoàn thành một tính năng mới trên branch tính năng, ta quay về branch gốc trước đó để merge. Tuy nhiên, để an toàn hơn, nên tạo thêm branch mới từ branch gốc, ta tiến hành merge trên branch test này để đảm bảo có conflict cũng không ảnh hưởng những việc đang làm trên branch gốc.

```
git checkout main-branch
git branch main-branch-test
git checkout main-branch-test
git merge fix-f-cking-bug
```
Khi có conflict xảy ra, giả sử lúc đó không có thời gian để sửa, ta có thể bỏ hết code bị thay đổi, checkout lại branch gốc để làm việc ưu tiên cao hơn trước. Sau đó có thời gian thì sửa confict rồi commit sau.
// TODO: cần viết chi tiết hơn
