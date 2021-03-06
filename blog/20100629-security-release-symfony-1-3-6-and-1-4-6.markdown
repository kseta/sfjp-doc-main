セキュリティー リリース: symfony 1.3.6 と 1.4.6
===============================================

([原文リンク](http://www.symfony-project.org/blog/2010/06/29/security-release-symfony-1-3-6-and-1-4-6))

symfony 1.3と1.4 の新しいリリースが予定より早く用意されました。
これは昨日(訳者追記: 6/28)報告されたセキュリティーの脆弱性に対応するためです。
symfony 1.3と1.4 で稼働している全てのアプリケーションを、早急に最新版へアップグレードすることを強く推奨します。


セキュリティー フィックス
-------------------------

symfony 1.3と1.4 には、GETパラメーターを含むURL(例: `/feed?page=2`)でもレンダリングされたテンプレートをキャッシュする機能が追加されました。
これらのパラメーターはユニークなキャッシュのキーを生成するために利用されています。
そして、このユニークなキャッシュのキーはキャッシュされたファイルを保存するディレクトリ構造を生成するためにも利用されています。

これらのアプリケーションに入ってくるパラメーターに対して適切にクリーニング処理を行っていない場合は、ディレクトリ トラバーサルの危険性があります。たとえば、 `/feed?page=..`に対するレスポンスは実際よりも上層にあるキャッシュディレクトリに保存されてしまうでしょう。脆弱性を受けるかどうかはファイルのパーミッションがどのように指定されているかに依存します。また、`settings.yml` でキャッシュ機能を有効にしているアプリケーションが脆弱性の影響を受けます。

変更内容は[r30031](http://trac.symfony-project.org/changeset/30031)で確認できます。


アップグレード方法
------------------

Subversionでチェックアウトしている方は`switch`で最新バージョンにします:

    // symfony 1.3
    $ svn switch http://svn.symfony-project.com/tags/RELEASE_1_3_6

    // symfony 1.4
    $ svn switch http://svn.symfony-project.com/tags/RELEASE_1_4_6

PEARをご利用の方は`pear`コマンドからアップグレードします:

    // symfony 1.3
    $ pear upgrade symfony/symfony-1.3.6

    // symfony 1.4
    $ pear upgrade symfony/symfony-1.4.6


セキュリティー上の問題を連絡する方法
------------------------------------

既に記載していますが、セキュリティーに関連する問題点は直接Tracに書き込むよりは **security [at] symfony-project [dot] com** 宛連絡してください。そうすることで噂が広まる前にコアチームがレビューし対応することができるからです。
