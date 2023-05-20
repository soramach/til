# 1.導入

Next.js では、CSS Modules を初めからサポートしている為、パッケージの追加などは必要ない>

### sass のインストール

sass(Scss,Sass)を使う場合は、インストールする必要がある

```
npm install --save-dev sass
// --save-devは、開発環境のみインストールするためのオプション
```

# 2.ファイル管理

### components ディレクトリと同じ階層に置いて管理する

> - コンポーネントと同じ場所に scss もあるため、すぐに見つけやすい
> - この場合、ディレクトリ名をコンポーネント名にして、`index.tsx`、`index.module.scss`にするかなーって思うから、コーディングの時に分かりにくくなる？
>
> ```
> components/
> └ text/
>    ├ index.tsx
>    └ index.module.scss
> ```

### components と styles ディレクトリでそれぞれ管理する

> - component と style のディレクトリが分かれるから分かりやすい？
> - ファイル名がそのまま component 名になるから、編集の時に分かりやすい
>
> ```
> components/
> └ text.tsx
> styles/
> └ text.module.scss
> ``
> ```

# 3.使い方

## ファイル名は、`xxx.modules.css(scss)`とする

```text.module.scss
.text {
    color: yellow;
    &:hover {
        background: rgba(255,255,255,0.3);
    }
}
```

```text.tsx
import styles from './text.module.scss'

export function TextComp() {
  return (
    <p className={styles.text}>
      Sample Text
    </p>
  )
}
```

## メディアクエリの変数を共有する

```variable.scss
$breakpoints: (
  'sm': 576px,
  'md': 768px,
  'lg': 992px,
  'xl': 1200px,
);

@mixin mq($size) {
  @media screen and (max-width: #{map-get($breakpoints, $size)}) {
    @content;
  }
}
```

```comp.module.scss
@import './variables';

.comp {
  background: #fff;

  // ↓768px以下で適用したいCSS
  @include mq(md) {
    background: #333;
  }
}
```

# 4.Tips

## import で相対パスを使わない

`next.config.js`の`saasOptions`を設定するといい
`includepath`に`styles`ディレクトリを追加する

```next.config.js
const path = require('path');
module.exports = {
  saasOptions: {
    includePath: [path.join(__dirname,'styles')],
  },
}
```

```comp.module.scss
// 相対パスを使わなくて良くなる
@import 'variables';

.comp {
  background: #fff;

  // ↓768px以下で適用したいCSS
  @include mq(md) {
    background: #333;
  }
}
```

### 参考

[Zenn > Next.js に CSS Modules を導入する](https://zenn.dev/catnose99/scraps/5e3d51d75113d3)
