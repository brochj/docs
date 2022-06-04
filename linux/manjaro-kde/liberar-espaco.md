

```sh
rm -rf ~/.config/google-chrome/Default/Service\ Worker/CacheStorage/
rm -rf ~/.cache/google-chrome/default
rm -rf ~/.cache/mozilla/firefox
yarn cache clean
docker image prune -a # remove as imagens que não estão sendo utilizadas
```