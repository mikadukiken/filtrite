## filtrite-japanese
filtriteは[Bromite](https://www.bromite.org/)と[Cromite](https://www.cromite.org/)のフィルタリストを生成するプロジェクトです。 詳しくは[Custom Ad Block Filters](https://www.bromite.org/custom-filters)のページをご覧ください。　

# Lists
表から任意のリストを選択し、名前を長押ししてリンクをコピーします。 設定＞AdBlock setting（Cromiteの場合はLegacy AdBlock setting）で「Filters URL」をコピーしたリンクに設定し、Bromiteに追加します。

| リンク | 説明  |
| ------ | ------|
| [Bromite Default](https://github.com/mikadukiken/filtrite-japanese/releases/latest/download/bromite-default.dat) | Bromite [デフォルトのフィルターリスト](https://github.com/bromite/filters)、ただしこのツールで生成されたもの。|
| [Bromite Extended](https://github.com/mikadukiken/filtrite-japanese/releases/latest/download/bromite-extended.dat) | デスクトップの[uBlock Origin](https://github.com/gorhill/uBlock)で使用している迷惑ブロック機能を追加したデフォルトリストです。 |
| [Bromite Extended (Soft)](https://github.com/mikadukiken/filtrite-japanese/releases/latest/download/bromite-extended-soft.dat) | 「Bromite Extended」リストと同じですが、フィルタリングはそれほど強力ではありません（破損するサイトが少なくなります）。 |
| [German](https://github.com/mikadukiken/filtrite-japanese/releases/latest/download/german.dat) | Bromite Extendedリストに、ドイツのサイトの地域別ブロックリストが追加されています。 |
|[tamago](https://github.com/mikadukiken/filtrite-japanese/releases/latest/download/tamago.dat)|もちお様の[たまごフィルタ](https://raw.githubusercontent.com/eEIi0A5L/adblock_filter/master/tamago_filter.txt)をBromite用に変換したもの。|

あるいは、[このプロジェクトのフォークを検索するにはこちらへ](https://filterlists.010.one/) で、他の国のリストなどを検索することもできます。


これらのリストはGitHub Actionsを使って定期的に自動更新されます。

**Note**: 使用されているすべてのリスト形式が、[ルールセット生成ツール](https://github.com/xarantolus/subresource_filter_tools)によって実際にサポートされているかどうかは、100%確実ではありません(出力がいくつかの失敗を示しているため)。 もしそれについてコメントがあれば、issueを開いてください :)


### Advanced blocking
通常のBromite広告ブロックエンジンは、すべてのブロック形式をサポートしているわけではありません。 しかし、ユーザースクリプトの導入により、より多くの煩わしい要素をブロックすることが可能になりました。 より多くのブロッカー（例えば、クッキープロンプト用）が必要な場合は、こちらの[カスタムBromiteユーザースクリプトリポジトリ](https://github.com/xarantolus/bromite-userscripts/)を参照してください。

### Using your own filter lists
このプログラムは、新しいリストを簡単に追加できるように設計されています。

新しいリストを作成するには

1. このリポジトリをフォークする
2. GitHubアクションを有効にするには、リポジトリの "Actions "タブに切り替えて、有効にすることを確認します。
3. リストの名前を決めてください。例えば、以下の例では `example-list` とします。 ファイル名の末尾は `.txt` でなければならないので、ここでは `example-list.txt` とする（`lists` ディレクトリに置く）。
4. 使用したいフィルターリストを検索してください。 例えば、[ここで](https://filterlists.com/)、"uBlock Origin "または "AdBlock Plus "形式のものを使用することができます（ただし、[すべてのタイプのルールがサポートされていない](https://github.com/bromite/bromite/wiki/AdBlocking)可能性があります）。 情報]→[表示]で、URLをリストにコピーする。
5. ファイル`lists/example-list.txt`（`lists`ディレクトリ内）を作成し、その中に先ほどコピーしたフィルターリストのURLを入れます。 以下のようにする：
    ```
    # Lines starting with # are ignored, empty lines are also allowed
    # List one URL per line:
    https://easylist.to/easylist/easylist.txt
    https://...

    # The following line doesn't work, only put either a comment or an URL in one line, not both
    http://  # Invalid comment on URL
    ```
6. ファイルを保存し、コミットしてプッシュします。 GitHub Actions がリストを作成し、リリースを作成します。
7. GitHub Actions がリリースを生成したら、そのリリースにあるリンク先の URL をコピーすれば、生成された最新版を常に入手することができます。 このURLは `https://github.com/USERNAME/filtrite/releases/latest/download/FILENAME.dat` のようになります。 URL（ユーザー名/ファイル名の部分を除く）に数字が含まれている場合は、間違ったリンクをコピーしています。
8. 生成されたフィルターファイルのサイズが、許可された最大値[20MB](https://github.com/bromite/bromite/blob/6f40f8341ab3fbcab458c10fe7b6bbcb8f881404/build/patches/Bromite-subresource-adblocker.patch#L1160-L1161)未満であることを確認してください。 もしそうでなければ、いくつかのリストを削除する必要があります。
9. Bromiteの設定で、このURLをフィルターファイルとして設定します。

もう一つ注意すべきことは、[GitHubは60日を過ぎるとスケジュールされたワークフローを無効にする](https://docs.github.com/en/actions/managing-workflow-runs/disabling-and-enabling-a-workflow)こと。つまり、フォークを「生かす」ために何かをコミットしなければならないことがあります。


### [License](LICENSE)
これはフリーソフトのように自由です。 好きなように使ってください。

### AdGuardフィルタのライセンス
GNU General Public License v3.0に基づき使用しています。
https://github.com/AdguardTeam/AdguardFilters/blob/master/LICENSE
