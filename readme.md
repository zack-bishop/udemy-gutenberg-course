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
- Add attributes to the block.json file
- Pass them to the `Edit()` method in the `edit.json` file.
- This makes no sense to me: `onChange={(isChecked) => props.setAttributes({ enableTopCurve: isChecked })}`.  
  - Where does the `isChecked` get set?

### 11. Implement the top SVG curve
- All components must start with a capital letter.
- Since the `components/curvy.js` exports a `const`, we have to make it a named import/
  - We need to do `import { Curve }...` instead of `import XYZ...`
  - The curly braces are the important thing to use
- Deconstructors, i.e. `...blockProps`, are going to confuse me.
- `{props.attributes.enableTopCurve && <Curve/>}`<-- That double `&` is going to confuse me.

### 12. Enable built-in attributes using "supports".
- This part is about the built-in styles settings.
- On blocks, the `setttings` tab is consists of `attributes`, the `style` tab is consists of `supports`.
- You need to get familiar with the `theme.json` file. 
- Two ways to save a style / color:
  - Selecting a preset
  - Selecting a custom color
- Lots of information here.

### 13. Different ways to add default styles
- `styles.css` is for both backend and front end.
- `editor.css` is for just the backend
- **Default Style method 1:** Editing the css files is one way to add default styling.
- While it's totally valid to add default styling via CSS, it's better to use `attributes` whenever you can.
- **Default Style Method 2:** Setting defaults via attributes
```
	"attributes": {
		"style" : {
			"type" : "object",
			"default": {
				"color": {
					"background": "#ec4899"
				}
            }
        },
        ...
    }
```
- The above is useful for adding custom, one-off styles that are recognized by the Gutenberg editor.
- There's a third way to default style things using a child theme, but it's apparently pretty involved.

### 14. Fix the curvy block styles
- This is how padding settings get set on the block:
```
{"top":"var:preset|spacing|50","bottom":"var:preset|spacing|50","left":"var:preset|spacing|30","right":"var:preset|spacing|30"}}}}
```
- The `var:preset|spacing|50` is a representation of a CSS variable set in the theme.  I need to learn more about this.
- Adding custom CSS defaults via `attributes` is cool, but I wonder if there is a way for the client to reset them?  What I mean is, what if we have a very curated block with a lot of default CSS set as attributes, then the client comes in and fiddles with them.  Like, let's say they set the padding to the preset of 5.  Is there a way to undo that and restore the custom settings they blew way?
- Hmmm... adjusting the default attributes via `block.json` requires block recovery.  For instance, if you add a `curvy` block to a page with settings `XYZ`, but then you change the defaults to `ABC` in `block.json`, the `XYZ` block requires recovery.  But if the block's defaults are adjusted by the user (say, they change 50px top padding to 51px), it doesn't require recovery.  I wonder why?  Why does WP/Gutenberg require block recovery when the defaults change?  

### 15. Implementing the height and width controls
- I wonder why we needed another react fragment when adding the additional editor controls?  
- Is it because there are multiple items in the output of the conditional?
- God, I really hate the `shorthand` that's all over JavaScript, React.
- I'd like to know if there's a resource about all the components from WordPress components.
- I'd like to know when to use a `label` property versus a `title` property on the components.

### 16. Use the height and width attributes to manipulate the curve shape


## Section 3: Extra customizations for the curvy block

## Section 4: Create the Clicky blocks

## Section 5: Create the Piccy blocks

## Section 6: Block patterns and default block styles

## Section 7: Low-highlight text effect for rich text

## Section 8: Extra
