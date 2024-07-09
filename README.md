# Django-Boilerplate-for-Rest-Api



## স্ট্যাটিক ফাইল | Static File

Django তে, স্ট্যাটিক ফাইলগুলি হল এমন ফাইল যা ব্রাউজারের দ্বারা সরাসরি প্রদর্শিত হয়। উদাহরণস্বরূপ, চিত্র, CSS ফাইল এবং JavaScript ফাইলগুলি স্ট্যাটিক ফাইল।

এই টিউটোরিয়ালে, আমরা Django তে স্ট্যাটিক ফাইলগুলি কীভাবে পরিচালনা করবেন তা শিখব। আমরা নিম্নলিখিত বিষয়গুলি কভার করব:

***স্ট্যাটিক ফাইলগুলি কীভাবে সেটিংস করবেন***

***স্ট্যাটিক ফাইলগুলি কীভাবে সংরক্ষণ করবেন***

***স্ট্যাটিক ফাইলগুলি কীভাবে আপনার ওয়েবসাইটে লোড করবেন***

## স্ট্যাটিক ফাইলগুলি কীভাবে সেটিংস করবেন

Django তে, স্ট্যাটিক ফাইলগুলিকে STATICFILES_DIRS সেটিংয়ের মাধ্যমে সংজ্ঞায়িত করা হয়। এই সেটিংটি একটি সারণী যা স্ট্যাটিক ফাইলগুলির জন্য অবস্থানের একটি তালিকা রয়েছে।

আপনি আপনার Django প্রজেক্টের settings.py ফাইলে STATICFILES_DIRS সেটিংটি সংজ্ঞায়িত করতে পারেন। উদাহরণস্বরূপ, নিম্নলিখিত কোডটি আপনার প্রজেক্টের মূল ডিরেক্টরিতে একটি static ডিরেক্টরিতে স্ট্যাটিক ফাইলগুলি সংজ্ঞায়িত করবে:

```python
import os
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'static'),
]
```

## স্ট্যাটিক ফাইলগুলি কীভাবে সংরক্ষণ করবেন

আপনি আপনার Django প্রজেক্টের static ডিরেক্টরিতে স্ট্যাটিক ফাইলগুলি সংরক্ষণ করতে পারেন। এই ডিরেক্টরিতে, আপনি আপনার চিত্র, CSS ফাইল এবং JavaScript ফাইলগুলি সংরক্ষণ করতে পারেন।

উদাহরণস্বরূপ, নিম্নলিখিত কোডটি একটি static ডিরেক্টরিতে একটি images ডিরেক্টরি তৈরি করে এবং একটি logo.png ফাইলটি সেই ডিরেক্টরিতে সংরক্ষণ করে:

```python
# settings.py

STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'static'),
]

# static/images/

logo.png

```

## স্ট্যাটিক ফাইলগুলি কীভাবে আপনার ওয়েবসাইটে লোড করবেন

Django আপনাকে আপনার ওয়েবসাইটে স্ট্যাটিক ফাইলগুলি লোড করতে {% load static %} এবং {% static 'filename' %} টেমপ্লেট ট্যাগগুলি ব্যবহার করতে দেয়।

উদাহরণস্বরূপ, নিম্নলিখিত কোডটি আপনার ওয়েবসাইটের base.html টেমপ্লেটে একটি চিত্র লোড করে:

```python
{% load static %}

<img src="{% static 'images/logo.png' %}" alt="Logo">
```

***এই কোডটি static/images/logo.png ফাইলটি লোড করবে এবং এটিকে base.html টেমপ্লেটে img ট্যাগের মাধ্যমে প্রদর্শন করবে।***


## ডেভেলপমেন্ট মোডে স্ট্যাটিক ফাইলের অতিরিক্ত সেটিংস

আপনি যদি ডেভেলপমেন্ট মোড কাজ করেন তখন স্ট্যাটিক ফাইল কাজ করানোর জন্য প্রজেক্টের urls.py ফাইলে নিচের কোডটি লিখতে হয়। তা ছাড়া অনেক সময় ইমেজ লোড হয় না।

```python
from django.urls import path, include

urlpatterns = [
    path('static/', include('django.contrib.staticfiles.urls')),
]
```

## STATIC_ROOT সেট করা

আমরা আমাদের প্রজেক্টের static ফাইলের পাথ বলে দিয়েছি কিন্তু আমাদের app এ স্ট্যাটিক ফাইল থাকতে পারে এবং আমরা যা আমাদের প্রজেক্ট ফোল্ডারে আনতে হবে python manage.py collectstatic কমান্ড দিলে কপি হয়ে কোন ফোল্ডারে আসবে তা বলে দিতে হবে settings.py ফাইলে।

```python
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')  # Define your STATIC_ROOT
```

## app ফোল্ডারে কিভাবে স্ট্যাটিক ফাইল ব্যবহার করবো এবং প্রজেক্ট এর সাথে যুক্ত করবো।

মনেকরি আমাদের app এর নাম accounts এবং এর মধ্যে আমরা templates ফোল্ডারে html রেখেছি এবং css ও images ফাইল ব্যবহার করতে চাচ্ছি তাহলে আমাদের app ফোল্ডারে static নামে ফোল্ডার তৈরী করতে হবে তার মধ্যে স্ট্যাটিক ফাইল রাখতে হবে

```bash
accounts/
|-- static/
|   
|     |-- fonts/
|     |   |-- material-icon/
|     |       |-- css/
|     |           |-- material-design-iconic-font.min.css
|     |-- css/
|         |-- style.css
```

## app এ এভাবে ব্যবহার করতে হবে
```python
    <link rel="stylesheet" href="{% static 'fonts/material-icon/css/material-design-iconic-font.min.css' %}">
    <link rel="stylesheet" href="{% static 'css/style.css' %}">
    ```

*** কমান্ড টি রান করলে স্ট্যাটিক ফাইল কপি হবে প্রজেক্ট এ এবং ওখান থেকে লোড হবে

```bash
python manage.py collectstatic 
```