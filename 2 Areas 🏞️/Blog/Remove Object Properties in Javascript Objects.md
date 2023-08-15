---
title: "Remove Object Properties in Javascript Objects"
description: "It is mine and I love it!"
pubDate: "Aug 15 2023"
---

```typescript
const CdnImage: React.FC<CommonProps & CdnImageProps> = ({ alt, src, dropShadow, ...rest }) => {


// remove elementID from rest to avoid passing it to the DOM and causing a warning

const { elementID, ...newRest } = rest;

  

return (

<Image

loader={CdnImageLoader}

onError={() => console.error("Failed to load image", src)}

src={src}

alt={alt}

style={style}

priority={false}

data-element-id={elementID}

{...newRest}

/>

);

};

  

export default CdnImage;
```