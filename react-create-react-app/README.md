# Observable Example: create-react-app

To run this example, you must clone this repository and install it. From the terminal:

```
git clone https://github.com/observablehq/examples.git
cd examples/react-create-react-app
yarn
yarn start
```

Then go to http://localhost:3000 to view the live app.

This repo was created using `create-react-app`:

```
yarn create react-app react-zoomable-sunburst
```

To install the Observable runtime:

```
yarn add @observablehq/runtime
```


Lastly, to instantiate the notebook, see App.js:

```js
import {Runtime, Inspector} from '@observablehq/runtime';
import React, {useEffect, useRef} from 'react';
import notebook from './@d3/zoomable-sunburst';
import './App.css';

export default function App() {
  const ref = useRef();

  useEffect(() => {
    const runtime = new Runtime();
    runtime.module(notebook, (name) => {
      if (name === 'chart') {
        return new Inspector(ref.current);
      }
    });
    return () => runtime.dispose();
  }, []);

  return (
    <>
      <h1>Hello, Observable!</h1>
      <div ref={ref} />
    </>
  );
}
```
