# Puttin' in work (images in Gatsby)

## Images
- making websites slow :( 
- Gatbsy images take care about everything
    - fetching data img in base64 to display when the real image is loading
    - fixing ration 
    - creates `<picture>` element with media queries inside that are fetching the right size of the image (that fits the device best)
    - loading on demand, only as they are in the view 
- we need something to process out image to create a bunch of image version that are available later (webp/small/portrait/...), two ways
    - use compute power: pipe them thru `gatsby-plugin-sharp` -> can take long 
    - use online service 
        - Sanity Image Pipline
        - Cloudinary
        - Imgix

### Gatsby image types
- fixed 
- fluid - that is what you usually want (image is responsive)

## Static query
- quering that is not inside a page element - it is inside a component for example 
- statis queries dont take variables 

