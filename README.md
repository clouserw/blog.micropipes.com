Just the content for my blog

Theme is based on [Hydure](https://github.com/zivong/jekyll-theme-hydure) and uses [Jekyll](http://jekyllrb.com)

### Local work

To preview work locally: `bundle exec jekyll serve --host 0.0.0.0 --drafts`

### Deploying

```
bundle exec jekyll build
cp _site/feed/by_tag/Mozilla.xml blog/mozilla.xml
cp _site/feed.xml blog/atom.xml
```

Then commit & push.
