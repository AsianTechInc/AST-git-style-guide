#Git cheat sheet

## Các định nghĩa
### repo
Nơi lưu giữ code và các file quản lý code. Thường là ở thư mục chứa tất cả các phần liên quan tới 1 dự án.

Ở đây sẽ có thêm 2 khái niệm là local repo và remote repo. 

### local repo
Các repo ở trên máy cá nhân. Git là kiểu quản lý phân tán, do đó mỗi 1 member tham gia dự án đều có 1 repo để làm việc. 

### remote repo
repo này thường được đặt trên các server bên ngoài như github, bitbucket, ... 
repo này nơi chứa tổng hợp tất cả các code từ các local repo của member. Đây cũng được coi là repo gốc quan trọng nhất. 

### working tree
Nơi user chỉnh sửa, thay đổi những file của project. 

### index
Sau khi thay đổi từ working tree, trước khi commit vào repo thì những thay đổi đó sẽ được index lại để quản lý. 

### commit
Sau khi thay đổi các file, index những file này thì ta cần commit để định nghĩa và lưu lại những thay đổi đó. 

### branch
Khi hình dung git là 1 cái cây thì branch là những cành cây. Tiếng việt thường còn gọi là "nhánh"
Branch là nơi lưu giữ, quản lý, phân tách lịch sử của 1 project. 
Nếu mỗi commit là 1 lá cây, thì branch là cành cây. 1 cành cây có thể có 1 hoặc nhiều lá cây trên đó. Ngoài ra các cành cây này đều được tách ra từ thân cây - nhánh chính hay còn gọi là master branch. 

Trong git có 3 loại branch : **local branch**, **remote branch**, **remote tracking branch**. 

#### local branch
các branch được quản lý trên local repo

#### remote branch
các branch được quản lý trên remote repo

#### remote tracking branch
là các branch dùng để truy vết local branch với remote branch. 
Ví dụ,  với branch **origin/master** thì phần origin là tên remote repo, master là tên branch đang được tracking. 

### checkout
Là 1 câu lệnh của git - cũng là 1 khái niệm quan trong. Tác dụng của lệnh này là để chuyển branch,  quay về 1 commit hay 1 tags cho trước, chuyển về branch trên remote repo, ... 

### tags
Được sử dụng để đánh dấu history.

### revision
Tương ứng với mỗi commit, git sẽ sinh ra 1 mã hash. Mã này được gọi là revision để phân biệt các commit và dễ thao tác hơn. 

### HEAD
1 khái niệm để gọi tên commit mới nhất trên local branch hiện tại.

### FETCH_HEAD
khái niệm gọi tên commit mới nhất trên remote tracking branch. 

### ORIG_HEAD
commit phía trước HEAD, hay là commit mới thứ 2 trên branch hiện tại. Cách viết khác là HEAD@{1}

### MERGE_HEAD
Chỉ tới commit mới nhất được sinh ra khi merge code. 
Ví dụ : 
```
git checkout master
git merge <branch-name>
```
Như thế MERGE_HEAD là commit mới nhất.
Sau đó sửa và thêm 1 số commit vào thì MERGE_HEAD vẫn không thay đổi. 

## Workflow
1. Tạo repo
2. Tạo và chỉnh sửa file (working tree)
3. Đăng kí index
4. Commit vào repo

## Setting
### Tạo repo
```
# tạo repo
git init

ls a
.    ..   .git

# các file và folder được tạo ra để quản lý git
cd .git
ls
HEAD        description info        refs
config      hooks       objects
```

### username, email sử dụng trong git
```
# global setting
git config --global user.name "username"
git config --global user.email "email"

# ứng với từng repo
git config user.name "username"
git config user.email "email"
```

