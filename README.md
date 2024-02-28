# Write accessible HTML emails that work everywhere

The complexity of the work of the web developer has always been to make its code works everywhere. Solutions like jQuery and Babel came to help the professional to save his time with compatibility of browser and spend his time with the new features. That age of incompatibilities for browsers is gone since we dont't need to support the Internet Explorer.

Now talking about emails there's another enemy, the IE of the email clients called Outlook. I dont't understand the real it's not updated to a new app that works with modern HTML and CSS, but until there I'm happy to help everyone who wants to overcome this challenge. 

To send and HTML it's only necessary to select all the page, the content, not the markup and paste on the email body.

During the article I'll explain some rules, in bold, to understand that is important.

## Structure

Just like the Web, the emails started as text documents. By the years the Web evolved, first with non-semantic HTML like div tags only to bring CSS styles and after JavaScript, semantic HTML, ARIA attributes and advanced CSS that replace technologies like flash. However, the majority of email clients stopped at text documents, in other words, all you will see below is a workaround to fake the evolution of the Web and bring it to email templates.

### Layout with tables

As I introduced, some email clients do not understand tags not used to write text documents and the reason is clear, their text editors only write and read text elements, i.e. all you have to place your content in columns are tables that are allowed in text documents.

Tables are grids with lines and columns aligneds with the limitation that you can not merge columns, threfore there is no possibility to create one line with full width content and other with two columns of half width. That is the reason why the layout with tables needs a lot of tables. The following image shows a color for each table.

