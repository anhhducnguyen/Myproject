# How to deploy app Django use Heroku

### Cách này đẩy cả file `db.sqlite3` lên `Heroku`


#### Điều kiện tiên quyết

1. Đảm bảo `requirements.txt` chứa các thư viện sau

    ```python
    Django==5.0.6
    django-heroku==0.3.1
    gunicorn==22.0.0
    ```

2. Đảm bảo `Procfile` có chứa đoạn mã sau, trong đó `myproject` là tên dự án lúc bạn tạo `django`

    ```python
    web: gunicorn myproject.wsgi --log-file -
    ```

3. Đảm bảo `settings.py` có chứa

- Giúp không bị mất `css`

  ```python
  import django_heroku
  django_heroku.settings(locals())
  ```

- Đảm bảo có chứa tên miền
  
  ```python
  ALLOWED_HOSTS = [
      'chat-123-b5f27fe98cab.herokuapp.com',
  ]
  ```


**Step 1.** Tạo app trên `Heroku` tại [Heroku](https://dashboard.heroku.com/)

**Step 2.** Sử dụng `powershell` di chuyển đến thư mục bạn đang làm việc
  
  ```
   cd E:\2ndSemester3rdYear\applicationAnalysis\Myproject
  ```

**Step 3.** Đăng nhập `Heroku` bằng cách sử dụng câu lệnh sau trên `powershell`

  ```
  heroku login
  ```

**Step 4.** Tạo kho lưu trữ

```
git init
```

**Step 5.** Kết nối với `chat-123` tên app mà bạn đã đặt trên `Heroku`

```
heroku git:remote -a chat-123
```


```
git add .
```

```
git commit -m "commit"
```

```
git push heroku master
```

**Step 6.** Nếu có lỗi hãy sử dụng sau đó `push` lại

```
heroku config:set DISABLE_COLLECTSTATIC=1
```

### Cách này kết nối `aiven.io` với `Heroku` cơ sở dữ liệu sử dụng `mysql`


#### Điều kiện tiên quyết

1. Tài khoản `aiven.io` là bắt buộc, bạn có thể đăng ký tài khoản tại [aiven](https://console.aiven.io/)

2. Đảm bảo `requirements.txt` chứa các thư viện sau

    ```python
    Django==5.0.6
    django-heroku==0.3.1
    gunicorn==22.0.0
    mysqlclient==2.2.4
    python-dotenv==1.0.1
    ```

3. Đảm bảo `Procfile` có chứa đoạn mã sau, trong đó `myproject` là tên dự án lúc bạn tạo `django`

    ```python
    web: gunicorn myproject.wsgi --log-file -
    ```

4. Đảm bảo `settings.py` có chứa

- Giúp không bị mất `css`

  ```python
  import django_heroku
  django_heroku.settings(locals())
  ```

- Đảm bảo có chứa tên miền
  
  ```python
  ALLOWED_HOSTS = [
      'chat-123-b5f27fe98cab.herokuapp.com',
  ]
  ```

- Đảm bảo có các dòng này trong `setting.py`
  
    ```python
    import os
    from pathlib import Path
    from dotenv import load_dotenv
    ```

 - Đảm bảo có các dòng này trong `setting.py` để lấy dữ liệu từ file `.env`
   
    ```python
    load_dotenv()
    
    DATABASES = {
        "default": {
            "ENGINE": os.getenv('DB_ENGINE'),
            "NAME": os.getenv('DB_NAME'),
            "USER": os.getenv('DB_USER'),
            "PASSWORD": os.getenv('DB_PASSWORD'),
            "HOST": os.getenv('DB_HOST'),
            "PORT": os.getenv('DB_PORT'),
        }
    }    
    ```

 - Đẩy code lên `Heroku` bằng cách

   ```
   git add .
   ```

   ```
   git commit -m "aiven connect"
   ```
   
   ```
   git push heroku master
   ```


