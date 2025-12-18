# models field and related fields to build model

Basic import 
```python
from django.db import models
import uuid
```

The identifiers
```python
id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
```

Text and Strings
```python
name = models.CharField(max_length=255)
description = models.TextField(blank=True, null=True)
slug = models.SlugField(max_length=255, unique=True)
created_at = models.DateField(auto_now=True)
created_at = models.DateTimeField(auto_now_add=True)
updated_at = models.DateTimeField(auto_now=True)
is_active = models.BooleanField(default=True)
```

Numbers
```python
age = models.IntegerField()
phone = models.PositiveIntegerField()
half_value = models.FloatField()
num_com = models.DecimalField(max_digits=10, decimal_places=2)
```

Date and Time
```python
today_date = models.DateField()
date_time = models.DateTimeField()
time = models.TimeField()
```

boolen/status
```python
models.BooleanField(default=False)
```

Choices
```python
STATUS_CHOICES = [
    ('pending', 'Pending'),
    ('active', 'Active'),
    ('completed', 'Completed'),
]

orders = models.CharField(max_length=20, choices=STATUS_CHOICES, default='pending')
```

Relationship Field
```python
rel = models.ForeignKey('app.Model', on_delete=models.CASCADE, related_name='items')

rel = models.OneToOneField('app.Model', on_delete=models.CASCADE)

rel = models.ManyToManyField('app.Model', blank=True)
```

User-Related-Field
```python
from django.conf import settings

models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE, related_name='objects')

#Common variation

created_by = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.SET_NULL, null=True, blank=True)
```

Media and Files
```python
models.ImageField(upload_to='images/', blank=True, null=True)
models.FileField(upload_to='files/', blank=True, null=True)
```