# PythonBackendHomework

### Реализовать OAuth2-авторизацию
Через любую социальную сеть, используя библиотеку social-auth-app-django. Должна быть готова страница с кнопкой, по нажатию на которую произойдет механизм авторизации. Также для авторизованного пользователя должна отображаться кнопка логаута.

### Написать декоратор, проверяющий авторизацию при вызовах API
На все функции view, требующие чтобы пользователь был залогинен в системе, навесить САМОПИСНЫЙ декоратор, проверяющий есть ли пользователь в объекте HttpRequest, иначе - редирект на страницу логина

### Изменить запросы и код API

Изменить вьюхи так, чтобы в них учитывался текущий пользователь.
Допустим, у вас функция, возвращающая заказы пользователя. Тогда ваш код был:

```python
def get_orders(request):
	orders = Order.objects.all()
	return JsonResponse({'orders': [{'id': order.id, 'date': order.date} for order in orders]})
```

Станет:

```python
@login_required
def get_orders(request):
	# берем закаты текущего пользователя из запроса
	orders = Order.objects.filter(user=request.user)
	return JsonResponse({'orders': [{'id': order.id, 'date': order.date} for order in orders]})
```