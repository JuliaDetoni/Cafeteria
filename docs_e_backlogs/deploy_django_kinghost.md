## 🧹 Plano: Começar do zero (mas de verdade agora)

### Passo 1: Backup do que temos (só por segurança)

```bash
cd ~/apps_wsgi
mv cafe cafe_backup_inception_$(date +%Y%m%d_%H%M%S)
```

### Passo 2: Criar estrutura limpa

```bash
cd ~/apps_wsgi
mkdir cafe
cd cafe

# Criar o venv
python3.9 -m venv venv
source venv/bin/activate

# Instalar Django
python -m pip install django==4.2.* mysqlclient

# Criar o projeto Django CORRETAMENTE
# O ponto (.) é crucial — cria na raiz atual, não cria subdiretório
django-admin startproject cafe .
```

**A estrutura final deve ser:**
```
~/apps_wsgi/cafe/
├── manage.py
├── cafe/                    ← pacote de configuração do Django
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
└── venv/
```

### Passo 3: Criar o `cafe.wsgi` em `~/apps_wsgi/`

```bash
cat > ~/apps_wsgi/cafe.wsgi << 'EOF'
import sys
import os

sys.path = [p for p in sys.path if '/.local/' not in p]

HOME = '/home/creta'
PROJECT_DIR = HOME + '/apps_wsgi/cafe'
VENV_SITE = HOME + '/apps_wsgi/cafe/venv/lib/python3.9/site-packages'

sys.path.insert(0, VENV_SITE)
sys.path.insert(0, PROJECT_DIR)

os.environ['DJANGO_SETTINGS_MODULE'] = 'cafe.settings'

from django.core.wsgi import get_wsgi_application
application = get_wsgi_application()
EOF
```

### Passo 4: Configurar `settings.py`

Edita `~/apps_wsgi/cafe/cafe/settings.py`:

```python
# --- ~/apps_wsgi/cafe/cafe/settings.py
# (só as linhas que precisam mudar)

ALLOWED_HOSTS = ['creta.dev.br', 'www.creta.dev.br', 'localhost', '127.0.0.1']

ROOT_URLCONF = 'cafe.urls'
WSGI_APPLICATION = 'cafe.wsgi.application'

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'creta01',
        'USER': 'creta01',
        'PASSWORD': 'EJROSose12n',
        'HOST': 'mysql64-farm2.uni5.net',
        'PORT': '3306',
        'OPTIONS': {
            'charset': 'utf8mb4',
            'init_command': "SET sql_mode='STRICT_TRANS_TABLES'",
        },
    }
}

STATIC_URL = 'static/'
STATIC_ROOT = '/home/creta/www/cafe/static/'
MEDIA_URL = '/media/'
MEDIA_ROOT = '/home/creta/www/cafe/media/'

LANGUAGE_CODE = 'pt-br'
TIME_ZONE = 'America/Sao_Paulo'
USE_I18N = True
USE_TZ = True
```

### Passo 5: Criar `urls.py` com Hello World

```python
# --- ~/apps_wsgi/cafe/cafe/urls.py
from django.contrib import admin
from django.urls import path
from django.http import HttpResponse

def hello(request):
    return HttpResponse("☕ Hello World do Cafe!")

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', hello),
]
```

### Passo 6: Criar pastas e rodar migrations

```bash
mkdir -p ~/www/cafe/static
mkdir -p ~/www/cafe/media

cd ~/apps_wsgi/cafe
source venv/bin/activate
python manage.py migrate
python manage.py collectstatic --noinput
```

### Passo 7: Touch no wsgi e testar

```bash
touch ~/apps_wsgi/cafe.wsgi
```

Acede: `https://creta.dev.br/cafe/`

---

## 🎭 Sobre o `uada` que quebrou

Depois de arrumar o `cafe`, a gente volta pro `uada`. O `uada.wsgi` provavelmente dependia de algum arquivo que tu deletaste. A gente recria.

---

## ❓ Quer que eu gere tudo pronto?

Posso criar um **script shell** que tu corres no servidor e ele faz tudo de uma vez (backup, cria estrutura limpa, instala Django, configura settings, cria urls, roda migrate, etc.).

**Queres o script ou prefere fazer passo a passo manual?**

E me conta: como foi que aconteceu o Inception? 😂 Foi `startproject cafe` sem o ponto? KKKKKK
