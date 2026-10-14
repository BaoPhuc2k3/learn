1. So sánh git revert và git reset
git reset: Xoá vĩnh viễn hoặc thay đổi lịch sử commit
git revert: Tạo commit mới đảo ngược nội dung commit cũ

| Tình huống                                | Dùng gì?                  | Giải thích                       |
| ----------------------------------------- | ------------------------- | -------------------------------- |
| Lỡ commit sai, chưa push                  | `git reset`               | Dễ dàng sửa lại, vì chưa ai thấy |
| Lỡ commit sai, đã push                    | `git revert`              | Không phá remote history         |
| Dọn dẹp commit lịch sử                    | `git rebase -i` + `reset` | Rewriting history                |
| Undo một tính năng vừa merge              | `git revert -m`           | Revert merge commit              |
| Xoá hết thay đổi local về trạng thái repo | `git reset --hard`        | Cẩn thận mất code                |

2. So sánh git merger và git rebase
merge kết hợp 2 nhánh lại với nhau bằng cách tạo một commit mới, giữ lịch sử phân nhánh rõ ràng.
    A---B---C (main)
        \
        D---E (feature)

    Sau merge:

    A---B---C-------M (main)
        \         /
        D---E---/

rebase chuyển toàn bộ commit của 1 nhánh lên "đầu" của nhánh khác, bằng cách tái tạo commit mới → làm lịch sử thẳng, sạch.
    A---B---C (main)
        \
        D---E (feature)

    Sau rebase:

    A---B---C---D'---E' (feature)

| Tình huống                 | Dùng gì? | Lý do                                |
| -------------------------- | -------- | ------------------------------------ |
| Làm việc nhóm              | `merge`  | Giữ lịch sử rõ ràng, dễ trace        |
| Làm việc cá nhân           | `rebase` | Lịch sử sạch sẽ, gọn gàng            |
| Trước khi merge vào `main` | `rebase` | Giảm số lượng commit rác             |
| Đã push lên remote         | `merge`  | An toàn, không phá commit người khác |
| Chưa push                  | `rebase` | Tự do viết lại lịch sử               |

3. So sánh git fetch và git pull
git fetch Lấy dữ liệu mới từ remote về local, chưa hợp nhất
git pull Lấy dữ liệu mới từ remote và hợp nhất ngay vào branch hiện tại