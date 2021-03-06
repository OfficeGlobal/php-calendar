# PHP 予定表 API のサンプル #

[日本 (日本語)](https://github.com/jasonjoh/php-calendar/blob/master/loc/readme-ja.md) (Japanese)

このサンプルでは、PHP から[予定表 API](https://msdn.microsoft.com/office/office365/APi/calendar-rest-operations) を使用する方法を示します。サンプル アプリは、架空のコミュニティ劇場のシェークスピア祭の「今後の公演」アプリです。ユーザーは、Office 365 アカウントに接続し、参加する公演について予定表にイベントを追加することができます。ユーザーには、友人を招待して、招待した友人それぞれに会議出席依頼を送信するオプションがあります。 

## 使用する API の機能 ##

- ユーザーの既定の予定表にイベントを作成する
- イベントに添付ファイルを追加する
- イベントに出席者を追加する
- [予定表ビュー](https://msdn.microsoft.com/office/office365/APi/calendar-rest-operations#GetCalendarView)を使用して、定期的なイベントを展開し、1 日のすべての予定を表示します。

## 必要なソフトウェア ##

- [PHP 5.6](http://php.net/downloads.php)
- PHP に対応可能な Web サーバー。

私のテストでは、Windows 8.1 ノート PC にインストールされている IIS 8 を使用しました。[Web Platform インストーラー](http://www.microsoft.com/web/downloads/platform.aspx) (Windows/IIS のみ) を使用して、PHP 5.6.0 をインストールしました。

## サンプルの実行 ##

開始する前に PHP がインストールされていること、および Web サーバーが処理用に構成され、サーバーの PHP ファイルが構成されていることが前提となっています。 

1. サンプル プロジェクトをダウンロードまたはフォークします。
1. Web のルート ディレクトリに、`php-calendar` という新しいディレクトリを作成します。リポジトリからのファイルをこのディレクトリにコピーします。
1. [Azure Active Directory にアプリを登録します](https://github.com/jasonjoh/office365-azure-guides/blob/master/RegisterAnAppInAzure.md)。アプリは、サインオン URL が `http://localhost/php-calendar` の Web アプリとして登録されている必要があります。また、\[ユーザーの予定表へのフル アクセス] のアクセス許可が付与されている必要があります。このアクセス許可は、\[代理アクセス許可] ドロップダウン リストから選択できます。
1. `.\o365\ClientReg.php` ファイルを編集します。 
	1. アプリの登録時に取得したアプリのクライアント ID をコピーし、`$clientId` 変数の値として貼り付けます。 
	1. アプリの登録時に作成したキーをコピーし、`$clientSecret` 変数の値として貼り付けます。
	1. ファイルを保存します。
1. 更新された CA 証明書を使用して SSL を検証するように PHP のインストールが構成されていない場合、サーバーで Fiddler を実行し、かつ `Office365Service.php` で変数 `$enableFiddler` を `true` に設定しない限り、要求は失敗します。別の方法として、`curl_exec` への呼び出しの直前に次の行を挿入することができます。**ただし、**これを行った場合、SSL 検証がすべて無効になる点に注意してください (運用環境では SSL 検証を無効にすべきではありません)。

    curl\_setopt($curl, CURLOPT\_SSL\_VERIFYPEER, 0);
1. Web ブラウザーを開き、`http://localhost/php-calendar/home.php` に移動します。
1. 今後のさまざまなシェークスピア演劇の上演時間が一覧表示されていることが分かります。いずれかの \[予定表に接続] ボタンをクリックすると、Office 365 にサインインします。
1. サインインすると、ホーム ページにリダイレクトされ、ボタンは \[予定表に追加] に変わります。 特定の上演時間の横にあるボタンをクリックすると、その時間が予定表に追加されます。\[はい] の \[伝票が必要] フィールドがあるイベントには、イベントの添付ファイルとして伝票が含まれています。

## 著作権 ##

Copyright (c) Microsoft.All rights reserved.

----------
Twitter ([@JasonJohMSFT](https://twitter.com/JasonJohMSFT)) でぜひフォローしてください。

[Exchange 開発ブログ](http://blogs.msdn.com/b/exchangedev/)をフォローする