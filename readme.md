# Bible

This repo contains JSON and TXT Bibles to be served from GitHub pages:

[philholden.github.io/bible/json/kjv.json](philholden.github.io/bible/json/kjv.json)  
[philholden.github.io/bible/json/cuv.json](philholden.github.io/bible/json/cuv.json)  

The .txt Bibles are a little smaller than the JSON ones:

[philholden.github.io/bible/json/kjv.txt](philholden.github.io/bible/json/kjv.txt)  
[philholden.github.io/bible/json/cuv.txt](philholden.github.io/bible/json/cuv.txt)  

This is the codec used to translate between JSON and txt formats:

```javascript
export const encode = (bible) =>
  bible.map(book =>
    book.map(chapter =>
      chapter.map(({ n, txt }) =>
        `${n}|${txt}`
      ).join('')
    ).join('||')
  ).join('|||')

export const decode = (bible) =>
  bible.split('|||').map(book =>
    book.split('||').map(unflattenChapter)
  )

const unflattenChapter = chapter =>
  chapter
    .replace(/\d+\|/g, match => `||${match}`)
    .substr(2)
    .split('||')
    .map(verse => {
      const [n, txt] = verse.split('|')
      return { n, txt }
    })
```
