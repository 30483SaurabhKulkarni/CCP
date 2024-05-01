- Create New Project
- After that open cloud shell, then

- Step 2: Set your project (if you haven't already)
    ```
    gcloud config set project YOUR_PROJECT_ID
    ```

- Step 3: Navigate to your application directory

Add some files in Folder or Clone Repo from Github
main.py
``` py
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html')

if __name__ == '__main__':
    app.run()
```

app.yaml
``` yaml
runtime: python39
```

requirement.txt
``` txt
Flask>=2.0
Werkzeug>=2.2
```

index.html file in templates folder
``` html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome to My App</title>
</head>
<body>
    <h1>Welcome to My App!</h1>
    <p>This is the main page of my web application.</p>
    <p>Feel free to explore!</p>
</body>
</html>
```

- Step 4: Deploy your application to App Engine
    ```
    gcloud app deploy
    ```

- Step 5: Access your deployed application
    ```
    gcloud app browse
    ```
