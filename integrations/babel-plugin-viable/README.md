<p align="center">
    <img alt="Viable Logo" height="250px" src="https://user-images.githubusercontent.com/14347895/159069181-53bce5b3-a831-43f1-8c14-af6c6ed7b92b.svg">
</p>

A babel plugin that converts string literals and template strings containing Viable syntax to regular expression syntax.

To mark a string for the plugin, add `/*viable*/` before it.

## Install

```sh
npm install --save-dev babel-plugin-viable
```

or

```sh
yarn add -D babel-plugin-viable
```

## Usage

```jsonc
// .babelrc
{
  "plugins": ["babel-plugin-viable"]
}
```

## Example

### Input

```js
const regex = new RegExp(/*viable*/ `2 to 3 of "na";`);

const otherRegex = new RegExp(/*viable*/ '5 to 9 of "other";');

const rawRegex = /*viable*/ `
  <start>; 
  "other";
  <end>;
`;

const thirdRegex = new RegExp(rawRegex);
```

### Output

```js
const regex = new RegExp('(?:na){2,3}');
const otherRegex = new RegExp('(?:other){5,9}');
const rawRegex = '^other$';
const thirdRegex = new RegExp(rawRegex);
```

## Known issues

- Interpolation within template strings is not currently supported

## Links

- [Language Documentation](https://yoav-lavi.github.io/viable/book/)
- [Repository](https://github.com/yoav-lavi/viable)
