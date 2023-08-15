---
title: "Remove Object Properties in Javascript Objects"
description: "It is mine and I love it!"
pubDate: "Aug 15 2023"
---

```typescript
const Image: React.FC<ImageProps> = ({ alt, src, dropShadow, ...rest }) => {


// remove elementID from rest to avoid passing it to the DOM and causing a warning
const { elementID, ...newRest } = rest;

  

return (

<Image

src={src}
alt={alt}
style={style}

data-element-id={elementID}

{...newRest}

/>

);

};

  

export default CdnImage;
```