# 1.Next.js とは

参考：[初めての Next.js 入門](https://youtu.be/eEP7CLqnRr0)

React だと JS を読み込んで、レンダリングするため、白い画面が出てしまう

これをサーバ側でプリレンダリングしてから、クライアント側で表示することで、UX、SEO を高めることが出来る  
→SG(Static Generation),SSR(Server Side Rendering)

# 2.プロジェクト作成

該当フォルダで、コマンドよりプロジェクトを作成する。

```
// -tsはtypescriptプロジェクトのためのオプション
npx create-next-app {プロジェクト名} --ts
```

# 3.フォルダ構成

pages フォルダにあるファイル名が、そのまま URL(ルーティング)に使用される。

```
project
 ├ public：画像などの静的なファイル
 ├ pages：ページファイル
 ├ styles：cssファイル
 └ components：コンポーネントファイル(デフォルトではない)
```
