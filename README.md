John Gruber [remarked](https://twitter.com/gruber/status/701951688903630848) that image syntax was his biggest mistake with Markdown, and [mentioned](https://twitter.com/gruber/status/701951915605827585) an alternative:

> My best idea for good Markdown img syntax would be to just paste in a URL ending in .jpg/.png/.gif etc.

We liked the idea:

```
http://example.com/minard.jpg (Napoleon’s disastrous Russian campaign of 1812)
/Flowchart.png "Engineering Flowchart"
```

At the time, we were also looking for a syntax for [file transclusion][transclusion]. The same idea applied equally well to other file types:

```
/Savings Account.csv 'Recent Transactions'
/Example.swift
/Lorem Ipsum.txt
```

CSV files are embedded as tables, source code files become code blocks, and embedded text files help writers structure their work:

	| Debit | Credit |
	|:--|:--|
	| 0 | 0 |
	[Recent Transactions]
	
	```swift
	print("Hello World!")
	```
	
	Lorem ipsum dolor sit amet.

We decided to call this syntax “content blocks”. You can try it in [iA Writer 4][iA Writer] today.

We think that content blocks are a natural extension of Markdown. We’d be happy if more apps supported them. We’re publishing this spec to aid the process, and to start the conversation around it. We’re just getting started. Your suggestions are welcome.

We describe content block syntax closely following John Gruber’s [Markdown Syntax][Markdown] and [CommonMark Spec][CommonMark].

[transclusion]: https://en.wikipedia.org/wiki/Transclusion
[iA Writer]: https://ia.net/writer
[Markdown]: https://daringfireball.net/projects/markdown/syntax
[CommonMark]: http://spec.commonmark.org

---

A content block consists of:

- a [online image][online-image] URL, or a [local file][local-file] path, optionally indented by up to three spaces;
- optionally followed by a [title][], enclosed in double or single quotes, or enclosed in parentheses, which, if present, must be separated from the URL or path by one or more spaces (or tabs).

[online-image]: #online-image
[local-file]: #local-file
[title]: #content-block-title

---

A <a id="online-image" href="#online-image">online image</a> URL consists of either:

- a sequence of zero or more characters between an opening `<` and a closing `>` that contains no spaces, line breaks, or unescaped `<` or `>` characters, or
- a nonempty sequence of characters that does not include ASCII space or control characters, and includes parentheses only if (a) they are backslash-escaped or (b) they are part of a balanced pair of unescaped parentheses that is not itself inside a balanced pair of unescaped parentheses

which includes:

- a period, followed by one of the following path extensions: `png` `jpg` `jpeg` `gif` `tif` `tiff`.

iA Writer automatically uses direct links for images hosted on some services. Currently, it adds `raw=1` query item for online image URLs from GitHub and Dropbox.

---

A <a id="local-file" href="#local-file">local file</a> path consists of one or more path components. Path component consists of:

- a forward slash `/`;
- followed by file name: a sequence of one or more characters including spaces (but not tabs);
- followed by path extension (optional for all but last path component), which consists of a period, followed by a sequence one or more uppercase or lowercase ASCII characters or numbers.

---

A content block <a id="content-block-title" href="#content-block-title">title</a> consists of of either:

- a sequence of zero or more characters between straight double-quote characters `"`, including a `"` character only if it is backslash-escaped, or
- a sequence of zero or more characters between; straight single-quote characters `'`, including a `'` character only if it is backslash-escaped, or
- a sequence of zero or more characters between matching parentheses `(...)`, including a `)` character only if it is backslash-escaped.

Content block titles block titles have obvious uses for some files, for example image alt attributes and figure captions, table captions. Content block titles are ignored when there’s no obvious use, for example with other plain text files.

Source code path extensions are mapped to programming language names with [`Languages.json`](Languages.json).
