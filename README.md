<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Styled Form with Validation</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f9f9f9;
        }

        form {
            background: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 400px;
        }

        h2 {
            text-align: center;
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
        }

        input {
            width: 100%;
            padding: 10px;
            margin-bottom: 15px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 1em;
            box-sizing: border-box;
        }

        input:focus {
            border-color: #0077cc;
            outline: none;
            box-shadow: 0 0 5px rgba(0, 119, 204, 0.5);
        }

        input:invalid {
            border-color: red;
        }

        button {
            width: 100%;
            padding: 10px;
            background: #0077cc;
            color: #fff;
            border: none;
            border-radius: 5px;
            font-size: 1em;
            cursor: pointer;
        }

        button:hover {
            background: #005fa3;
        }

        .error-message {
            color: red;
            font-size: 0.9em;
            margin-top: -10px;
            margin-bottom: 10px;
        }
    </style>
</head>
<body>
    <form novalidate>
        <h2>Register</h2>
        <label for="name">Name</label>
        <input type="text" id="name" name="name" placeholder="Enter your name" required>
        <span class="error-message" aria-live="polite"></span>

        <label for="email">Email</label>
        <input type="email" id="email" name="email" placeholder="Enter your email" required>
        <span class="error-message" aria-live="polite"></span>

        <label for="password">Password</label>
        <input type="password" id="password" name="password" placeholder="Enter your password" minlength="8" required>
        <span class="error-message" aria-live="polite"></span>

        <button type="submit">Submit</button>
    </form>

    <script>
        const form = document.querySelector('form');
        const errorMessages = document.querySelectorAll('.error-message');

        form.addEventListener('submit', (e) => {
            errorMessages.forEach(msg => msg.textContent = '');

            const name = form.elements['name'];
            const email = form.elements['email'];
            const password = form.elements['password'];

            if (!name.validity.valid) {
                e.preventDefault();
                name.nextElementSibling.textContent = 'Please enter your name.';
            }

            if (!email.validity.valid) {
                e.preventDefault();
                email.nextElementSibling.textContent = 'Please enter a valid email address.';
            }

            if (!password.validity.valid) {
                e.preventDefault();
                if (password.validity.tooShort) {
                    password.nextElementSibling.textContent = 'Password must be at least 8 characters.';
                } else {
                    password.nextElementSibling.textContent = 'Please enter a valid password.';
                }
            }
        });
    </script>
</body>
</html>


