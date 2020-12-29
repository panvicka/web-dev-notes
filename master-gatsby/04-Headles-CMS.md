# Headless CMS - Sanity

- option `hotspot: true` enables selection of the important part of the image that wont be cropped in any image version (landscape, thumbnail,...)

## Creating personalized Sanity field

- for example as a price input, we do not want to force non-tech people to input price in cents as they can not understand why
- create own React component with logic inside and use it instead

```javascript
// more code here - pizza.js schema
    {
      name: 'price',
      title: 'Price',
      type: 'number',
      description: 'Price of the pizza in cents',
      validation: (Rule) => Rule.min(1000).max(50000),
      inputComponent: PriceInput, // this is the custom react component
    },
// more code here
```

- this is the component with a little Sanity magic (patching is for live updates etc.)

```javascript
// more code here - PriceInput.js component
import React from 'react';
import PatchEvent, { set, unset } from 'part:@sanity/form-builder/patch-event';

function createPatchFrom(value) {
  return PatchEvent.from(value === '' ? unset() : set(Number(value)));
}

export default function PriceInput({ type, value, onChange, inputComponent }) {
  return (
    <>
      <h2>{type.title}</h2>
      <p>{type.description}</p>
      <input
        type={type.name}
        value={value}
        onChange={(event) => onChange(createPatchFrom(event.target.value))}
        ref={inputComponent}
      />
    </>
  );
}
```
