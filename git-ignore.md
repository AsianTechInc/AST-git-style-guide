# Sử dụng gitignore.io

[gitignore.io](https://www.gitignore.io/)

Dùng các từ khoá sau để tạo file : 
1. Chọn framework ( rails, revel, ... )
2. Chọn HĐH ( OSX, ubuntu, ... )
3. Chọn editor hay dùng ( Sublime, OSX, ... )
 
Và cuối cùng là generate :100: 

# Các bước xử lý để remove 1 file ra khỏi git

## Nếu là 1 file có tồn tại : 
```
$ git rm --cached <tên_file>
$ echo '<tên_file>' >> .gitignore # nếu cần 
```
## Nếu là 1 file không tồn tại nhưng vẫn có trong git history 
```
# chỉ xoá trong history (vẫn tồn tại trong working tree)
$ git filter-branch -f --index-filter 'git rm --cached -rf --ignore-unmatch <tên_file>' HEAD

# xoá cả trong history lẫn working tree
$ git filter-branch -f --index-filter 'git rm -rf --ignore-unmatch <tên_file>' HEAD
```
