# Blue Sky Comment Embedding through iFrames

I designed [bsky-comments](https://github.com/Kayinnasaki/bsky-comments) to embed bluesky replies as "comments" on small websites,
but unfortunately neocities, a great place for this kind of thing, has prohibitive COR rules that prevents that script from running.

The solutions, like with other comment boxes, is *iframes*. This setup allows you to call the script in an offsite. This repository is designed
to be forked and modified, where you can publish it as a github page and add your own changes or CSS.

If that's too much for you, I have published a version here that you can use. You won't be able to style the comments at all, but it's easy to drop in anywhere.

[https://kayinnasaki.github.io/comment-embed/](https://kayinnasaki.github.io/comment-embed/)

Going there alone only gives you a blank page, but by adding you **DID** and a *post ID**...

[https://kayinnasaki.github.io/comment-embed/#did:plc:scmcyemdposb4vuidhztn2ui#3lbb32nb4322g](https://kayinnasaki.github.io/comment-embed/#did:plc:scmcyemdposb4vuidhztn2ui#3lbb32nb4322g)

you'll get a feed of comments. This gets formatted as `comment-embed/#{{Poster's DID}}#{{Post ID}}`. On the other side of things, on your page, you can embed the comments like...

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

*(or refer to `neocities-example.html`)*

iframeResizer helps the fact the iframe doesn't know how big it's supposed to be until the page loads. If someone can figure out how to do this without it, please let me know.
