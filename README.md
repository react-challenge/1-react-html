# react-html

🍉🍉🍉 use react in pure html files

## base demo

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>react html</title>
    <script src="https://unpkg.com/react@18/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  </head>
  <body>
    <div id="root"></div>
    <script type="text/babel">
      function MyApp() {
        return <h1>Hello, world!</h1>;
      }
      const container = document.getElementById("root");
      const root = ReactDOM.createRoot(container);
      root.render(<MyApp />);
    </script>
  </body>
</html>
```

## Component & Form

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>react html</title>
    <script src="https://unpkg.com/react@18/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <style>
      button {
        margin: 10px;
      }
      .bold {
        font-size: 18px;
        font-weight: bold;
      }
    </style>
  </head>
  <body>
    <div id="root"></div>
    <script type="text/babel">
      const { useState, useEffect } = React;
      function Greeting({ name }) {
        return <h1>Hello, {name}!</h1>;
      }

      function LoginForm() {
        const [name, setName] = useState("");
        const [age, setAge] = useState("");

        function nameChange(e) {
          setName(e.target.value);
        }
        function ageChange(e) {
          setAge(e.target.value);
        }
        function reset() {
          setName("");
          setAge("");
        }
        function submit() {
          if (!name || !age) {
            alert("Please enter you name or age!");
            return;
          }
          fetch("/user", {
            method: "POST",
            headers: new Headers({
              "Content-Type": "application/json",
            }),
            body: JSON.stringify({
              name,
              age,
            }),
          })
            .then((res) => console.log(res))
            .catch(console.log);
        }
        return (
          // 阻止默认事件防止页面刷新
          <form onSubmit={(e) => e.preventDefault()}>
            <input
              value={name}
              onChange={nameChange}
              placeholder="Enter your name"
            />
            <input
              value={age}
              onChange={ageChange}
              placeholder="Enter your age"
            />
            <p class="bold">
              Your Input, name: {name}， age: {age}
            </p>
            <button onClick={submit}>Submit</button>
            <button onClick={reset}>Reset</button>
          </form>
        );
      }
      const container = document.getElementById("root");
      const root = ReactDOM.createRoot(container);
      root.render(
        <div>
          <Greeting name="dev-zuo" />
          <LoginForm />
        </div>
      );
    </script>
  </body>
</html>
```
