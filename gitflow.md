# Gitflow
Là 1 mô hình cách quản lý và sử dụng Git hiện đại, được tạo ra bởi Vincent Driessen. Nó đã chứng minh được sự hiệu quả và uyển chuyển của mình trong rất nhiều các dự án opensource và được công nhận rộng rãi trong cộng đồng LTV.
 
Dưới đây là mô hình tổng quát về git-flow.
![image](https://cloud.githubusercontent.com/assets/1412648/8957459/d0bf758c-3628-11e5-9ecf-e17438111ccc.png)

# Ý nghĩa của các branch trong Git-flow
* nhánh master: nhánh chứa code chuẩn của toàn dự án và là nhánh duy nhất được deploy lên trên production. Khi nào cần deploy hoặc release mới update code vào master.
* Hotfix: là những nhánh để sửa lỗi khẩn cấp.
* Release : là những nhánh để trợ giúp quá trình release.
* Develop: nhánh quan trọng thứ 2 trong project. Nhánh này chứa tất cả các code đang được phát triển.
* Feature: là những nhánh dùng để phát triển. Mỗi một branch dạng này sẽ dùng để làm 1 chức năng, hay 1 task.
 
**_Master, Hotfix, Release do leader hoặc manager thao tác. Member không tự ý tạo mới hay thay đổi những nhánh này nếu chưa có sự cho phép của leader._**
 
Trong quá trình làm việc, team sẽ chủ yếu thao tác trên nhánh develop và những nhánh feature. Do đó mô hình làm việc cũng sẽ đơn giản hơn nhiều.

# Mô hình làm việc với develop và features
Như đã nói ở trên, master, hotfix, release sẽ do leader thao tác. Trong quá trình làm việc ta chỉ quan tâm tới develop và features. Mô hình git lúc đó sẽ như sau:
 
![image](https://cloud.githubusercontent.com/assets/1412648/8957576/899d9a52-3629-11e5-8b25-92b0ffe9e7db.png)

* Develop : develop sẽ được tách ra từ master, và là nhánh chứa toàn bộ code đang trong quá trình phát triển.
 
* Feature branches : là những branch được tách ra từ develop mới nhất. Mỗi 1 branch sẽ xử lý duy nhất 1 task hoặc 1 bug. Thường sẽ do 1 người đảm nhiệm.
 
Mô hình này tương ứng với Github-flow, tuy nhiên để có thể sử dụng cho tất cả các project của công ty, ta sẽ sử dụng gitflow.
 
[Hướng dẫn trực quan và đơn giản về Github flow](https://guides.github.com/introduction/flow/)
 Link này giải thích các sử dụng Github-flow, mọi người có thể tham khảo. Khác biệt duy nhất là thay branch master trong đó thành develop.

# Các quy ước
* 1 branch feature chỉ để làm 1 task hoặc 1 bug duy nhất. Không nên để nhiều người cùng làm 1 branch.
 
* push lên branch cùng tên trên Github.
 
* Thường xuyên push lên, ít nhất 1 ngày 1 lần để leader nắm tiến độ.
 
* Việc merge các branch với nhau sẽ được làm trên github thông qua các pull requests. Không merge trên local.
 
* Gửi pull request khi cần feedback hay giúp đỡ, hoặc khi đã hoàn thiện và sẵn sàng merge.

* merge vào master sẽ chỉ do leader tiến hành. Không merge trên local rồi tự ý push vào master. merge các branch khác thì không cần leader.
 
* Sau khi hoàn thành xong các branch (sau khi đã review, fix, …) sẽ rebase lại các commit rồi push chèn lên remote.
 
* Nếu xảy ra conflict, người tạo branch phải merge hoặc rebase lại develop để xử lý.
[git rebase](https://github.com/AsianTechInc/AST-ruby-code-review/issues/5)
