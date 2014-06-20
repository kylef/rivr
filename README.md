# rivr

[![Build Status](https://travis-ci.org/kylef/rivr.png?branch=master)](https://travis-ci.org/kylef/rivr)

rivr is a microweb framework inspired by djng, the reason I decided to create rivr and not use djng was that djng still depended on Django. I wanted rivr for places where I don't have Django. It is a lightweight framework which can be included along side another python application. rivr does not have a database layer, you are free to use whatever you choose.

What rivr includes:

- Django like template engine
- Domain router (Like django's URL router, but you can have a regex search over the whole domain, useful for subdomains).
- A debugging middleware
- Basic HTTP authentication

## Examples

### Simple views

```python
def hello_world(request):
    return Response('Hello, World!', content_type='text/plain')
```

### URL Routing

```python
router = Router()

@router.register(r'^$')
def index(request):
    return Response('Hello world.')

@router.register(r'^test/$')
def test(request):
    return Response('Testing!')
```

### Class based views

```python
class RESTExampleView(View):
    def get(self, request):
        return {'status': 'ok'}
```

## Testing

rivr exposes a `TestClient` which allows you to create requests and get a
response. Simply pass the TestClient your view, router or application and you
can make requests using the testing DSL to get a response.

```python
from rivr.tests import TestClient

class TestCase(unittest.TestCase):
    def setUp(self):
        self.client = TestClient(router)

    def test_status(self):
        assert self.client.get('/status/').status_code is 204
```

## License

rivr is released under the BSD license. See [LICENSE](LICENSE).

