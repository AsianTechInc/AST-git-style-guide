Mô hình Git cho các dự án release 
===
# Vấn đề 
Gitflow là mô hình rất nổi tiếng và được sử dụng rất rộng rãi. Tuy nhiên, điều đó không có nghĩa là gitflow là mô hình hoàn hảo. 

Mô hình gitflow ứng dụng 1 cách rất khó khăn vào các dự án có release và yêu cầu phải test trên nhiều môi trường khác nhau. 

Ví dụ, 
- bạn có 3 môi trường phải test là develop, staging, và production.
- bạn có 5 task là A, B, C, D, E
Giả sử team của bạn đã dev xong 5 tasks này và merge vào develop để test. Tuy nhiên, task A, D bị failed khi test, và bạn chỉ được đưa task B, C, E lên staging. 
Trên staging khách hàng test tiếp và chỉ có task C được chấp nhận đưa lên production. 

Với trường hợp như thế này, sử dụng gitflow cực kì khó khăn : 
- các task đã merge vào develop nhưng bị failed test thì sẽ phải remove ra khỏi develop rồi mới merge vào staging được. Việc này rất mạo hiểm và yêu cầu kĩ năng dùng git rất tốt. Ngoài ra làm thế này cũng rất tốn thời gian.
- Trường hợp kinh khủng nhất là code của develop, staging và production có sự khác biệt bởi các lý do khách quan. Vì thế việc merge từ staging vào production sẽ gặp khó khăn khi xử lý. 

Trong trường hợp này có 1 mô hình git đơn giản mà giải quyết khá tốt các vấn đề kể trên. Mô hình này được gọi là env branch.

# Các branch cơ bản 
1. production : live site
2. staging : môi trường test của khách hàng
3. develop : môi trường test của team 

Mỗi một môi trường sẽ có 1 branch tương ứng. 1 dự án thường sẽ có 3 môi trường cơ bản như trên. 3 branch này sẽ được gọi chung là env branch. 

1 feature sau khi được hoàn thành sẽ merge vào các môi trường tương ứng, deploy lên server và test. 

Như vậy, về cơ bản sẽ có 2 loại branch là features và branch để deploy lên các môi trường khác nhau. 

# Quy ước 
1. Không bao giờ được commit trực tiếp vào các env branch. 
2. Không bao giờ được merge các env branch với nhau.
3. Các features branch đều có thể deploy độc lập với nhau. 

# Ví dụ

## tạo feature branch
```
# lấy code mới nhất từ origin/master
git pull --rebase origin master
 
# tạo branch
git checkout -b 123-wine-validations
```

## Dev và commit
```
# dev và commit thay đổi vào feature branch
git add -A
git commit -m "refs #123 - adding validations to wine model"
```

## Deploy vào develop để test và review
```
# rebase lại origin/master và xử lý conflict nếu có 
git pull --rebase origin master
 
# đổi sang develop branch
git checkout dev
 
# rebase lại origin/dev
# (vì có thể chứa merge từ các team khác)
git pull --rebase origin dev
 
# merge với feature branch 
git merge 123-wine-validations
 
# push vào origin/dev và deploy lên dev
git push origin dev
```

## Deploy vào staging để test
```
# checkout sang feature branch và rebase lại origin/master
git checkout 123-wine-validations
git pull --rebase origin master
 
# push thay đổi vào staging branch 
git checkout stage
git pull --rebase origin stage
git merge 123-wine-validations
git push origin stage
```

## Deploy vào production để test
```
# checkout sang feature branch và rebase lại origin/master
git checkout 123-wine-validations
git pull --rebase origin master
 
# push feature branch lên origin
git push origin 123-wine-validations
 
# gửi pull request hoặc merge bằng tay
```

