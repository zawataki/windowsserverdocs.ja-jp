---
title: Android でリモート デスクトップを概要します。
description: Basic では、Android のリモート デスクトップ クライアントの手順を設定します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 64f038e1-40ec-4c67-938b-72edea49e5d8
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 07/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: 42b4b4ffb73bd9d5d1397d32bd36c41d7e404dd7
ms.sourcegitcommit: d3f73936160505a40633ad8dd5931ac5fe3eccdb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297431"
---
# Android でリモート デスクトップを概要します。

>適用対象: Windows 10、Windows 8.1、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2

Android のリモート デスクトップ クライアントを使用して、Android デバイスから直接 Windows アプリとデスクトップを操作することができます。

開始するのには、次の情報を使用します。 必ずご質問がある場合は、[よく寄せられる質問](remote-desktop-client-faq.md)を確認してください。

> [!NOTE]
> - Android クライアントの新しいリリースについて知りたがっていますか。 チェック アウト[Android でリモート デスクトップの新機能では何ですか?](android-whatsnew.md)
> さらにインストールされている ChromeOS 53 と chromebook に関する資料 Android 4.1 と新しいデバイスでクライアントを実行することができます。 Chrome で Android のアプリケーションについて詳しく[は、ここ](https://sites.google.com/a/chromium.org/dev/chromium-os/chrome-os-systems-supporting-android-apps)です。

## RD クライアントを取得し、使用を開始

Android デバイスでリモート デスクトップを開始するこれらの手順に従います。

1. [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android)からリモート デスクトップ クライアントをダウンロードします。 
2. [リモート接続を受け入れるように、PC を設定](remote-desktop-allow-access.md)します。
3. リモート デスクトップ接続またはリモートのリソースを追加します。 仮想デスクトップの公開、オンプレミスまたは RemoteApp プログラム、セッション ベースのデスクトップを使用するには、Windows PC とリモートのリソースに直接接続する接続を使用します。 
4. ウィジェットを作成して、迅速にリモート デスクトップを表示するようにします。

> [!NOTE]
> フライトの以前の新機能するには、Google Play ストアからアプリケーションでは[Microsoft リモート デスクトップ ベータ版](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android.beta)をダウンロードすることをお勧めします。 

### リモート デスクトップ接続を追加します。

リモート デスクトップ接続を作成します。

1. 接続センター タップで**+**、**デスクトップ**をタップします。
2. 接続先コンピューターの次の情報を入力します。
  - [ **PC の名前**]: コンピューターの名前。 Windows コンピューター名、インターネット ドメイン名、または IP アドレスを指定できます。 PC の名前 (たとえば、 **MyDesktop:3389**または**10.0.0.1:3389**) をポート情報を追加することもできます。
  - [**ユーザー名**]: を使用して、リモート PC にアクセスするユーザー名。 次の形式を使用することができます。*ユーザー名*、 *domain \user_name*、または*user_name@domain.com*します。 ユーザー名とパスワードの入力を求めるかどうかを指定することもできます。
3. 次の追加オプションを設定することもできます。
  - [**フレンドリ名**]: な覚えやすい名前を PC に接続しています。 任意の文字列を使用することができますが、フレンドリ名を指定しない場合、PC の名前が表示されます。
  - **ゲートウェイ**– 仮想デスクトップ、RemoteApp プログラム、および内部の企業ネットワーク上のセッション ベースのデスクトップへの接続に使用するリモート デスクトップ ゲートウェイです。 システム管理者からゲートウェイに関する情報を取得します。
    リモート デスクトップ ゲートウェイを構成する必要があるかどうか。
  - **サウンド**: リモート セッション中にオーディオを使用するには、デバイスを選択します。 ローカルのデバイスでは、リモート デバイスまたはすべてではなく、サウンドを再生することができます。
  - **カスタマイズ画面の解像度**でこの設定を有効にすると接続のカスタムの解像度を設定します。 解像度をオフが適用されると、アプリのグローバル設定が定義されています。
  - **スワップ マウス ボタン**– マウスの右ボタン、マウスの左ボタンの機能を交換するには、このオプションを使用します。 (これは特に便利です左利きのユーザーのリモート PC が構成されているが、右手によるマウスを使用する場合)。
  - **管理者セッションへの接続**- Windows server を管理するためには、コンソール セッションに接続するには、このオプションを使います。
  - **ローカル ストレージをリダイレクト**– リモート PC でリモート システム ファイルとして、ローカル記憶域をマウントします。
4. **保存**] をタップします。

