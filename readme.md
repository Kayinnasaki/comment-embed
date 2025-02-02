# Blue Sky Comment Embedding through iFrames

I designed [bsky-comments](https://github.com/Kayinnasaki/bsky-comments) to embed bluesky replies as "comments" on small websites,
but unfortunately neocities, a great place for this kind of thing, has prohibitive COR rules that prevents that script from running.

The solutions, like with other comment boxes, is *iframes*. This setup allows you to call the script in an offsite. This repository is designed
to be forked and modified, where you can publish it as a github page and add your own changes or CSS.

If that's too much for you, I have published a version here that you can use. You won't be able to style the comments at all, but it's easy to drop in anywhere.

The Easiest method is to use the auto feature.


[https://kayinnasaki.github.io/comment-embed/](https://kayinnasaki.github.io/comment-embed/)

Going there alone only gives you a blank page, but by adding you **DID** and a *post ID**...

[https://kayinnasaki.github.io/comment-embed/#did:plc:scmcyemdposb4vuidhztn2ui#3lbb32nb4322g](https://kayinnasaki.github.io/comment-embed/#did:plc:scmcyemdposb4vuidhztn2ui#3lbb32nb4322g)

you'll get a feed of comments. This gets formatted as `comment-embed/#{{Poster's DID}}#{{Post ID}}`. On the other side of things, on your page, you can embed the comments like...

A new, and easier version is to use the auto feature...

`https://kayinnasaki.github.io/comment-embed/auto/#user.bsky.app#https://link.to/article#https://link.to/style/comments.css`

The 3 hashes here are for *your handle, *the link to your post*, and optionally *a link to a CSS style sheet*. The script will find the first time you posted that link on bluesky and make that the comments. By doing this, you can have a fairly automated comment system.

Also keep in mind the CSS is remote, so refer to any images in it with full URLs. You can add CSS to the previous method in the same way.

```html
<iframe
    onload='javascript:resizeIframe(this);'
    id="comments"
    src="https://kayinnasaki.github.io/comment-embed/#did:plc:scmcyemdposb4vuidhztn2ui#3lbb32nb4322g"
    frameborder="0"
    scrolling="no"
    class="" style="width:100%"></iframe>
<script src="https://cdn.jsdelivr.net/npm/@iframe-resizer/parent@5.3.2"></script>
<script>
    // If you're using this on neocities there is probably no way in hell you're commercial so you should be allowed to use this
    // ... Don't worry about it
    iframeResize({
        license: 'GPLv3',
        waitForLoad: true
    }, '#comments');
</script>
```

Alternatively for the iframe source you can do something like...

```html
<iframe
    onload='javascript:resizeIframe(this);'
    id="comments"
    src=""
    frameborder="0"
    scrolling="no"
    class="" style="width:100%"></iframe>
<script>
    // Set up auto-comments using current page URL
    const handle = 'your.handle.bsky.social'; // Set this to your handle
    const commentFrame = document.getElementById('comments');
    const currentURL = encodeURIComponent(window.location.href);
    const cssURL = 'https://example.com/your/css/file.css'; // Optional: your CSS URL
    
    commentFrame.src = `https://kayinnasaki.github.io/comment-embed/auto/#${handle}#${currentURL}${cssURL ? '#' + cssURL : ''}`;

    iframeResize({
        license: 'GPLv3',
        waitForLoad: true
    }, '#comments');
</script>
```

and just put this on every page you want to support comments. Then just post the link on bluesky and it SHOULD work.

*(or refer to `neocities-example.html`)*

iframeResizer helps the fact the iframe doesn't know how big it's supposed to be until the page loads. If someone can figure out how to do this without it, please let me know.
