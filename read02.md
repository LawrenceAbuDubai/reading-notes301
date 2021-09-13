# State and Props

What are the events that occur during the component lifecycle?
Components can be defined as classes or functions in React. The methods you can use on these are referred to as lifecycle events. These methods are available throughout a component's lifespan and allow you to adjust the UI and application states.

The three steps of the component lifecycle are mounting, updating, and unmounting.
Mounting

It is during the mounting step that an instance of a component is created and injected into the DOM. During mounting, the constructor, static getDerivedStateFromProps, render, componentDidMount, and UNSAFE componentWillMount are all called in this order.

Updating

It is rerendered whenever a component is modified or its state changes. These lifecycle events occur in this order during updating.
static componentDidUpdate, UNSAFE componentWillUpdate, UNSAFE componentWillReceiveProps Unmounting getDerivedStateFromProps, shouldComponentUpdate, render, getSnapshotBeforeUpdate, componentDidUpdate, UNSAFE componentWillUpdate, UNSAFE componentWillReceiveProps

When a component is removed from the DOM, the final phase of the lifecycle is invoked. During this phase, componentWillUnmount is the single lifecycle event.

constructor()
A React component's constructor is called before it is mounted.
If the component is a subclass, super(props) must be called or the props will be undefined.

class FishTableRow extends React.Component {
constructor() {
super(props); //gives us access to props
//Don’t call this.setState() here
this.state = { //intitialize local state
showDescription: false
}; }

This.setState() should not be used in the constructor since it can produce side effects and is unneeded. This will cause all prop updates to be ignored, therefore it should only be done if it is done on purpose.
getDerivedStateFromProps static ()
This strategy is only used in rare circumstances where the state is dependent on prop changes over time.
render()
In a class component, only the render method is necessary. When called, it will look at this.props and this.state. The render method should not change the component state because doing so every time it rerenders would result in a slew of issues. I should also avoid interacting with the browser directly. If shouldComponentUpdate is true, render will not be called () returns false. Here is an example of using render.

ReactDOM.render(
<FishTable fishes= {fishData}/>,//set fishes document.getElementById(‘app’)
);

componentDidMount()
This method is called as soon as a component is mounted. This is where you should put anything that requires a network request or that has to be initialized in the DOM. This is a nice place to start if you want to set up any subscriptions. Don't forget to unsubscribe in componentWillUnmount if you do this ().
setState() can be used here, but it should be used with caution because it will force a redraw, which may create performance difficulties.
When the component is rendered, we use componentDidMount() to connect to the YouTube API and retrieve videos.

componentDidMount() {
console.log(‘got videos’);
this.getVideos(‘cats’);
}
getVideos(query) {
var options = {
key: this.props.YOUTUBE_API_KEY,
query: query
};

shouldComponentUpdate()
React's default behavior is to redraw after each state update. If you set shouldComponentUpdate() to false, you can avoid this from occuring. This is done to improve performance. If you want to use this method, PureComponent, which does a shallow comparison of props and state, would be a better choice. If you use this method, double-check the prior props and state against the current props and state. UNSAFE componentWillUpdate(), render(), and componentDidUpdate() will not be called if shouldComponentUpdate() returns false.

getSnapshotBeforeUpdate()
This is another rarely used method that allows you to capture a picture of the DOM to check it before actually changing anything on the DOM.
componentDidUpdate()
This method is useful for performing network requests after a change has occurred.
componentDidUpdate(prevProps) {
// Typical usage (don’t forget to compare props):
if (this.props.userID !== prevProps.userID) {
this.fetchData(this.props.userID);
}
}

componentWillUnmount()
This method allows you to clean up the DOM and netwrok requests/ subscriptions.
UNSAFE Lifecycle Events
UNSAFE_componentWillMount()
UNSAFE_componentWillUpdate()
UNSAFE_componentWillReceiveProps()

Because these events have resulted in several issues and unforeseen side effects, they will no longer be usable without the UNSAFE tag in front of them in React 17. Use ComponentDidMount instead of componentWillMount.
Use static getDerivedStateFromProps instead of componentWillReceiveProps.
We'll use getSnapshotBeforeUpdate instead of componentWillUpdate.
