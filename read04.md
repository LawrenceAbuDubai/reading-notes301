# Forms

Because form elements inherently preserve some internal state, they behave differently in React than other DOM elements. In basic HTML, for example, this form takes only one name:

```

<form>
  <label>
    Name:
    <input type="text" name="name" />
  </label>
  <input type="submit" value="Submit" />
</form>

```

When the user accepts the form, the default HTML form behavior is for the user to be redirected to a new page. It merely works with React if you desire this behavior. However, in most circumstances, it's more convenient to have a JavaScript function that handles form submission and has access to the data submitted by the user. The most common method is to use a technique known as "controlled components."

## Controlled Components

Form components like input, textarea, and select in HTML often keep their own state and change it based on user input. In React, mutable state is normally stored in component state and only updated with setState ().

By making the React state the "one source of truth," we may merge the two. The React component that renders a form then has control over what happens in that form when the user enters data. A "controlled component" is an input form element whose value is managed by React in this way.

For example, we may write the form as a controlled component to have the previous example log the name when it is submitted:

```

class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}

```

The displayed value will always be this.state.value because the value property is set on our form element, making the React state the source of truth. The displayed value will update as the user types since handleChange executes on every keystroke to update the React state.

The value of the input in a controlled component is always determined by the React state. While you'll have to put a little more code as a result, you'll be able to send the value to other UI elements and reset it from other event handlers.

## The textarea Tag

In HTML, a <textarea> element defines its text by its children:

```

<textarea>
  Hello there, this is some text in a text area
</textarea>

```

In React, a <textarea> uses a value attribute instead. This way, a form using a <textarea> can be written very similarly to a form that uses a single-line input:

```

class EssayForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: 'Please write an essay about your favorite DOM element.'
    };

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('An essay was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Essay:
          <textarea value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}

```

Notice that this.state.value is initialized in the constructor, so that the text area starts off with some text in it.

## The select Tag

In HTML, <select> creates a drop-down list. For example, this HTML creates a drop-down list of flavors:

```
<select>
  <option value="grapefruit">Grapefruit</option>
  <option value="lime">Lime</option>
  <option selected value="coconut">Coconut</option>
  <option value="mango">Mango</option>
</select>
```

Because of the selected property, the Coconut choice is initially picked. Instead of using the selected attribute on the root select tag, React uses the value attribute. In a controlled component, this is more convenient because you only have to change it once. Consider the following scenario:

```
class FlavorForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: 'coconut'};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('Your favorite flavor is: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Pick your favorite flavor:
          <select value={this.state.value} onChange={this.handleChange}>
            <option value="grapefruit">Grapefruit</option>
            <option value="lime">Lime</option>
            <option value="coconut">Coconut</option>
            <option value="mango">Mango</option>
          </select>
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

Overall, this makes it so that <input type="text">, <textarea>, and <select> all work very similarly - they all accept a value attribute that you can use to implement a controlled component.

Note

You can pass an array into the value attribute, allowing you to select multiple options in a select tag:

```
<select multiple={true} value={['B', 'C']}>
```

## The file input Tag

In HTML, an <input type="file"> lets the user choose one or more files from their device storage to be uploaded to a server or manipulated by JavaScript via the File API.

<input type="file" />
Because its value is read-only, it is an uncontrolled component in React.

## Handling Multiple Inputs

When you need to handle multiple controlled input elements, you can add a name attribute to each element and let the handler function choose what to do based on the value of event.target.name.

For example:

```
class Reservation extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isGoing: true,
      numberOfGuests: 2
    };

    this.handleInputChange = this.handleInputChange.bind(this);
  }

  handleInputChange(event) {
    const target = event.target;
    const value = target.type === 'checkbox' ? target.checked : target.value;
    const name = target.name;

    this.setState({
      [name]: value
    });
  }

  render() {
    return (
      <form>
        <label>
          Is going:
          <input
            name="isGoing"
            type="checkbox"
            checked={this.state.isGoing}
            onChange={this.handleInputChange} />
        </label>
        <br />
        <label>
          Number of guests:
          <input
            name="numberOfGuests"
            type="number"
            value={this.state.numberOfGuests}
            onChange={this.handleInputChange} />
        </label>
      </form>
    );
  }
}

```

Note how we used the ES6 computed property name syntax to update the state key corresponding to the given input name:

```

this.setState({
  [name]: value
});
```

It is equivalent to this ES5 code:

```

var partialState = {};
partialState[name] = value;
this.setState(partialState);
```

Also, since setState() automatically merges a partial state into the current state, we only needed to call it with the changed parts.

## Controlled Input Null Value

If you specify the value prop on a controlled component, the user will not be able to change the input unless you want them to. If you specify a value yet the input remains editable, you may have set value to undefined or null by accident.

This is demonstrated in the code below. (At first, the input is locked, but after a short delay, it becomes editable.)

```
ReactDOM.render(<input value="hi" />, mountNode);

setTimeout(function() {
  ReactDOM.render(<input value={null} />, mountNode);
}, 1000);
```
## Alternatives to Controlled Components

Because you must construct an event handler for every method your data can change and pipe all of the input information through a React component, using controlled components can be difficult at times. When converting an old codebase to React or integrating a React application with a non-React library, this can be extremely aggravating. In these cases, you might want to consider using uncontrolled components, a different approach to constructing input forms.

## Fully-Fledged Solutions

If you’re looking for a complete solution including validation, keeping track of the visited fields, and handling form submission, Formik is one of the popular choices. However, it is built on the same principles of controlled components and managing state — so don’t neglect to learn them.