![image](https://github.com/jomarcardoso/email-with-html/assets/27368585/18e58c2d-f988-48a8-9e06-07286081702a "lines to simulate tables")

The structure of table as layout is written the same way like in the web, but for structure it is not necessary border or space between the lines and the content, therefore you need to unsed these like the example below.

![image](https://github.com/jomarcardoso/email-with-html/assets/27368585/3e862513-595d-4f96-b202-99ca8f3e15d9 "example of a row with two columns")

### Legacy HTML

As you can see in the example of table with some unusual attributes such as border, cellpadding, cellspacing, this attributes are deprecated because the CSS can do the same in a more organized way, nevertheless, many of those CSS features is not available in some email clients, for this way to not run the risk of making a mistake, we must use these old attributes and also some legacy tags. 

![image](https://github.com/jomarcardoso/email-with-html/assets/27368585/1059dded-aa9a-4350-8b2d-a36e450d06e4 "some old tags and attributes")

About emails, redundancy is important to reach the same result in many clients, then prefer to put styles and this legacy attributes to ensure that property will be applied one way or other.

![image](https://github.com/jomarcardoso/email-with-html/assets/27368585/366dc86a-1965-4e58-89f4-75e3ebe05850 "a tag td with bgcolor attribute, class with value black and also style with background-color black")

### Reset CSS

Just like on the Web it is necessary to normalize some styles to become the development easier. It is better to apply resets because we can only investigate the styles on a browser with dev tools, but we can not see the effect of them for example in an mobile app or a desktop software. Instead of try to find out a problem of styles, apply the reset, possibly the it is solved. You can copy the [resets that I use in my personal projects.](https://github.com/jomarcardoso/email/blob/master/projects/html/styles/reset.css)

### Load CSS

As you can check in this [site of email clients what support](https://www.caniemail.com/features/html-link/) the link tag to import the styles is barely compatible instead of this you are going to prefer use style tags. Event with the styles inside the document [there is some limitations](https://www.caniemail.com/features/html-style/) if import in the head or in the body tag. Some email clients cut the elements out of the body tag and others does not accept styles inside the body. The bullet proof style tag is to copy the same style inside head and body and also create a fake head tag to be removed by some email clients.

![image](https://github.com/jomarcardoso/email-with-html/assets/27368585/c73aa236-94ed-4369-bca2-26eb95af0abe "style tag in head and body | source: https://mosaico.io/email-client-tricks/double-head-trick-yahoo-app-android/")

### Fake body

Get rid of body tag it doesn't belong to your email content. Instead of this, do yourself fake body tag and in this element you can place properties like background and that won't be removed. It's useful for Gmail.

![image](https://github.com/jomarcardoso/email-with-html/assets/27368585/94ca33de-fbd9-4b15-8772-f7e4112b05c4 "a fake body made wtih table and a class body")

## Styles

If we dont't use conventional tags, we don't use conventional CSS simple that. A common library like Bootstrap won't work well with tables. 

### style tags

A rule that I don't know right if are necessary, **embed the CSS in style tags** and **always duplicate and put the style tag in body and head elements.** There're rumors that some email clients cut the head tag and others that ignore CSS out of the a tag style inside the head, so we did both to ensure that will work well. Instead of write the styles and also duplicate them, I made a script that load the CSS, put in a tag style twice.

![image](https://github.com/jomarcardoso/email-with-html/assets/27368585/4259b3f2-d004-4ffa-9b34-8a60e866cd2c)

### CSS

Something almost excluded for most people now turns necessary for compatility of email template, it is CSS inline. Perhaps style inline is not necessary anymore, but to not test every email client, prefer this 100% granted solution. There's some tool on Web to help you with this task and I'm gonna recommend to use [htmlemail.io](https://htmlemail.io/inline/) because this tool also put the legacy attributes such as bgcolor, width...

![image](https://github.com/jomarcardoso/email-with-html/assets/27368585/a9285c8f-1650-4c42-82fd-4da3064844e1 "a conversion of an HTML with style tag to CSS inline")

### Grid

The reason why the grids came up, is to design and technology work together with a patter that speed up the development. The first time I'd seen this was with Bootstrap. Its 12 columns grid became so popular and in my opinion it concept also is fit for emails.

![image](https://github.com/jomarcardoso/email-with-html/assets/27368585/69fd668b-cb3c-425b-8ed4-ff742b3cca07 "a grid with one table six rows and twelve columns")

Tables are semantic grids and with it you can simulate something like Flexbox or Grid Layout and each approache have different structures. As like Grid Layout you create a table, like a container and every tr tag is a row and td tag is a column exactly like tables and grids work. To become more flexible you can use the HTML attributes colspan and rowspan to take more than one column or row. Pay attention, this approach you can't cross the grid lines, so it's low likely you will use on the root of your email HTML.

![image](https://github.com/jomarcardoso/email-with-html/assets/27368585/364603f6-c58f-41e3-80e1-1a4bfdff7f10 "the code of two lines of the grid, with 3 and 2 columns")

As Flexbox, the idea is split the lines in new tables, with this you don't have to follow a vertical grid and sometimes don't use any grid.

### Responsive

...

### Forbidden styles

...flex

## Images

CDN, Base64, attachment

width

SVG to PNG

## Fonts

Tag font

Web safe fonts

## Accessibility

ARIA attributes

## Conclusion

Use tools or create you one.
Summary

## Replace SVG by pixeled images

I took a screenshot of the SVG images and saved it as .png. Email don't send images instead of this you have two options, put the images online in a CDN or send as a base64 image.

## Reset of CSS

## Base HTML

Other thing very important is the base HTML for any email agent and also a CSS reset for general and specific agents. You can copy the reset.css and the base html from my GitHub. It's necessary move applied properties from the body to new root tag as part of the content because some email clients ignore the styles of the body tag e.c Gmail.

![image](https://github.com/jomarcardoso/email-with-html/assets/27368585/81233ab2-edf5-4e39-b3e3-28fa80f697ff)

The image below is a comparison in Gmail before and after applied the default CSS reset and the CSS inside the document. The main difference of this improvement is the width is well defined for all the content, and of course the background is there.

![image](https://github.com/jomarcardoso/email-with-html/assets/27368585/becabe6c-eb71-401c-921b-1da8b621d60b "left side of the image is before and the right one is after")

### CSS Inline

### Deprecated attributes

Required attributes by tag:

img: width

table: 

## References

- https://templates.mailchimp.com/development/css/client-specific-styles/
- https://www.campaignmonitor.com/blog/email-marketing/creating-a-centred-responsive-design-without-media-queries/
- https://www.emailonacid.com/blog/article/email-development/how-to-code-accessible-emails/
- https://stackoverflow.design/email/base/mso/
- https://www.htmlemailcheck.com/knowledge-base/recommended-externalclass-css-fix-outlook-com/
- https://github.com/seanpowell/Email-Boilerplate/issues/10
- https://www.caniemail.com/
- https://caniuse.email/
- https://maool.com/html-email-tips-and-tricks/yahoo/
- https://www.litmus.com/blog/do-email-marketers-and-designers-still-need-to-inline-css
- https://mosaico.io/
- https://jasemiller.medium.com/a-fix-for-outlook-image-issues-in-html-email-campaigns-b8dd1c8f7d16
- https://htmlemail.io/inline/
- https://templates.mailchimp.com/resources/inline-css/
- https://stackoverflow.com/questions/13785587/if-ie-is-not-working-as-expected-in-this-case
- https://en.wikipedia.org/wiki/Conditional_comment
