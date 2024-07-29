# Udemy Gutenberg Course

## Section 1: Introduction and project setup

### 1. Important Read theis before you start the course
- Nothing to report about this section

### 2. Introduction
- Nothing to report about this section.

### 3. Udemy Ratings and Reviews
- Skipped this

### 4. Environment and project setup
- Introduced `npx @wordpress/create-block block-name`
- Not sure how I feel about the above command.  I feel like there'll be a lot of debris created when using this command.

### 5. IMPORTANT! BREAKING CHANGE!
- Not sure if this is still an issue.

### 6. Codebase overview
- `npx @wordpress/create-block block-name` creates a plugin.  Not sure if that's ideal.
- `__DIR__` => Current directory.  Not sure if I ever knew that.

### 7. Update the plugin structure and metadata
- `node -v > .nvmrc` is a handy command to create a .nvmrc file

## Section 2: Create the Curvy Block

### 8. Start implementing the side panel
- react components (such as the `Edit()` thingie), can only return one parent element.  That's why return statements are wrapped in a `react fragment`
```
return (
    <> // <-- start react fragment
        //stuff
    </> // <-- /end react fragment
)
```
- inspector controls component
```
// taken from app/public/wp-content/plugins/blockylicious/src/blocks/curvy/edit.js

import {InspectorControls, useBlockProps} from '@wordpress/block-editor';
...
export default function Edit() {
    return (
        <>
            <p {...useBlockProps()}>
                {__('Test – hello from the editor!', 'test')}
            </p>
            <InspectorControls>
                Test Message
            </InspectorControls>
        </>
    );
}
```
### 9. Build out the side panel
- `PanelBody` react component: WordPress gives us the `PanelBody` component to style inspector elements
```
import {PanelBody} from '@wordpress/components';
...
export default function Edit() {
    return (
        <>
            <p {...useBlockProps()}>
                {__('Test – hello from the editor!', 'test')}
            </p>
            <InspectorControls>
                <PanelBody title="Top Curve">
                    Test message
                </PanelBody>
            </InspectorControls>
        </>
    );
```
- had to run `npm install @wordpress/components --save` to get the components package
- If you want to include inline styles, you have to pass them like this `<div style={{ display: flex; }}>`
- I probably need to find a resource that includes all the different wordpress react components
- `import metadata from './block.json'` <-- pretty neat
- if you want to use a JavaScript function in the return statement, you have to wrap it in `{ }`

### 10. Introduction to block attributes

## Section 3: Extra customizations for the curvy block

## Section 4: Create the Clicky blocks

## Section 5: Create the Piccy blocks

## Section 6: Block patterns and default block styles

## Section 7: Low-highlight text effect for rich text

## Section 8: Extra
