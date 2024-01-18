# Flask ile Temel Konseptler / bitmedi

 - Routing Variable Rules Unique URLs 
 - Redirection Behavior URL
 - Building HTTP Methods 
 - Static Files 
 - Rendering Templates 
 - File Uploads
 - Cookies 
 - Redirects and Errors 
 - APIs with JSON 
 - Logging


## Routing Variable Rules

Flask'ta URL'leri dinamik olarak oluşturmak ve yönetmek için değişken kuralları kullanabilirsiniz. Örneğin:



```py
from flask import Flask

app = Flask(__name__)

@app.route('/kullanici/<kullanici_adi>')
def kullanici_profili(kullanici_adi):
    return f'Kullanıcı Profili: {kullanici_adi}'

if __name__ == '__main__':
    app.run(debug=True)
```

Yukarıdaki örnekte, "/kullanici/username" şeklindeki URL'lere dinamik olarak yanıt verilecektir.

## Unique URLs / Redirection Behavior

Flask'ta benzersiz URL'ler oluşturmak için `url_for` fonksiyonunu kullanabilirsiniz. Aynı zamanda, yönlendirmeler ile farklı URL'lere yönlendirme yapabilirsiniz:



```py
from flask import Flask, redirect, url_for

app = Flask(__name__)

@app.route('/yonlendir')
def yonlendir():
    return redirect(url_for('ana_sayfa'))

if __name__ == '__main__':
    app.run(debug=True)` 
```

Yukarıdaki örnekte, "/yonlendir" URL'sine gidildiğinde, `ana_sayfa` fonksiyonuna yönlendirme yapılır.

## URL Building

Flask'ta URL oluşturmak için `url_for` fonksiyonunu kullanabilirsiniz. Bu, URL'leri manuel olarak oluşturmak yerine isimlendirilmiş rotalardan faydalanmanızı sağlar:


```py
from flask import Flask, url_for

app = Flask(__name__)

@app.route('/')
def ana_sayfa():
    return 'Ana Sayfa'

@app.route('/iletisim')
def iletisim():
    return 'İletişim Sayfası'

if __name__ == '__main__':
    with app.test_request_context():
        print(url_for('ana_sayfa'))
        print(url_for('iletisim'))` 
```
Yukarıdaki örnekte, `url_for` fonksiyonu ile isimlendirilmiş rotalara uygun URL'leri oluşturabilirsiniz.

## HTTP Methods

Flask ile HTTP metodlarını yönetmek için `methods` parametresini kullanabilirsiniz:



`from flask import Flask, request

app = Flask(__name__)

@app.route('/giris', methods=['GET', 'POST'])
def giris():
    if request.method == 'POST':
        # POST metoduyla gelen verileri işle
    else:
        # GET isteği için sayfayı göster` 

Yukarıdaki örnekte, "/giris" URL'sine sadece GET ve POST metodları ile erişilebilir.

## Static Files

Flask ile statik dosyaları (CSS, JS) sunmak için `static` klasörünü kullanabilirsiniz:


`<!-- templates/index.html -->
<link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">` 

Yukarıdaki örnekte, `style.css` dosyasını kullanmak için `url_for` fonksiyonu ile statik klasöründen CSS dosyasının yolu alınmıştır.

## Rendering Templates

Flask'ta HTML şablonlarını kullanmak için `render_template` fonksiyonunu kullanabilirsiniz. Şablon dosyalarını `templates` klasörü içine eklemelisiniz:


`from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def ana_sayfa():
    return render_template('index.html', baslik='Flask ile Çalışma')

if __name__ == '__main__':
    app.run(debug=True)` 

Yukarıdaki örnekte, `render_template` fonksiyonu ile `index.html` şablonu çağrılmış ve `baslik` değişkeni ile dinamik içerik eklenmiştir.

## File Uploads

Flask ile dosya yükleme işlemi için `request.files` kullanılabilir:

pythonCopy code

`from flask import Flask, request

app = Flask(__name__)

@app.route('/yukle', methods=['POST'])
def dosya_yukle():
    if 'dosya' not in request.files:
        return 'Dosya seçilmedi!'
    
    dosya = request.files['dosya']
    # Dosya işlemleri
    return 'Dosya yüklendi: ' + dosya.filename

if __name__ == '__main__':
    app.run(debug=True)` 

Yukarıdaki örnekte, "/yukle" URL'sine POST metodu ile dosya yükleme işlemi gerçekleştirilmektedir.

## Cookies

Flask ile çerezlerle çalışmak için `request.cookies` ve `make_response` fonksiyonlarını kullanabilirsiniz:


`from flask import Flask, request, make_response

app = Flask(__name__)

@app.route('/cerez-oluştur/<isim>')
def cerez_olustur(isim):
    resp = make_response(f'Çerez oluşturuldu: {isim}')
    resp.set_cookie('kullanici_adi', isim)
    return resp

@app.route('/cerez-oku')
def cerez_oku():
    kullanici_adi = request.cookies.get('kullanici_adi')
    return f'Çerezden okunan kullanıcı adı: {kullanici_adi}'

if __name__ == '__main__':
    app.run(debug=True)` 

Yukarıdaki örnekte, "/cerez-oluştur" URL'sine gidildiğinde bir çerez oluşturulur ve "/cerez-oku" URL'sine gidildiğinde bu çerez okunur.

## Redirects and Errors

Flask ile yönlendirmeler ve hata sayfalarını yönetmek için `redirect` ve `abort` fonksiyonlarını kullanabilirsiniz:


`from flask import Flask, redirect, abort

app = Flask(__name__)

@app.route('/yonlendir')
def yonlendir():
    return redirect('/')

@app.route('/hata')
def hata():
    abort(404)

if __name__ == '__main__':
    app.run(debug=True)` 

Yukarıdaki örnekte, "/yonlendir" URL'sine gidildiğinde ana sayfaya yönlendirme yapılır. Ayrıca, "/hata" URL'sine gidildiğinde 404 hatası üretilir.

## APIs with JSON

Flask ile JSON tabanlı API'ler oluşturmak için `jsonify` fonksiyonunu kullanabilirsiniz:


`from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/api/veri')
def veri_al():
    veri = {'anahtar': 'değer'}
    return jsonify(veri)

if __name__ == '__main__':
    app.run(debug=True)` 

Yukarıdaki örnekte, "/api/veri" URL'sine gidildiğinde JSON formatında bir veri döndürülmektedir.

## Logging

Uygulamanızdaki olayları kaydetmek için Python'un `logging` modülünü kullanabilirsiniz:


`import logging

app.logger.addHandler(logging.StreamHandler())
app.logger.setLevel(logging.INFO)

@app.route('/log')
def log_olustur():
    app.logger.info('Bu bir bilgi mesajıdır.')
    return 'Log oluşturuldu!'` 

Yukarıdaki örnekte, "/log" URL'sine gidildiğinde bir bilgi logu oluşturulur.

Bu başlıklar, Flask ile temel konseptleri anlamanıza yardımcı olacaktır. Daha fazla detay ve özellik için Flask Resmi Belge adresini inceleyebilirsiniz.
