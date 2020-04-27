# TestDomeSolutions


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
