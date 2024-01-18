# Flask Nedir?

Flask, Python tabanlı hafif bir web çerçevesidir. Web uygulamaları ve API'ler oluşturmak için kullanılır. Flask, basit ve esnek yapısı sayesinde hızlı bir şekilde uygulama geliştirmenize olanak tanır.

---

## Temel Bir Uygulama Örnegi

Flask ile temel bir uygulama şu şekildedir:

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def ana_sayfa():
    return 'Merhaba, Flask Dünyası!'

if __name__ == '__main__':
    app.run(debug=True)
```

Bu uygulama, tarayıcınızda `http://localhost:5000` adresine gidildiğinde "Merhaba, Flask Dünyası!" metnini görüntüler.

## Dışarıdan Erişilebilir Sunucu
Uygulamanızı dış ağlardan erişilebilir yapmak için şu şekilde çalıştırabilirsiniz:
```python
app.run(host='0.0.0.0')
```
Bu, uygulamanızın dış IP adresiniz üzerinden erişilebilir hale gelmesini sağlar.

## Hata Ayıklama Modu
Uygulamanızı geliştirirken hata ayıklama yapmak için debug modunu kullanabilirsiniz:

```python
app.run(debug=True)
```
Bu, hata mesajlarını daha ayrıntılı bir şekilde görmenizi sağlar.

## Html template 

```html
<!doctype html>
<title>Hello from Flask</title>
{% if name %}
  <h1>Hello {{ name }}!</h1>
{% else %}
  <h1>Hello, World!</h1>
{% endif %}
```

Flask, HTML şablonlarını templates klasörü içinde arar. Bu nedenle, proje dizininde templates adlı bir klasör oluşturun ve içine index.html dosyasını ekleyin.

```file
/application
    /__init__.py
    /templates
        /hello.html

```



