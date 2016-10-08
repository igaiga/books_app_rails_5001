# memo
- rails new books_app
- cd books_app/
- rails g scaffold book title:string memo:text
- rails db:migrate
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
