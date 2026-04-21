# Django Q&A

---

## 1. What are Views?

A **view** is a Python function or class that takes a web request and returns a web response.

```python
from django.http import HttpResponse

def home(request):
    return HttpResponse("Hello, World!")
```

> Views contain the **logic** of your app — fetching data, processing it, and sending it back.

---

## 2. What command is used to show migrations?

```bash
python manage.py showmigrations
```

This lists all apps and their migration files, showing which ones have been applied (✔) and which haven't.

```
auth
 [X] 0001_initial
 [X] 0002_alter_permission
myapp
 [X] 0001_initial
 [ ] 0002_add_field  ← not yet applied
```

---

## 3. What is `requirements.txt`?

A file that lists all the Python packages your project needs.

```txt
Django==4.2
djangorestframework==3.14
Pillow==9.5
```

**To install all packages at once:**
```bash
pip install -r requirements.txt
```

> It helps others set up the same project environment easily.

---

## 4. What is Migrations? (How to start them)

Migrations are Django's way of **saving changes to your database models**.

```bash
# Step 1: Create migration files from your models
python manage.py makemigrations

# Step 2: Apply them to the database
python manage.py migrate
```

**Example flow:**
```python
# You add a new field to your model
class Post(models.Model):
    title = models.CharField(max_length=100)
    likes = models.IntegerField(default=0)  # ← new field
```
Then run `makemigrations` → Django detects the change → `migrate` applies it to the DB.

---

## 5. What is a Reverse Proxy?

A **reverse proxy** is a server that sits in front of your app and forwards client requests to it.

```
User → Nginx (reverse proxy) → Django App (Gunicorn)
```

**Why use it?**
- Handles SSL (HTTPS)
- Serves static files faster
- Load balancing
- Hides your backend server

> **Nginx** is the most common reverse proxy used with Django in production.

---

## 6. Difference between `render` and `redirect`

| | `render` | `redirect` |
|---|---|---|
| **Does** | Returns an HTML page | Sends user to another URL |
| **HTTP Status** | 200 OK | 301/302 |
| **Use when** | Showing a page | After form submit, login, etc. |

```python
from django.shortcuts import render, redirect

def my_view(request):
    # render → shows a template
    return render(request, 'home.html', {'name': 'Django'})

def submit_view(request):
    # redirect → sends to another page
    return redirect('/success/')
```

---

## 7. What is the `render` function used for?

`render` combines a **template** with **context data** and returns an HTTP response.

```python
from django.shortcuts import render

def profile(request):
    context = {
        'username': 'venky',
        'age': 25
    }
    return render(request, 'profile.html', context)
```

**In `profile.html`:**
```html
<h1>Hello, {{ username }}!</h1>
<p>Age: {{ age }}</p>
```

> `render(request, template_name, context)` — these are its 3 main arguments.

---

## 8. How to implement Authorization?

Authorization = controlling **who can access what**.

**Method 1 — `@login_required` decorator:**
```python
from django.contrib.auth.decorators import login_required

@login_required
def dashboard(request):
    return render(request, 'dashboard.html')
```

**Method 2 — `@permission_required`:**
```python
from django.contrib.auth.decorators import permission_required

@permission_required('myapp.can_edit')
def edit_post(request):
    ...
```

**Method 3 — Check in view manually:**
```python
def secret_page(request):
    if not request.user.is_authenticated:
        return redirect('/login/')
    return render(request, 'secret.html')
```

---

## 9. Difference between MVC and MVT

| Component | MVC | MVT (Django) |
|---|---|---|
| Handles logic | **Controller** | **View** |
| Manages data | **Model** | **Model** |
| Shows UI | **View** | **Template** |

```
MVC:  User → Controller → Model → View → User
MVT:  User → URL → View → Model → Template → User
```

**Django's MVT in action:**
```python
# Model — data layer
class Article(models.Model):
    title = models.CharField(max_length=200)

# View — logic layer
def article_list(request):
    articles = Article.objects.all()
    return render(request, 'articles.html', {'articles': articles})
```

```html
<!-- Template — presentation layer -->
{% for article in articles %}
  <h2>{{ article.title }}</h2>
{% endfor %}
```

> In Django, the **framework itself acts as the Controller** — you just write Views and Templates.
