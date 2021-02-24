Now that our backend is finished, time to build our frontend! We will be building our frontend in React.

I won't go too much into React, but here's how to handle the form for registration.

```
export default class Registration extends Component {
    constructor(props) {
        super(props);
        this.state = {
            email: '',
            password: '',
            password_confirmation: '',
            RegistrationErrors: ''
        }
    }

      handleChange = (event) => {
        this.setState({
            [event.target.name]: event.target.value
        })
    }

    render() {
        return (
            <div>
                <form onSubmit={this.handleSubmit}>
                    <input type='email' name='email' value={this.state.email} placeholder="Enter your email." onChange={this.handleChange} required />
                    <input type='password' name='password' value={this.state.password} placeholder="Enter your password" onChange={this.handleChange} required />
                    <input type='password' name='password_confirmation' value={this.state.password_confirmation} placeholder="Enter your password" onChange={this.handleChange} required />
                    <input type='submit' value='Register' />
                </form>
            </div>
        )
    }
}
```

Nothing really new with this. With this block of code, this would render a form asking the user to input their email and password. Here is where the magic happens though! We have our constructor which will be a state of email and password that will start off as an empty string. We also have a base state of any registration errors that will also start off as an empty string. 

```
    handleSubmit = (event) => {
        const {email, password, password_confirmation} = this.state;

        axios.post('http://localhost:3001/registrations', {
            user: {
                email: email,
                password: password,
                password_confirmation: password_confirmation
            }
        }, 
        {withCredentials: true}
        ).then(response => {
            if (response.data.status === 'created') {
                this.props.handleSuccessfulAuth(response.data);
            }
    }).catch(error => {
        console.log("reg error", error)
    })
```

To communicate our form with the Rails API, we are going to need to use axios. Now we need all of our data from the form, we need to send that to our API which is what our handleSubmit method will do.

### What is Axios?

We need to communicate with an outside API. We are doing a POST request and the axios will take in three arguments. With axios POST, first argument is API endpoint to hit (the url), the next is the data that we want to send into our POST request and these need to be passed in as an object. The last argument is to set the cookie and persist it. This is going to be another object, withCredentials: true, never forget this third argument. This is what tells the API that it's okay to set the cookie in our client. Without this, it would not have permission to do it. 

Axios returns a promise, then we want to take that response to ___. If we have any errors, we want to catch that error.

We are passing props, handleSuccessfulAuth(response.data). Only pass this if the user has been created.

```
export default class Home extends Component {
    constructor(props) {
        super(props);
        this.handleSuccessfulAuth = this.handleSuccessfulAuth.bind(this);
        this.handleLogoutClick = this.handleLogoutClick.bind(this);
    }

    handleSuccessfulAuth(data) {
        this.props.handleLogin(data);
        this.props.history.push('/dashboard');
    }

    ...
```

Now we bind the handleSuccessfulAuth method, it receives the user data, and inside of the method, we are going to perform two key tasks. First is that it needs to call the parent app component. We are calling the handleLogin method to go grab the data and pass it onto the App component. The second task is to redirect the user, which we can push the dashboard onto the user's history. 

```
export default class App extends Component {
  constructor() {
    super();
    this.state = {
      loggedInStatus: "NOT_LOGGED_IN",
      user: {}
    };

    this.handleLogin = this.handleLogin.bind(this);
    this.handleLogout = this.handleLogout.bind(this);
  }

   handleLogin(data) {
    this.setState({
      loggedInStatus: "LOGGED_IN",
      user: data.user
    })
  }

  ...
```

handleLogin is going to update the state, it takes in an argument of data and the user is going to filled with the data.

Now that is the full registration component!