# TestDomeSolutions for React


1. Toggle Message  
The Message component contains an anchor element and a paragraph below the anchor. Rendering of the paragraph should be toggled by clicking on the anchor element using the following logic:

At the start, the paragraph should not be rendered.
After a click, the paragraph should be rendered.
After another click, the paragraph should not be rendered.
Finish the Message component by implementing this logic.

Template
class Message extends React.Component {
  render() {
    return (<React.Fragment>
          <a href="#">Want to buy a new car?</a>
          <p>Call +11 22 33 44 now!</p>
        </React.Fragment>);
  }
}

document.body.innerHTML = "<div id='root'> </div>";
  
const rootElement = document.getElementById("root");
ReactDOM.render(<Message />, rootElement);

Solution:
class Message extends React.Component {
  state = { show: false }
  render() {
    return (<React.Fragment>
          <a href="#" onClick={()=>this.setState({show: !this.state.show})}>Want to buy a new car?</a>
        { this.state.show ? <p>Call +11 22 33 44 now!</p> : null }
        </React.Fragment>);
  }
}
document.body.innerHTML = "<div id='root'> </div>"; 
const rootElement = document.getElementById("root");
ReactDOM.render(<Message />, rootElement);


2. Change Username

This application should allow the user to update their username by inputting a custom value and clicking the button.

The Username component is finished and should not be changed, but the App component is missing parts. Finish the App component so that the Username component displays the inputted text when the button is clicked.

The App component should use the React.useRef Hook to pass the input to the Username component for the input element and for the Username component.

For example, if the user inputs a new username of "John Doe" and clicks the button, the div element with id root should look like this:

<div><button>Change Username</button><input type="text"><h1>John Doe</h1></div>


Template:
class Username extends React.Component {
  state = { value: "" };

  changeValue(value) {
    this.setState({ value });
  }

  render() {
    const { value } = this.state;
    return <h1>{value}</h1>;
  }
}

function App() {
  function clickHandler() {}

  return (
    <div>
      <button onClick={clickHandler}>Change Username</button>
      <input type="text" />
      <Username />
    </div>
  );
}

document.body.innerHTML = "<div id='root'></div>";
const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);


Solution:

class Username extends React.Component {
  state = { value: "" };

  changeValue(value) {
    this.setState({ value });
  }

  render() {
    const { value } = this.state;
    return <h1>{value}</h1>;
  }
}

function App() {
  const inputRef = React.useRef(null);
  const ref = React.useRef(null);

  function clickHandler() {
    ref.current.changeValue(inputRef.current.value);
  }

  return (
    <div>
      <button onClick={clickHandler}>Change Username</button>
      <input type="text" ref={inputRef} />
      <Username ref={ref} />
    </div>
  );
}

document.body.innerHTML = "<div id='root'></div>";
const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);