これらの設定を編集する必要があるかどうか。 デスクトップの名の横にオーバーフロー メニュー (**.** タップして、**編集**します。

接続を削除するかどうか。 ここでも、オーバーフロー メニュー (**.**、タップして、**削除**します。

>[!TIP]
> 0xf07 エラーが発生する場合 (「できませんでした接続リモート PC へのユーザー アカウントに関連付けられているパスワードの有効期限が切れたため」)、不正なパスワードは、パスワードを変更して再試行します。

### リモート リソースを追加します。
リモートのリソースは、RemoteApp プログラム、セッション ベースのデスクトップおよび公開 RemoteApp とデスクトップ接続を使用して仮想デスクトップです。

リモートのリソースを追加します。

1. [接続センター画面で、タップ**+**、し、**リモートのリソースのフィード**をタップします。 
2. リモートのリソースの情報を入力します。
   - **メールまたは URL**の RD Web アクセス サーバーの URL。 クライアントがメール アドレスに関連付けられている RD Web アクセスのサーバーを検索するように指示 – このフィールドで、会社のメール アカウントを入力することもできます。
   - **ユーザー名**- に接続している RD Web アクセスのサーバーに使用するユーザー名です。
   - **パスワード**の RD Web アクセス サーバーに接続するのに使用するパスワードです。
3. **保存**] をタップします。

リモートのリソースが接続センターで表示されます。


リモート リソースを削除するには。

1. 接続センターで、リモートのリソースの横にあるオーバーフロー メニュー (**.** をタップします。
2. **削除**をタップします。
3. 削除を確認します。

### ウィジェット – ホーム画面に保存されているデスクトップ暗証番号 (pin)

リモート デスクトップ アプリケーションでは、Android ウィジェット機能を使用して、ホーム画面にピン留めの接続をサポートします。 ウィジェットを追加する方法は、Android デバイスを使用しているとそのオペレーティング システムの種類によって異なります。 ウィジェットを追加する最も一般的な方法を次に示します。 

1. アプリのメニューを起動する**アプリ**をタップします。
2. **ウィジェット**をタップします。
3. ウィジェットのスワイプし、説明、「暗証番号 (pin) リモート デスクトップ」でリモート デスクトップのアイコンを探します
4. タップし、そのリモート デスクトップのウィジェットを保持し、ホーム画面に移動します。
5. アイコンを離すと、保存済みのリモート デスクトップが表示されます。 ホーム画面に保存する接続を選択します。

今すぐタップすることにより、ホーム画面から直接、リモート デスクトップ接続を開始できます。

> [!NOTE]
> リモート デスクトップ アプリケーションでデスクトップの接続の名前を変更する場合、このピン留めしたリモート デスクトップのラベルは更新されません。

## 内部資産へのアクセスの RD ゲートウェイへの接続します。

リモート デスクトップ ゲートウェイ (RD ゲートウェイ) では、どこからでも、企業ネットワーク上のリモート コンピューターに接続できます。 インターネット上します。 作成して、リモート デスクトップ クライアントを使用して、ゲートウェイを管理することができます。

新しいゲートウェイを設定します。

1. 接続センターで、**設定 _gt ゲートウェイ**をタップします。 タップ**+** 新しいゲートウェイを追加します。
2. 次の情報を入力します。
  - [**サーバー名**]: ゲートウェイとして使用するコンピューターの名前。 Windows コンピューター名、インターネット ドメイン名、または IP アドレスを指定できます。 サーバー名にポート情報を追加することもできます (例: **RDGateway:443**または**10.0.0.1:443**)。
  - **ユーザー名**- ユーザー名とパスワードを接続しているリモート デスクトップ ゲートウェイを使用します。 リモート デスクトップ接続用に使用されるものと同じ資格情報を使用する**デスクトップのユーザー アカウントの使用**を選択することもできます。

## ユーザー アカウントを管理します。

デスクトップまたはリモートのリソースに接続するときは、もう一度から選択するユーザー アカウントを保存できます。 デスクトップに接続するときに、ユーザーのデータを保存するのではなく、クライアント自体でユーザー アカウントを定義することもできます。

新しいユーザー アカウントを作成します。

1. 接続センターで、**設定**をタップし、**ユーザー アカウント**の順にタップします。
2. タップ**+** を新しいユーザー アカウントを追加します。
3. 次の情報を入力します。
   - **ユーザー名**- 使用したリモート接続を保存するユーザーの名前です。 次の形式で入力したユーザー名: ユーザー名、domain \user_name、または user_name@domain.com します。
   - **パスワード**の指定したユーザーのパスワードです。 リモート接続を使用するを保存するすべてのユーザー アカウントには、それに関連付けられているパスワードが必要です。
4. **保存**] をタップします。

ユーザー アカウントを削除します。

1. 接続センターで、 **_gt ユーザー アカウントの設定**をタップします。
2. タップして選択をリストで、ユーザー アカウントを保持します。 複数のユーザーを選択することができます。
3. 選択したユーザーを削除するごみ箱] をタップします。

## リモート デスクトップ セッションを移動します。
リモート デスクトップ接続を開始するときは、セッションの移動に使用できる利用可能なツールがあります。

### リモート デスクトップ接続を開始します。

1. セッションを開始するリモート デスクトップ接続をタップします。 
2. リモート デスクトップの証明書を確認するメッセージが表示されたら、**接続**] をタップします。 **このコンピューターへの接続をもう一度通知しない**を常に証明書を受け入れるを選択することもできます。

### グローバル アプリ設定を管理します。

Android クライアントでは、次のグローバル設定を設定できます。

