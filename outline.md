I. Intro to APIs

## Why even API?
What is an API?
- An API is an Application Programming Interface.
- Cool story, what does that *mean*?
  - If you're at a Starbucks, you order your drink off of a menu, and pass your request over the counter to the cashier in the form of an order. The cashier processes your order, and then writes your drink request on a cup and places it in line for the barista. The barista fills your request, and passes the response (your drink) back over the counter to you. In this scenario, you're the application.
  - The application makes a request > the API (cashier) serves the request to the system (the barista) > The system gives the API the response > The API serves the response back to the application
  - The same thing happens when you use the Starbucks app to order: you put in your drink request to the app, the request gets sent to the barista, and the barista sends you a response in the form of a delicious Pumpkin Spice Latte. The Starbucks app is actually using an API behind the scenes; when you order in-person, that API is the cashier and counter where you pick up the drink.
  - The bottom line is this: APIs are how applications communicate data, and that exchange is occurring between websites more and more frequently. Developers are more open with their data, and are even encouraging other to access it, which is encouraging a more intertwined online community.

Why even API?
- A system without an API is like [a lego toy that's been super-glued together](https://cloud.githubusercontent.com/assets/27806/18210851/29f679e4-7100-11e6-9345-d41f3a83e532.jpg), it can only *be* one thing
- As developers, they allow us to craft greater experiences and insights into the platforms and systems we use, both for ourselves and for others, beyond that originally conceived
- APIs keep you from having to manually complete repetitive tasks
  - Save time, boredom, and possibly frustration
  - Computers doing the work means there is less chance for human error
    - Just as an example, how many of us have received our Starbucks coffee with a funny rendition of our names written on the cup? This won't happen if you order from the app, which keeps your name stored.
    - This isn't to say we should replace Starbucks employees with APIs, however, because then customers would miss the complete in-store experience that Starbucks provides its customers. The in-store experience also utilizes APIs for various things:
      - The Clover® machine uses an API to adjust brew time, which affects the acidity of the coffee
      - The store might play music from Spotify via an API
      - Your credit card transaction uses an API
      - That store's sales numbers are stored and tracked with APIs

Why use the GitHub API?

   - Avoid doing those repetitive tasks manually, and save time!
   - Examples of what the GitHub API can be used for:
       - Adding new hires to predetermined teams
       - Check for stale Issues over 100 days old
       - Check for repositories containing the word `password` to see if anyone is putting passwords in plain text
       - Send reminders to people with Pull Requests open for over 30 days

II. Quick GraphQL Example
      1. have 5 pull requests in 5 different repositories that people can comment on if they are just creating a GitHub account for this course
III. Build a Query
  1. What is a Query?

        ```
        query {
          viewer {
          contributedRepositories(last:5, privacy:PUBLIC) {
            edges {
              node {
                owner {
                  login
                }
                name
                url
              }
            }
          }
          }
        }
        ```

    2. Defining our query
    
    - viewer: Who is currently the logged in user? (you!)
    - contributedRepositories(last:#, privacy:PUBLIC): Contributed repositories is what is known as a connection. It a relationship between two sets of data. In this case, it is a connection between the user (in this case the logged in user) and the (most recent) repositories the viewer has contributed to. We are providing two arguments to help us limit the results.
    - Last: tells the query to return the most recent results. In this case, the # must be used to limit the number of repositories returned.
    - We also chose to only display PUBLIC repositories by providing the privacy argument. We could also set this parameter to PRIVATE, or leave it out altogether if we’d like PUBLIC and PRIVATE repositories.
    - edge: It is easiest to think of an edge as a bridge between two sets of data. You will need an edge any time you are working between nodes.
    - node: A node is a set of data. If an edge is a bridge connecting two islands, the node is the island. Within a node, you can select specific data you would like to view. In this case, the node contains the information about the repositories.

For a visual example of nodes and edges, view the GraphQL Voyager site(https://apis.guru/graphql-voyager/). Any column of data in the graphs would be considered a node, and the lines connecting them would be considered edges.
    
   - owner: Within the node, you will find specific pieces of information called interfaces. These are interfaces have additional layers of data.
   - login: The repository owner’s username on GitHub. The owner may be an individual, or an organization.
   - name: The name of the repository.
   - url: The repository’s URL.



IV. GraphQL Query Response
  1. Before clicking Query, where is our data going to be returned? Why?
  1. Examining what is returned
  1. What can we do with this data?

V. Use Query to Find Specific Information
  1. Create an issue in a repo on your account
      Run this with your specific username and repository id

        ```
        query FindIssueID {
          repository(owner: "", name: "") {

          }
        }
        ```
        
VI. Create Mutation
  1. What is a Mutation?
     Allows us to manipulate server side data, in this instance, it is going to create a list of the repositories we recently contributed to.
        
        ```
         mutation AddComment {
           addComment(input: {
             subjectId: "[issueID]",
             body: "[contribution template]"})
           {
             subject {
               id
             }
           }
         }
       ```

     Examine the mutation
     Run and watch a comment be added to the issue
