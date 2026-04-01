# kiranpatils-website
kiranpatils-website

https://gohugo.io/host-and-deploy/host-on-github-pages/

Local
hugo server -D


# 1. Check it looks right in browser
hugo server -D

# 2. Do a full minified build to catch any errors
hugo --minify

# 3. If no errors, push
git add .
git commit -m "your message"
git push