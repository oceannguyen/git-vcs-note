## Git là gì?

Git cho phép các thành viên trong nhóm làm việc cùng nhau trên cùng một tài liệu (thông thường là code) cùng lúc. Là hệ thống quản lý phiên bản phân tán (**Distributed Version Control System**)

#### 1.1. Khởi tạo kho chứa

Tạo thư mục tài liệu **beginning-git** làm kho chứa để quản lý Git, sử dụng câu lệnh sau để khởi tạo:
```
git init
```

Git sẽ tạo một kho chứa (repository) rỗng trong **/.git/**. Kho chứa này là một thư mục ẩn để Git hoạt động

#### 1.2. Kiểm tra trạng thái

Để xem trạng thái hiện tại của project:
```
git status
```

Tạo một file bất kỳ (*readme.md*) trong **beginning-git**, lúc này khi chạy lại lệnh **git status** thì Git sẽ thông báo rằng file *readme.md* trong thái chưa được tổ chức (**unstaged**), có nghĩa chưa được quản lý bởi Git

#### 1.3. Tổ chức files

Để yêu cầu Git bắt đầu theo dõi file *readme.md*, cần phải thêm file vào vùng được tổ chức (**staged**) với lệnh sau:
```
git add readme.md
```

Chạy lệnh ```git status``` để xem trạng thái hiện tại của file

#### 1.4. Committing

> Chú ý rằng những files được tổ chức (**staged**) vẫn chưa được lưu vào kho chứa cho đến khi chúng được **commited**

> Có thể thêm/xóa files từ được tổ chức trước khi lưu vào repository

Để lưu các thay đổi trong staged, sử dụng lệnh:
```
git commit -m "Add readme.md file"
```
#### 1.5. Xem lịch sử

Để theo dõi lại lịch sử commit, Git cung cấp câu lệnh như:
```
git log
```
#### 1.6. Remote Repositories

Những thay đổi ta thực hiện cho đến giờ đang diễn tại local, để cả team có thể cùng nhau làm việc với kho chứa (**beginning-git**) đó ta cần đưa nó  lên server. Sau đó ta sẽ liên kết kho chứa local và kho chứa server lại với nhau. 

Các bước bạn cần làm như sau:

- Truy cập [Github](https://github.com) (là một server cho phép lưu trữ Git repository) để tạo repository server. 

- Sau khi đã tạo một repository trên Github bạn sẽ có được địa chỉ SSH trỏ tới kho chứa mà bạn vừa tạo, chẳng hạn: https://github.com/try-git/try_git.git (là kho chứa rỗng cung cấp bởi cho mục đích demo)

- Cuối cùng ta sẽ liên kết kho chứa git ở local với kho chứa trên server qua lệnh git sau:

```
// git remote add [shortname] [SSH repository]
git remote add origin https://github.com/try-git/try_git.git
```
#### 1.7. Đưa/Cập nhật thay đổi lên server

Ta cần cập nhật những thay đổi lên server qua lệnh **push**:

```
git push -u origin master
```
Trong đó tên remote là **origin** và cập nhật lên nhánh **master** (nhánh mặc định). **-u** chỉ thị cho Git nhớ các tham số origin và master, trong các lệnh push tiếp theo ta chỉ cần gõ ```git push```.

#### 1.8. Kéo/Cập nhật thay đổi từ server

Khi có ai đó trong team cập nhật thay đổi lên server Git, ta cần nhật thay đổi đó về local với lệnh sau:

```
git pull origin master
```
#### 1.9. Khôi phục

Các files có thể được khôi phục lại trạng thái ban đầu ở lần commit cuối cùng.

Giả sử: bạn thay đổi file *readme.md* và sao đó bạn lại muốn phục hồi lại file *readme.md* ban đầu

Tạo có thể phục hồi lại file với câu lệnh sau:
```
git checkout -- readme.md
```
> Chú ý: File được khôi phục lại ở lần commit cuối cùng

#### 1.10. Nhánh

Khi developers làm việc với một tính năng hoặc bug, thường sẽ cần tạo một copy code của họ sang một nhánh mới (not master branch) để không ảnh hưởng tới nhánh chính (master). Sau khi hoàn thành xong mới merge thay đổi vào master.

G/s ta cần tạo một nhánh *clean_up*:
```
git branch clean_up
```
#### 1.11. Chuyển nhánh

Bây giờ nếu gõ lênh ```git branch``` sẽ thấy ta đang làm việc tại nhánh master. Để chuyển sang nhánh *clean_up* để phát triển, ta thực hiện lệnh sau:
```
git checkout clean_up
```
#### 1.20. Quy trình Merge

Hiện tại ta đang ở nhánh "clean_up". Hãy thực hiện những lệnh dưới đây:

```
//1. Tạo file mới feature.txt
touch feature.txt
//2. Tổ chức file feature.txt
git add feature.txt
// Xóa file readme.md
git rm readme.md
//3. Commit thay đổi
git commit -m "Developed new feature"
//4. Trở lại nhánh chính
git checkout master
// Merge nhánh clean_up vào master
git merge clean_up
```
Các thao tác từ 1-4 giả định quá trình ta phát triển trên nhánh *clean_up*. Sau khi phát triển xong ta trở lại nhánh chính (4) để cập nhật những thay đổi. Lệnh **merge** dùng để gộp nhánh "clean_up" vào nhánh hiện tại (master)

#### 1.21. Xóa nhánh

Khi mục đích phát triển trên một nhánh hoàn thành hoặc tả không cần nữa, để xóa nhánh *clean_up* ta dùng lệnh:
```
git branch -d clean_up
```

#### 1.21. Final

Lúc này điều bạn cần làm là push những thay đổi lên repository server.

```
git push
```
## Stuff

#### Làm thế nào thể resolve conflicts files

Trong trường hợp khi có nhiều người làm việc trên cùng một file, tạo thay đổi cùng một dòng. Khi ấy Git sẽ không biết nên phải bỏ/giữ phần nào. Cụ thể như:
T và D code trên cùng 1 file
- T cập nhật code lên nhánh master
- D lúc sau cũng cập nhật code lên nhánh master
Khi này D sẽ bị conflict, vì version tại working copy của D không phải là bản mới nhất. 

Vậy làm sao thể resolve trường hợp này. 
D phải tự quyết định merge và sau đó đẩy lên master. Nhưng thông thường theo chuẩn thì source code sẽ được tách thành các nhánh cho mục đích phát triển khác nhau, sau đó sẽ được merge vào nhánh master.

- Các thành viên sẽ chỉnh sửa code của riêng họ và đẩy code lên nhánh được tạo cho họ
- Team leader sẽ là người tạo pull request và merge code vào nhánh chính master











