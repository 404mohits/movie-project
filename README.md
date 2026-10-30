# Movie Library

A movie library web app built with **React** and **Redux**. It uses the **TMDb (The Movie Database) API** to show popular movies, search results and detailed movie information. Users sign in to save their favorite movies.

## Features

- **Popular movies:** a grid of currently popular movies with poster and rating
- **Movie search:** results update dynamically as you type
- **Movie details:** title, poster, language, description, rating, genres, release date and cast
- **Favorites:** save or remove movies and view them on your profile
- **User sign in:** simple login with protected pages (PrivateRoute)
- **Loading and error handling:** a spinner while data loads and a clear message if something fails
- **Responsive design:** works on mobile and desktop, with a collapsible navigation bar
- **Sample data fallback:** if no API key is set, the app runs with built-in sample movies

## Tech stack

| Purpose | Tool |
|---|---|
| UI | React 18 (Create React App) |
| State management | Redux, React-Redux, Redux-Thunk |
| Routing | React Router DOM v6 |
| API calls | Axios |
| Styling | Bootstrap 5 and custom CSS |
| Data source | TMDb API |

## Getting started

### 1. Install dependencies

```bash
npm install
```

### 2. Add your TMDb API key

1. Create a free account at https://www.themoviedb.org/signup
2. Open https://www.themoviedb.org/settings/api and copy the **API Key (v3)**
3. Copy `.env.example` to a new file named `.env` in the project root (the folder that contains `package.json`)
4. Add your key:

```
REACT_APP_TMDB_KEY=your_api_key_here
```

No quotes and no spaces. Without a key, the app still works using sample movies.

### 3. Run the app

```bash
npm start
```

Open http://localhost:3000. Restart the app whenever you change `.env`.

### Login

This is a demo login. Use any username with 3 or more characters and any password with 4 or more characters.

## Project structure

```
movie-library/
├── public/
│   └── index.html
├── src/
│   ├── api/
│   │   ├── tmdb.js            # API functions (popular, search, details)
│   │   └── sampleData.js      # sample movies used when no API key is set
│   ├── redux/
│   │   ├── types.js           # action type names
│   │   ├── actions.js         # actions and thunks (async API calls)
│   │   ├── reducers.js        # popular, search, details and auth reducers
│   │   └── store.js           # Redux store with thunk middleware
│   ├── components/
│   │   ├── Navbar.js          # responsive navigation bar
│   │   ├── MovieList.js       # popular movies page
│   │   ├── MovieSearch.js     # search page
│   │   ├── MovieDetails.js    # single movie page
│   │   ├── MovieGrid.js       # grid layout for movie cards
│   │   ├── MovieCard.js       # one movie card with save button
│   │   ├── Login.js           # sign in page
│   │   ├── Profile.js         # user favorites
│   │   ├── PrivateRoute.js    # blocks pages until the user signs in
│   │   └── Status.js          # Loader and ErrorMsg components
│   ├── App.js                 # routes
│   ├── index.js               # Provider (Redux) and BrowserRouter
│   └── styles.css
├── .env.example
└── package.json
```

## Routes

| Path | Page | Access |
|---|---|---|
| `/login` | Sign in | Public |
| `/` | Popular movies | Signed-in users |
| `/search` | Search movies | Signed-in users |
| `/movie/:id` | Movie details | Signed-in users |
| `/profile` | Favorites | Signed-in users |

## How it works

1. **Components** dispatch a thunk, for example `fetchPopularMovies()`.
2. The **thunk** sets `loading`, calls the TMDb API through Axios, then dispatches a success or failure action.
3. The **reducer** updates the store with `items`, `loading` and `error`.
4. The component reads the store with `useSelector` and shows a loader, an error message or the movies.

Redux state has four parts: `popular`, `search`, `details` and `auth` (the signed-in user and favorites). The `auth` part is saved in `localStorage`, so login and favorites stay after a page refresh.

## Notes

- The login is for learning only. Passwords are not verified and there is no backend.
- Never upload your `.env` file or API key to GitHub.
- This product uses the TMDb API but is not endorsed or certified by TMDb.
