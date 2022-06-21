# Material UI

[공식문서](https://mui.com/material-ui/getting-started/installation/)

## Styled-Components with MUI

```
npm install @mui/material @emotion/react @emotion/styled
```

```
...
  <React.StrictMode>
    <StyledEngineProvider injectFirst>
      ...
        <App />
      ...
    </StyledEngineProvider>
  </React.StrictMode>
...
```

- 사용할 때는 아래와 같이 `styled-components`와 함께 섞어서 사용.

```
import styled from "styled-components";
import { Card, CardMedia, CardContent, Typography } from "@mui/material";

const PostCard = styled(Card)`
  width: 90%;
  background-color: #efefef;
  margin-bottom: 20px;
  flex-shrink: 0;
`;

const PostCardMedia = styled(CardMedia)`
  height: 130px;
  background-color: #27ae60;
`;

const Post = () => {
  return (
    <PostCard>
      <PostCardMedia></PostCardMedia>
      <CardContent>
        <Typography variant="h5">제목</Typography>
        <Typography variant="body2">본문</Typography>
      </CardContent>
    </PostCard>
  );
};

export default Post;

```
