Four stages of React component Lifecycle:
1) Initialization
  This is where we define the constructor and initialie the components with some default props.

2) Mounting
  This is when the component is mounted in the DOM tree and rendered on the UI.
  The functions called are 
  a) static getDerivedStateFromProps (props, state) ----> this is used to set the state of the component based on the props passed. Always called before the render function
  b) render function contains the HTML component to rendered (may contain nested components enclosed in a div).
  c) componentDidMount is called afetr the render.

3) Updation
  This is involves the process when a component is updated....
  a) getDerivedStateFromProps (props, state) -> the state is set based on the new props passed.
  b) setState -> not a part of the lifecycle but state is updated using this method.
  c) shouldComponentUpdate -> called before render, returns boolean, if false render and componentDidUpdate function will not be called.
  d) getSnapshotBeforeUpdate(prevProps, prevState) -> always used with componentDidUpdate to get the snapshot of the previous state.
  e) componentDidUpdate -> called when a component is updated.

4) Unmounting
  componentWillUnmount() Function: This function is invoked before the component is finally unmounted from the DOM i.e. this function gets invoked once before the component is removed from the page and this denotes the end of the lifecycle.





import React from "react";
import ReactDOM from "react-dom/client";

//getDerivedStateFromProps ---> render ---> componentDidMount ----> setState -----> getDerviedStateFromProps -----> shouldComponentUpdate ----> getSnapshotBeforeUpdate ------>render

class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hello: " Gagan!" };
  }

  static getDerivedStateFromProps(props, state) {
    console.log("derive function called....", props, state);

    return { hello: props.greet };
  }

  shouldComponentUpdate(
    nextProps: Readonly<{}>,
    nextState: Readonly<{}>,
    nextContext: any
  ): boolean {
    console.log("check to be updated....");
    return true;
  }

  getSnapshotBeforeUpdate(prevProps, prevState) {
    console.log("snapshot taken");
    return true;
  }

  render() {
    console.log("rendering......");
    return (
      <div>
        <button onClick={this.onClick}>
          GeeksForGeeks.org, Hello
          {this.state.hello}
        </button>
      </div>
    );
  }

  componentDidMount() {
    console.log("component mounted......");
    //this.setState({ hello: "Geeks!" });
  }

  componentDidUpdate(
    prevProps: Readonly<{}>,
    prevState: Readonly<{}>,
    snapshot?: any
  ): void {}

  onClick() {
    console.log("clicked");
    this.setState({ hello: " Ayushi!" });
  }
}

const rootElement = document.getElementById("root")!;
console.log(rootElement);
const root = ReactDOM.createRoot(rootElement);

root.render(<App greet=" World!" />);
