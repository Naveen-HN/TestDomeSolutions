# TestDomeSolutions for React


1. Toggle Message  
The Message component contains an anchor element and a paragraph below the anchor. Rendering of the paragraph should be toggled by clicking on the anchor element using the following logic:

At the start, the paragraph should not be rendered.
After a click, the paragraph should be rendered.
After another click, the paragraph should not be rendered.
Finish the Message component by implementing this logic.

SOLUTION:

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

SOLUTION:

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

3. Focus

The TextInput component renders an input element in the DOM and accepts a ref that is forwarded to that input element. Finish the FocusableInput component:

The component should accept a focused prop.
When the focused prop is changed from false to true, and the input is not focused, it should receive the focus.
If on mounting the focused prop is true, the input should receive the focus.


SOLUTION:

class Input extends React.PureComponent {
  render() {
    let {forwardedRef, ...otherProps} = this.props; 
    return <input {...otherProps} ref={forwardedRef} />;
  }
}

const TextInput = React.forwardRef((props, ref) => {
  return <Input {...props} forwardedRef={ref} />;
});

class FocusableInput extends React.Component {
  
  ref = React.createRef();
  
  render() {
    return <TextInput ref={this.ref} />
  }
  
  componentDidUpdate(prevProps) {
    if (!prevProps.focused) {
      this.focus();
    }
  }
  
  componentDidMount() {
    this.focus();
  }
  
  focus() {
    if (this.props.focused && document.activeElement !== this.ref.current) {
      this.ref.current.focus();
    }
  }
}

FocusableInput.defaultProps = {
  focused: false
};

const App = (props) => <FocusableInput focused={props.focused} />;

document.body.innerHTML = "<div id='root'></div>";
const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);



