<h1 align="center">react-css-theme-switcher</h1>
<p>
  <a href="https://www.npmjs.com/package/react-css-theme-switcher" target="_blank">
    <img alt="Version" src="https://img.shields.io/npm/v/react-css-theme-switcher.svg">
  </a>
  <img src="https://img.shields.io/badge/node-%3E%3D10-blue.svg" />
  <a href="#" target="_blank">
    <img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-yellow.svg" />
  </a>
  <a href="https://codecov.io/gh/Jfelix61/react-css-theme-switcher" target="_blank">
    <img alt="codecov" src="https://codecov.io/gh/Jfelix61/react-css-theme-switcher/branch/master/graph/badge.svg" />
  </a>
  <a href="http://makeapullrequest.com" target="_blank">
    <img alt="PRs Welcome" src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square" />
  </a>
  <img alt="Bundle size" src="https://badgen.net/bundlephobia/minzip/react" />
 
</p>

> 💫 Switch between CSS themes using React

## Prerequisites

- node >=10

## Usage

Import ThemeSwitcherProvider and pass a theme object with the name of the theme and the path to the css (normally,public folder).

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

import { ThemeSwitcherProvider } from 'react-css-theme-switcher';

const themes = {
  light: 'public/light.css',
  dark: 'public/dark.css',
};

const App = () => {
  return (
    <ThemeSwitcherProvider defaultTheme='light' themeMap={themes}>
      <Component />
    </ThemeSwitcherProvider>
  );
};
```

Use `useThemeSwitcher` Hook:

```jsx
import { useThemeSwitcher } from 'react-css-theme-switcher';

const Component = () => {
  const { switcher, themes, currentTheme, status } = useThemeSwitcher();
  const [isDarkMode, setIsDarkMode] = React.useState(false);

  if (status === 'loading') {
    return <div>Loading styles...</div>;
  }

  const toggleDarkMode = () => {
    setIsDarkMode(previous => {
      switcher({ theme: previous ? themes.light : themes.dark });
      return !previous;
    });
  };

  return (
    <div>
      <h2>Current theme: {currentTheme}</h2>
      <button onClick={toggleDarkMode} />
    </div>
  );
};
```

### Avoiding CSS Override

react-css-theme-switcher provided a way to avoid collision with other stylesheets or appended styles providing a where to inject the styles. To achieve this add an HTML comment like `<!--inject-styles-here-->` and then provide `'inject-styles-here'` in the insertionPoint prop in `ThemeSwitcherProvider`.

```html
<!DOCTYPE html>
<html lang="en">
  <head>    
    <style>
      @import url('https://fonts.googleapis.com/css2?family=Poppins&display=swap');

      * {
        color: inherit;
      }

      html {
        font-family: 'Poppins', sans-serif;
      }
    </style>
    <!-- inject-styles-here -->
    <title>Playground</title>
  </head>

  <body>
    <div id="root"></div> 
  </body>
</html>
```

```jsx
const App = () => {
  return (
    <ThemeSwitcherProvider defaultTheme='light' insertionPoint='inject-styles-here' themeMap={themes}>
      <Component />
    </ThemeSwitcherProvider>
  );
};
```

## API

### ThemeSwitcherProvider

#### Props
| Name           | Type   | Default value       | Description                                                                                                                                                                                                                         |
|----------------|--------|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| attr           | String | data-theme          | Attribute name for that will be appended to the body tag. Its value will be the current theme name.                                                                                                                                 |
| defaultTheme   | String |                     | Default theme to load on mount. Must be in themeMap                                                                                                                                                                                 |
| id             | String | current-theme-style | Id of the current selected CSS.                                                                                                                                                                                                     |
| insertionPoint | String |                     | Comment string where pre-fetch styles and current themes will be injected. The library will look for the comment string inside head element. If missing will append styles at the end of the head. This is useful for CSS override. |
| themeMap       | Object |                     | Object with all themes available. Key is the theme name and the value is the path for the CSS file.                                                                                                                                 |

### useThemeSwitcher

#### Returns

| Name         | Type                                    | Default value | Description                                                                                     |
|--------------|-----------------------------------------|---------------|-------------------------------------------------------------------------------------------------|
| currentTheme | String or Undefined                     | undefined     | Current selected theme                                                                          |
| themes       | Object                                  | themeMap keys | All themes supplied in the themeMap.                                                            |
| switcher     | ({ theme }: { theme: string }) => void; | Function      | Function to change themes.                                                                      |
| status       | enum('idle', 'loading', 'loaded')       | idle          | Current load status of the selected stylesheet. Useful to prevent flicker when changing themes. |


## Contributors

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://jfelix.info"><img src="https://avatars1.githubusercontent.com/u/21092519?s=460&u=55be9996a2652c79880c62ad50d06e17639456e8&v=4" width="100px;" alt=""/><br /><sub><b>Jose Felix</b></sub></a><br /><a href="https://github.com/Jfelix61/react-theme-switcher/commits?author=Jfelix61" title="Code">💻</a> <a href="https://github.com/Jfelix61/react-theme-switcher/commits?author=Jfelix61" title="Documentation">📖</a> <a href="https://github.com/Jfelix61/react-theme-switcher/commits?author=Jfelix61" title="Tests">⚠️</a></td>    
  </tr>  
</table>

<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://allcontributors.org) specification.
Contributions of any kind are welcome!

## Show your support

Give a ⭐️ if this project helped you!
