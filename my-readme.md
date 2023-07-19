We need to pass another movie in MovieCard .


Props allow us to pass values into our components and making it more reusable.


```jsx
function MovieCard() {
  return (
    <div className="movie-card">
      <img
        src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTn1OTYGz2GDC1XjA9tirh_1Rd571yE5UFIYsmZp4nACMd7CCHM"
        alt="Mad Max: Fury Road"
      />
      <h2>Mad Max: Fury Road</h2>
      <small>Genres: Action, Adventure, Science Fiction, Thriller</small>
    </div>
  );
}
```


### Passing in props

To pass props to a component, you add them as attributes when you render the
component, just like adding attributes to an HTML element:

`props are enclosed with {} unless a string`

```jsx
const movieTitle = "Mad Max"
<MovieCard title={movieTitle} />          /this is more of a manual way do this instead/
```  

```jsx

<MovieCard title="Mad Max" />              /instead of using movietitle put thre movie name directly
```


Now example using props

```jsx
// parent component
function App() {
  const title = "Mad Max";
  const posterURL =
    "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTn1OTYGz2GDC1XjA9tirh_1Rd571yE5UFIYsmZp4nACMd7CCHM";
  const genresArr = ["Action", "Adventure", "Science Fiction", "Thriller"];

  return (
    <div className="App">
      {/* passing down props from the parent component */}
      <MovieCard title={title} posterSrc={posterURL} genres={genresArr} />
    </div>
  );
}

// child component
function MovieCard(props) {
  return (
    <div className="movie-card">
      <img src={props.posterSrc} alt={props.title} />
      <h2>{props.title}</h2>
      <small>{props.genres.join(", ")}</small>
    </div>
  );
}
```

## Destructuring Props

This method makes our code cleaner since we only use on argument props
so no props everywhere.


```jsx
function MovieCard({ title, posterSrc, genres }) {
  return (
    <div className="movie-card">
      <img src={posterSrc} alt={title} />
      <h2>{title}</h2>
      <small>{genres.join(", ")}</small>
    </div>
  );
}
```

### Destructuring Nested Objects


```jsx
/parent component/

function App() {
  const socialLinks = {
    github: "https://github.com/liza",
    linkedin: "https://www.linkedin.com/in/liza/",         /nested values
  };

  return (
    <div>
      <SocialMedia links={socialLinks} />
    </div>
  );
}

/child component/
function SocialMedia({ socialLinks }) {
  return (
    <div>
      <a href={socialLinks.github}>{socialLinks.github}</a>
      <a href={socialLinks.linkedin}>{socialLinks.linkedin}</a>
    </div>
  );
}
```

This is not as clean lets make a change;


**********************************************************************************************************************************
```jsx
function SocialMedia({ socialLinks }) {

  const { github, linkedin } = socialLinks;

  return (
    <div>
      <a href={github}>{github}</a>
      <a href={linkedin}>{linkedin}</a>
    </div>
  );
}
```
**********************************************************************************************************************************

or 

```jsx
function SocialMedia({ socialLinks: { github, linkedin } }) {
  return (
    <div>
      <a href={github}>{github}</a>
      <a href={linkedin}>{linkedin}</a>
    </div>
  );
}
```

## Default Values for Props

if we have a lot of movies to add and maybe a poster isnt provided we can add a default one

Instead of passing in that default poster image in case we don't have one, we can tell our MovieCard component to use a default value if the posterSrc prop was not provided. To do this, we can add the default value to our destructured props:


```jsx
function MovieCard({
  title,
  genres,
  posterSrc = "https://m.media-amazon.com/images/M/MV5BOTJjNzczMTUtNzc5MC00ODk0LWEwYjgtNzdiOTEyZmQxNzhmXkEyXkFqcGdeQXVyNzMzMjU5NDY@._V1_UY268_CR1,0,182,268_AL_.jpg",
}) {
  return (
    <div className="movie-card">
      <img src={posterSrc} alt={title} />
      <h2>{title}</h2>
      <small>{genres.join(", ")}</small>
    </div>
  );
}
```

in my `App Component` i will not use an url under posterSrc and still it will display.


```js
function App() {
  const title = "Mad Max";
  const genresArr = ["Action", "Adventure", "Science Fiction", "Thriller"];

  return (
    <div className="App">
      {/* posterSrc is omitted, so the default value will be used instead */}
      <MovieCard title={title} genres={genresArr} />
    </div>
  );
}
```

`a poster will still be displayed`.
