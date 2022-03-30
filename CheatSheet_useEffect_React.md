# CheatSheet useEffect React
```javascript
import { useEffect, useState } from "react";

export default function EffectCheatSheet() {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  useEffect(() => {
    fetch("https://test.com")
      .then((response) => {
        if (response.ok) {
          return response.json();
        }
        throw response;
      })
      .then((data) => {
        setData(data);
      })
      .catch((error) => {
        console.error("error data", error);
        setError(error);
      })
      .finally(() => {
        setLoading(false);
      });
  }, []);
}
```