- **デスクトップのプレビューを表示する**に接続する前に、接続センターでデスクトップのプレビューを表示することができます。 既定では、これが**上**に設定します。
- **ズームにピンチ**-、ピンチによるズーム ジェスチャを使用することができます。 リモート デスクトップを使用しているアプリ (Windows 8 で導入) マルチタッチをサポートする場合は、この設定を有効にする**オフ**です。
- **リモート デスクトップを向上させるために役立つ**- Microsoft に匿名データを送信します。 クライアントを向上させるためにこのデータを使用します。 この匿名のプライベート データを処理する方法について詳しくは、[リモート デスクトップ クライアントのプライバシーに関する声明](https://www.microsoft.com/privacystatement/RemoteApp/Default.aspx)を表示できます。 既定では、この設定が**オン**です。
- **表示**のディスプレイの 2 つのグローバル設定があります。
   - **向き**は、セッションの推奨される向き (横または縦向き優先) を設定します。 
   >[!NOTE]
   > Windows 8 または Windows の以前のバージョンを実行している PC に接続する場合は、セッションが正しくスケーリングされません。 最善の方法では、PC から切断し、使用する方向に再接続します。 さらに向上のオプションは、少なくともに PC をアップグレードする Windows 8.1 します。

   - **解像度**では、グローバルにデスクトップの接続に使用する解像度を設定します。 個々 のアプリまたは接続のカスタムの解像度を既に設定した場合にこの設定は変更されません。
   >[!NOTE]
   >ディスプレイの設定のいずれかを変更すると、のみに適用される新しい接続そのポイントからにします。 既に切断し、もう一度接続に接続しているセッションの変更を確認します。

### 接続バー

接続バーは、追加のナビゲーション コントロールへのアクセスを提供します。 既定では、接続バーは、画面の上部に中央に配置されます。 ダブル タップし、左または右に移動する、バーをドラッグします。

- **パン コントロール**: パン コントロールにより、画面拡大し、移動します。 パンのコントロールは、直接タッチを使って利用可能なだけことに注意してください。
   - 有効にする/パン コントロールを無効にする: パン コントロールを表示し、画面のズーム接続バーでパン アイコンをタップします。 コントロールを非表示にして、画面に戻るにその元の解像度をもう一度接続バーでパン アイコンをタップします。
   - パンのコントロールを使用: タップを押したままパンを制御し、画面を移動する方向にドラッグします。
   - パン コントロールに移動: ダブルタップ、画面上のコントロールを移動するパン コントロールを長押しします。
- **その他のオプション**: セッションの選択バーとコマンド バーの (下記参照) を表示する追加のオプションのアイコンをタップします。
- **キーボード**: キーボードを表示または非表示にキーボードのアイコンをタップします。 パン コントロールは、キーボードが表示されると自動的に表示されます。
- **接続バーを移動**: タップや長は接続バーと、ドラッグ アンド ドロップ、画面の上部に新しい場所にします。


### コマンド バー

画面の右側にあるコマンド バーを表示する接続バーをタップします。 (直接タッチとマウス ポインター) マウス モードを切り替えることができます。 コマンド バーから接続センターに戻るには、[ホーム] ボタンを使用します。 また、同じ操作の"戻る"ボタンを使用できます。 アクティブなセッションは切断できません。 


### 使用して直接タッチ ジェスチャやマウス モードをリモート セッションで

クライアントは、標準的なタッチ ジェスチャを使用します。 リモート デスクトップ上のマウス操作に対応するのにタッチ ジェスチャを使用することもできます。 利用可能なマウス モードは、次の表で定義されます。

> [!NOTE]
> Windows 8 と対話またはそれ以降は、ネイティブのタッチ ジェスチャが直接タッチ モードでサポートされます。 

| マウス モード    | マウス操作      | ジェスチャ                                                               |
|---------------|----------------------|-----------------------------------------------------------------------|
| 直接タッチ  | 左クリックします。           | 1 本指でタップ                                                          |
| 直接タッチ  | 右クリック          | 1 本指でタップと保留                                                 |
| マウス ポインター | ズーム                 | 2 本の指を使用し、ピンチ拡大または縮小表示のため離れて本の指を移動します。 |
| マウス ポインター | 左クリックします。           | 1 本指でタップ                                                          |
| マウス ポインター | 左クリックしてドラッグ  | 1 本の指ダブルタップを押したまま、ドラッグします。                               |
| マウス ポインター | 右クリック          | 2 本指でタップ                                                          |
| マウス ポインター | 右クリックしてドラッグ | 2 本の指ダブルタップを押したまま、ドラッグします。                               |
| マウス ポインター | マウス ホイール          | 2 本指でタップし、長押しすると、ドラッグして、上または下                           |

> [!TIP]
> 意見やご質問では、ようこそ常にします。 ただし、コメント機能を使用して、この記事の最後に、ヘルプをトラブルシューティングするための要求がしてください投稿は実行できません。 代わりに、[リモート デスクトップ クライアントのフォーラム](https://social.technet.microsoft.com/forums/windowsserver/en-us/home?forum=winrdc)に移動し、新しいスレッドを開始します。 機能のご意見があるかどうか。 [クライアント ユーザーの音声フォーラム](https://remotedesktop.uservoice.com/forums/272085-remote-desktop-for-android)で聞かせください。