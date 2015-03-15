# Flask-JWTAuth
A JWT(Token) Authorization extension of Flask, inspired by Flask-HTTPAuth 


##Quick Start
```python
from flask import app
from jwt_auth import HTTPJWTAuth

auth_token = HTTPJWTAuth()

class User(object):
	def __init__(self):
		pass
	
	@staticmethod
	def verify_auth_token(token):
		# your verify method here
		return True

@auth_token.verify_token
def verify_auth_token(token):
	g.user = User.verify_auth_token(token)
	return g.user is not None
	
@auth_token.error_handler
def unauthorized_token():
    response = jsonify({'status': 401,
                        'error': 'unauthorized',
                        'message': 'no authentication token'})
    response.status_code = 401
    return response


@app.route('/need_token_auth')
@auth_token.auth_required
def need_auth():
	return
	
```
