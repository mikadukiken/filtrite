## filtrite-japanese
filtriteは[Bromite](https://www.bromite.org/)と[Cromite](https://www.cromite.org/)のフィルタリストを生成するプロジェクトです。 詳しくは[Custom Ad Block Filters](https://www.bromite.org/custom-filters)のページをご覧ください。

# Lists
表から任意のリストを選択し、名前を長押ししてリンクをコピーします。 設定＞AdBlock setting（Cromiteの場合はLegacy AdBlock setting）で「Filters URL」をコピーしたリンクに設定し、Bromiteに追加します。

| リンク | 説明  |
| ------ | ------|
| [Bromite Default](https://github.com/mikadukiken/filtrite-japanese/releases/latest/download/bromite-default.dat) | Bromite [デフォルトのフィルターリスト](https://github.com/bromite/filters)、ただしこのツールで生成されたもの。|
| [Bromite Extended](https://github.com/mikadukiken/filtrite-japanese/releases/latest/download/bromite-extended.dat) | デスクトップの[uBlock Origin](https://github.com/gorhill/uBlock)で使用している迷惑ブロック機能を追加したデフォルトリスト |
| [Bromite Extended (Soft)](https://github.com/xarantolus/filtrite/releases/latest/download/bromite-extended-soft.dat) | Same as the "Bromite Extended" list, but with less aggressive filtering (should break fewer sites) |
| [German](https://github.com/xarantolus/filtrite/releases/latest/download/german.dat) | The "Bromite Extended" list with additional region-specific blocklists for german sites |

あるいは、[このプロジェクトのフォークを検索するにはこちらへ](https://filterlists.010.one/) で、他の国のリストなどを検索することもできます。


これらのリストはGitHub Actionsを使って定期的に自動更新されます。

**Note**: 使用されているすべてのリスト形式が、[ルールセット生成ツール](https://github.com/xarantolus/subresource_filter_tools)によって実際にサポートされているかどうかは、100%確実ではありません(出力がいくつかの失敗を示しているため)。 もしそれについてコメントがあれば、issueを開いてください :)

### Advanced blocking
The normal Bromite ad blocking engine does not support all blocking formats. However, since the introduction of user scripts, it has become possible to block even more annoying elements. If you want more blockers (e.g. for cookie prompts), see my [custom Bromite user scripts repository](https://github.com/xarantolus/bromite-userscripts/).

### Using your own filter lists
This program is designed in a way that allows easily adding new lists.

To create a new list:

1. Fork this repository
2. Enable GitHub Actions by switching to the "Actions" tab of your repo, then confirming that you want to enable them
3. Choose a name for the list, e.g. in the following the name is `example-list`. Please note that the file name must end with `.txt`, so in our case we call it `example-list.txt` (put it in the `lists` directory).
4. Search for filter lists you want to use. You can for example find them [here](https://filterlists.com/), use those in "uBlock Origin" or "AdBlock Plus" format (however, it's possible that [not all types of rules are supported](https://github.com/bromite/bromite/wiki/AdBlocking)). Go to info, then "View" and copy the URL to the list.
5. Create a file `lists/example-list.txt` (in the `lists` directory) that contains the URLs to filter lists you copied before. It should look like this:
    ```
    # Lines starting with # are ignored, empty lines are also allowed
    # List one URL per line:
    https://easylist.to/easylist/easylist.txt
    https://...

    # The following line doesn't work, only put either a comment or an URL in one line, not both
    http://  # Invalid comment on URL
    ```
6. Save your file, commit and push. GitHub Actions should now build the list and create a release
7. After GitHub Actions generated the release, you can copy the linked URL in the release to always get the latest generated version. This URL looks something like `https://github.com/USERNAME/filtrite/releases/latest/download/FILENAME.dat`. If your URL (except for the username/filename part) contains numbers, you copied the wrong link.
8. Check that the generated filter file size is less than the allowed maximum of [20 MB](https://github.com/bromite/bromite/blob/6f40f8341ab3fbcab458c10fe7b6bbcb8f881404/build/patches/Bromite-subresource-adblocker.patch#L1160-L1161). If it isn't, you must remove some lists
9. Set this URL as the filter file in Bromite settings.

Another thing to note is that [GitHub disables scheduled workflows after 60 days](https://docs.github.com/en/actions/managing-workflow-runs/disabling-and-enabling-a-workflow), meaning that you sometimes have to commit something to keep your fork "alive".


### [License](LICENSE)
This is free as in freedom software. Do whatever you like with it.
