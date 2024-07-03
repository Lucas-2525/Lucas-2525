rom django.contrib import admin
from django.urls import path, include
from django.conf.urls.static import static
from . import settings

urlpatterns = [
	path('admin/', admin.site.urls),
	path('', include('store.urls'))
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)

from django.db import models


class Category(models.Model):
	name = models.CharField(max_length=50)

	@staticmethod
	def get_all_categories():
		return Category.objects.all()

	def __str__(self):
		return self.name        kuods,ov2.@lliollooalsofjumsonlfosllolldoaw

from django.db import models


class Customer(models.Model):
	first_name = models.CharField(max_length=50)
	last_name = models.CharField(max_length=50)
	phone = models.CharField(max_length=10)
	email = models.EmailField()
	password = models.CharField(max_length=100)

	# to save the data
	def register(self):
		self.save()

	@staticmethod
	def get_customer_by_email(email):
		try:
			return Customer.objects.get(email=email)
		except:
			return False

	def isExists(self):
		if Customer.objects.filter(email=self.email):
			return True

		return False

from django.db import models
from .category import Category


class Products(models.Model):
	name = models.CharField(max_length=60)
	price = models.IntegerField(default=0)
	category = models.ForeignKey(Category, on_delete=models.CASCADE, default=1)
	description = models.CharField(
		max_length=250, default='', blank=True, null=True)
