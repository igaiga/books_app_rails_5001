# 画像投稿機能付き書籍管理アプリ

- Ruby 2.3.1
- Rails 5.0.0.1

- http://igarashikuniaki.net/rails_textbook/
  - CRUDからモデルの章あたり＋画像投稿機能追加

# 実行方法

- bundle install
- rails s

# 構築方法

## CRUD
- rails new books_app
- cd books_app/
- rails g scaffold book title:string memo:text
- rails db:migrate

## author追加
- rails g migration AddAuthorToBooks author:string
- rails db:migrate
- app/views/books/_form.html.erb 修正
```
+  <div class="field">
+    <%= f.label :author %><br>
+    <%= f.text_field :author %>
+  </div>
```
- app/views/books/show.html.erb修正
```
+<p>
+  <strong>Author:</strong>
+  <%= @book.author %>
+</p>
```
- app/views/books/index.html.erb 修正
```
+      <th>Author</th>
```
```
+        <td><%= book.author %></td>
```
- app/controllers/books_controller.rb 修正
```
params.require(:book).permit(:title, :memo, :author)
```
## 画像投稿
- rails g migration AddPictureToBooks picture:string
- rails db:migrate
- Gemfile 最後の行に追加
```
# my gems
gem 'carrierwave'
```
- bundle install
- rails g uploader Picture
- app/model/book.rb 修正
```
class Book < ApplicationRecord
+  mount_uploader :picture, PictureUploader
end
```
- app/views/books/_form.html.erb 修正
```
+  <div class="field">
+    <%= f.label :picture %><br>
+    <%= f.file_field :picture %>
+  </div>
```
- app/views/books/show.html.erb修正
```
+<p>
+  <strong>Picture:</strong>
+  <%= image_tag(@book.picture_url) if @book.picture.present? %>
```
- app/views/books/index.html.erb 修正
```
+      <th>Picture</th>
```
```
+        <td><%= book.picture %>
```
- app/controllers/books_controller.rb 修正
```
params.require(:book).permit(:title, :memo, :author, :picture)
```
