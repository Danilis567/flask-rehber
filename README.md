# Flask Nedir?

Flask, Python tabanlı hafif bir web çerçevesidir. Web uygulamaları ve API'ler oluşturmak için kullanılır. Flask, basit ve esnek yapısı sayesinde hızlı bir şekilde uygulama geliştirmenize olanak tanır.

---

## Temel Bir Uygulama

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
a
