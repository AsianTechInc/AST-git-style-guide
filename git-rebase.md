Sử dụng git rebase
===

`git rebase` có 2 ứng dụng chính để giúp git history đẹp và sạch sẽ hơn. Đầu tiên phải nhắc đến ứng dụng gộp nhiều commit lại thành 1, tiếp đến là  ứng dụng chỉnh lại thứ tự các commit bằng việc điều chỉnh gốc của nhánh.

# Gộp chung nhiều commit
Giả sử master của chúng ta hiện tại có những commit m1, m2, m3, m4. Giờ chúng ta muốn ghép chung tất cả commit này thành 1 commit duy nhất m1234. Ta sẽ làm như sau : 
```console
git checkout master
git rebase -i HEAD~4
```
tham số `HEAD~4` ở đây có nghĩa là ta muốn thao tác trên 4 commit gần nhất. Sau khi chạy lệnh này, màn hình sẽ như sau : 
```
pick 1b01880 m1
pick 021f277 m2
pick 8240aff m3
pick c1ff200 m4
# Rebase 94a7a25..c1ff200 onto 94a7a25 (       4 TODO item(s))
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```
`p` : giữ nguyên commit
`r` : giữ nguyên commit đó nhưng sẽ thay đổi nội dung commit message
`e` : giữ nguyên commit nhưng dừng amending
`s` : sử dụng commit, nhưng sẽ ghép chung vào với commit trước đó
`f` : giống `s`, nhưng sẽ bỏ qua cả commit message
`x` : thực thi 1 dòng command

Thông thường ta sẽ sửa thành : 
```
pick 1b01880 m1
s 021f277 m2
s 8240aff m3
s c1ff200 m4
```
sau khi save lại `:wq`, git sẽ xử lý và chuyển ra màn hình để edit lại message:
```
# This is a combination of 2 commits.
# The first commit's message is:

m4

# This is the 2nd commit message:

m5
...
```
Theo quy ước về cách làm việc với gitflow, thường mình sẽ xoá hết những message cũ và viết lại message theo dạng đơn giản hơn. Ví dụ như 
```
Remove config/database.yml from git index and add it to gitignore.
```

# Chỉnh lại thứ tự commit
Giả sử branch của chúng ta hiện tại có những commit m1, m2, m3, m4. Cùng thời gian đấy, có 1 bạn khác cũng có những commit M1, M2, M3, M4 và đã merge vào master.
Khi ta merge nhánh của mình vào master, các commit sẽ được sắp xếp theo thứ tự thời gian. Ví dụ như : M1 M2 m1 m2 M3 m3 m4 M4. 
Thứ tự này rất khó theo dõi khi ta muốn biết được cả quá trình làm việc của từng branch. 
Rõ ràng là thứ tự M1 M2 M3 M4 m1 m2 m3 m4 sẽ đơn giản và dễ theo dõi hơn. 

Những lúc này ta dùng `rebase`.

```
git checkout master
git pull
git checkout branchA
git rebase master
```

Nếu không có conflict thì commit M1 M2 M3 M4 sẽ được thêm vào branchA theo đúng thứ tự của nó trên master. 
Nếu có conflict thì bạn chỉ cần fix lại conflict, add lại và `git rebase --continue` (khi xảy ra vấn đề, git sẽ hướng dẫn cụ thể cho chúng ta luôn ).

[Link tham khảo: merge vs rebase](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)

Với gitflow hay github flow, trước khi gửi pull request, bạn bắt buộc phải rebase lại master để lấy code mới nhất và đảm bảo không xảy ra conflict. 
Ngoài ra sau khi sửa lại code theo comment, fix bugs, ... bạn cũng nên gộp hết tất cả những commit đó thành 1 để dễ theo dõi về sau. 
