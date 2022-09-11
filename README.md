# Benchmark of caching dependencies

npm, yarn v1, yarn v3, pnpm
https://blog.maximeheckel.com/posts/guide-to-cicd-for-frontend-developers/


## TODO
Cacheのスコープを確認する?
https://zenn.dev/mallowlabs/articles/github-actions-cache-scope

Github Actionsの正規表現のパース方法がドキュメントと違う事例を見つけた気がする。
https://github.com/no-yan/cache-actions-compare/commit/a291a1ade2ceac468479f5fa7ead256e083cfa20
ドキュメントでは ** が / を含んだ文字にマッチするとなっているけれど、hashFiles関数では / が含まれていないようで、結果として正規表現にマッチしたファイルがないことになっている。

↑github actionsに報告する & next.jsにドキュメントの修正を依頼する
https://nextjs.org/docs/advanced-features/ci-build-caching#github-actions

swc関連でyarn installが失敗する件の原因を考える
[エラー](https://nextjs.org/docs/messages/failed-loading-swc)
M1でインストールしたものをx64で動かしているため失敗しているよう。
swcMinifyをオフ、.babelrcを追加でも失敗、next@canaryを入れても失敗、optionalDependenciesに@next/swc-linux-x64-gnuを入れても失敗
単にビルドの前に`yarn` でインストールすると、ビルドが失敗しなくなった。
`yarn` を `--immutable-cache` に変更すると失敗する。
https://github.com/no-yan/cache-actions-compare/runs/8293766938?check_suite_focus=true
