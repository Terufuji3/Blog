
#git

- [[obsidianの特定のディレクトリにあるmdのみをgithub pagesで公開する方法]]で使われていた

## なにそれ
- 親リポジトリのワーキングディレクトリ内に別の Git リポジトリを埋め込む仕組み
- 親リポジトリは「サブモジュールのリモートリポジトリのURLと特定のコミットID」のみを保存する
	- サブモジュール内のコミット履歴は親リポジトリの履歴には残らない

# submoduleを設定

- クローンしてくる
```
git submodule add リモートリポジトリのurlなど
```

- 親リポジトリで差分が出るのでコミットする

- 親リポジトリに記録されているサブモジュールのコミットIDに、サブモジュールを強制的にチェックアウトする
```
git submodule update
```


# submoduleを解除

## 参考
https://qiita.com/k_yamashita/items/040c04f8798d2384806e

## 手順
- `.git/config` からサブモジュールの設定を削除する
	- これによりgitから認識されなくなる
	- `git submodule deinit -f QuartzTest` 
		- エラー発生
			- `Deletion of directory 'QuartzTest' failed. Should I try again? (y/n) `
			- 試したこと
				- エクスプローラ, コンソールから対象ディレクトリを開いていない状態にする
				- obsidian gitで `update submodule` のチェックを外しobsidianを再起動
				- **vscodeで開いたままだった**
- サブモジュールをリポジトリから削除
	- `git rm -f QuartzTest`
- `.git/modules/` からサブモジュール情報を削除
	- `rm -rf .git/modules/QuartzTest`
		- windowsの場合はrmコマンドが使用できないのでエクスプローラから手動で削除


# submoduleを更新
- submodule のディレクトリに入り、参照したいブランチやコミットにチェックアウトする
- submodule の外側に戻り、その submodule の現在のコミットを記録する (指し示す先を変更する)
	- 普通に差分をコミットするだけで参照するコミットが更新される

## どこにサブモジュールのコミットIDが記録されるのか

A. [[Gitのtreeオブジェクト]]

コミットID確認コマンド
```
git ls-tree HEAD サブモジュール名
```

## 参考
https://qiita.com/sotarok/items/0d525e568a6088f6f6bb



