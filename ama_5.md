# Django Q&A Session

---

## 1. How to Create a Django App — Sudheer

Use the `startapp` management command inside your project directory.

```bash
python manage.py startapp myapp
```

Then register it in `settings.py`:

```python
INSTALLED_APPS = [
    ...
    'myapp',
]
```

---

## 2. What is Middleware — Snajay

Middleware is a layer that sits between the request and response cycle. It processes requests before they reach the view and responses before they are sent to the client. Common uses: authentication, logging, session handling.

```python
# settings.py
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    ...
]
```

Custom middleware example:

```python
class SimpleMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response

    def __call__(self, request):
        print("Before view")
        response = self.get_response(request)
        print("After view")
        return response
```

---

## 3. How to Retrieve Data Fast — Abhay Singh

Use `select_related` (for ForeignKey) and `prefetch_related` (for ManyToMany) to reduce database queries. Also use `.only()` or `.values()` to fetch specific fields.

```python
# Without optimization (hits DB multiple times)
books = Book.objects.all()
for book in books:
    print(book.author.name)  # N+1 queries

# With select_related (single JOIN query)
books = Book.objects.select_related('author').all()

# Fetch only needed fields
books = Book.objects.only('title', 'price')

# Use values() for dict output (faster than full model instances)
books = Book.objects.values('title', 'price')
```

---

## 4. What is `manage.py` — Akshat

`manage.py` is a command-line utility automatically created in every Django project. It lets you interact with the project — running the server, making migrations, creating superusers, etc.

```bash
python manage.py runserver       # Start development server
python manage.py makemigrations  # Create migration files
python manage.py migrate         # Apply migrations
python manage.py createsuperuser # Create admin user
python manage.py shell           # Open Django shell
```

---

## 5. Why Use `makemigrations` — Saurav

`makemigrations` detects changes made to your models and creates migration files. These files act as a version history of your database schema.

```bash
python manage.py makemigrations
```

Example: After adding a field to a model —

```python
# models.py
class Product(models.Model):
    name = models.CharField(max_length=100)
    price = models.DecimalField(max_digits=8, decimal_places=2)  # new field
```

Running `makemigrations` generates a file like `0002_product_price.py` which Django uses to update the database.

---

## 6. How Templates Work — Mudassir

Django templates are HTML files with special template tags and variables. Django's template engine renders them by substituting variables and executing tags.

```python
# views.py
def home(request):
    return render(request, 'home.html', {'name': 'Django'})
```

```html
<!-- templates/home.html -->
<h1>Hello, {{ name }}!</h1>

{% if name %}
  <p>Welcome back.</p>
{% endif %}

{% for item in items %}
  <li>{{ item }}</li>
{% endfor %}
```

Configure template directory in `settings.py`:

```python
TEMPLATES = [{
    'BACKEND': 'django.template.backends.django.DjangoTemplates',
    'DIRS': [BASE_DIR / 'templates'],
    ...
}]
```

---

## 7. How to Include App URLs in Main Project — Abhishek

Use `include()` in the main `urls.py` to delegate URL routing to each app.

```python
# project/urls.py
from django.urls import path, include

urlpatterns = [
    path('blog/', include('blog.urls')),
    path('shop/', include('shop.urls')),
]
```

```python
# blog/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='blog-home'),
    path('<int:pk>/', views.detail, name='blog-detail'),
]
```

---

## 8. What is the `path()` Function — Ashok

`path()` maps a URL pattern to a view. It is imported from `django.urls`.

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home),                    # matches /
    path('about/', views.about),             # matches /about/
    path('post/<int:id>/', views.post),      # captures integer from URL
    path('user/<str:name>/', views.profile), # captures string from URL
]
```

Converters: `int`, `str`, `slug`, `uuid`, `path`.

---

## 9. Difference Between `.filter()` and `.get()` — Abhishek

| | `filter()` | `get()` |
|---|---|---|
| Returns | QuerySet (list-like) | Single model instance |
| No match | Empty QuerySet | Raises `DoesNotExist` |
| Multiple matches | Returns all matches | Raises `MultipleObjectsReturned` |

```python
# filter() - returns QuerySet
users = User.objects.filter(is_active=True)  # can be 0, 1, or many

# get() - returns one object or raises error
user = User.objects.get(id=1)  # must match exactly one
```

Use `filter()` when expecting multiple results; use `get()` when expecting exactly one.

---

## 10. What is Atomicity — Tharun

Atomicity means a group of database operations either all succeed or all fail together — there is no partial update. In Django, this is handled using `transaction.atomic()`.

```python
from django.db import transaction

def transfer_funds(sender, receiver, amount):
    with transaction.atomic():
        sender.balance -= amount
        sender.save()
        receiver.balance += amount
        receiver.save()
        # If any line above fails, both saves are rolled back
```

---

## 11. Difference Between `aggregate()` and `annotate()` — Sireesha

| | `aggregate()` | `annotate()` |
|---|---|---|
| Scope | Entire QuerySet → single value | Per object in QuerySet |
| Returns | A dictionary | A QuerySet with extra field per row |

```python
from django.db.models import Avg, Count

# aggregate() - one summary value for the whole table
result = Product.objects.aggregate(avg_price=Avg('price'))
# {'avg_price': 49.99}

# annotate() - adds a value to each object
categories = Category.objects.annotate(product_count=Count('product'))
for c in categories:
    print(c.name, c.product_count)  # Electronics 12, Books 8
```

---

## 12. What is the Default Port in Django — Abhay

The default development server port is **8000**.

```bash
python manage.py runserver         # runs on http://127.0.0.1:8000/

# Custom port
python manage.py runserver 8080    # runs on http://127.0.0.1:8080/

# Custom host + port
python manage.py runserver 0.0.0.0:8000
```

---

## 13. What is `makemigrations` — Subhash

`makemigrations` scans your models for any changes and generates migration files in the `migrations/` folder of each app. These files describe what changes need to be applied to the database schema.

```bash
python manage.py makemigrations          # all apps
python manage.py makemigrations myapp    # specific app
```

The generated file looks like:

```python
# myapp/migrations/0001_initial.py
class Migration(migrations.Migration):
    operations = [
        migrations.CreateModel(
            name='Product',
            fields=[
                ('id', models.AutoField(primary_key=True)),
                ('name', models.CharField(max_length=100)),
            ],
        ),
    ]
```

> **Note:** `makemigrations` only creates the files. Run `python manage.py migrate` to actually apply them to the database.
