# django-rest-4

## Links
- https://www.django-rest-framework.org/tutorial/1-serialization/

## Commands 1
- pip install djangorestframework
- pip install django # not needed, installed by djangorestframework
- pip install pygments # for code highlighting
- pip install python-dotenv
- django-admin startproject tutorial
- cd tutorial
- python manage.py startapp snippets
- python manage.py makemigrations snippets
- python manage.py migrate snippets
- pip install httpie
- http http://127.0.0.1:8000/snippets/ --unsorted
- http http://127.0.0.1:8000/snippets/2/ --unsorted


## Commands 2
- python manage.py shell
```
from snippets.models import Snippet
from snippets.serializers import SnippetSerializer
from rest_framework.renderers import JSONRenderer
from rest_framework.parsers import JSONParser

snippet = Snippet(code='foo = "bar"\n')
snippet.save()

snippet = Snippet(code='print("hello, world")\n')
snippet.save()

serializer = SnippetSerializer(snippet)
serializer.data

content = JSONRenderer().render(serializer.data)
content
```

```
import io

stream = io.BytesIO(content)
data = JSONParser().parse(stream)

serializer = SnippetSerializer(data=data)
serializer.is_valid()

serializer.validated_data
serializer.save()

serializer = SnippetSerializer(Snippet.objects.all(), many=True)
serializer.data
```






