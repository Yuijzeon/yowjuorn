# yowjuorn
在 Heroku 上部署 Express 反向代理伺服器

## How To Use
把這個存儲庫部署到您的 Heroku 上

並在 Heroku 的 `Settings` 頁面上 找到 `Config Vars`

填入 KEY: `TARGET_URL` VALUE: `http://您要反向代理的網址`

## 說明
`Procfile`: 用於 Heroku 啟動 APP 的檔案

`package.json`: 在這邊可以調整 Heroku Node.JS 所需要的 npm dependencies

`index.js`: Express 主程式
> `process.env.TARGET_URL`: 是上面自訂的反向代理的URL
> 
> `process.env.PORT`: 是 Heroku 保留的環境變數 傳回 APP 運行的埠口

　

index.js 示範著將所有 URL 反向代理到同一 `TARGET_URL` 若要反向代理到不同目標 可以這樣寫:
```js
app.all('/mysite1/*', createProxyMiddleware({
  target: process.env.TARGET1_URL,
  pathRewrite: { '^/mysite1': '', }
}))

app.all('/mysite2/*', createProxyMiddleware({
  target: process.env.TARGET2_URL,
  pathRewrite: { '^/mysite2': '', }
}))
```
並在 `Config Vars` 加入 `TARGET1_URL` 和 `TARGET2_URL` 的對應值

* 在 `https://<HerokuAppName>.herokuapp.com/mysite1/` 會和 `TARGET1_URL` 達到同一頁面
* 在 `https://<HerokuAppName>.herokuapp.com/mysite2/` 會和 `TARGET2_URL` 達到同一頁面
