---
title: リダイレクトされたフォルダーの最適化された移動を有効にします。
description: 新しいファイル共有にリダイレクトされたフォルダーの最適化の移動を実行する方法。
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 98fd5d50645ad454204dcf9dabf58e97c246ab1a
ms.sourcegitcommit: 505505b7ec99506e7ff50eddbdd6aa94a602abe6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2018
ms.locfileid: "3831382"
---
# リダイレクトされたフォルダーの最適化された移動を有効にします。

>適用対象: Windows 10、Windows 8、Windows 8.1、Windows Server 2012、Windows Server 2012 R2、Windows Server 2016

このトピックでは、新しいファイル共有にリダイレクトされたフォルダー (フォルダー リダイレクト) の最適化の移動を実行する方法について説明します。 任意の遅延が発生することがなくオフライン ファイルのローカル キャッシュで、キャッシュされたコンテンツの名前は、管理者は、リダイレクトされたフォルダーをホストしているファイル共有を移動し、リダイレクトされたフォルダーは、グループ ポリシーのターゲット パスを更新するとき、このポリシー設定を有効にした場合、またはユーザーのデータ損失の可能性です。

以前は、管理者が変更のグループ ポリシーや、クライアント コンピューターが影響を受けるユーザーの次回サインイン時、ファイルをコピーすることで、リダイレクトされたフォルダー ターゲット パス遅延サインインが原因です。 または、管理者は、ファイル共有の移動し、グループ ポリシーでリダイレクトされたフォルダーのターゲット パスを更新します。 ただし、移動後、移動の開始と最初の同期の間で、クライアント コンピューターにローカルで行われた変更は、失われます。

## 前提条件

最適化された移動では、次の要件があります。

- フォルダー リダイレクトは、セットアップである必要があります。 詳細については、[オフライン ファイルとフォルダー リダイレクトの展開](deploy-folder-redirection.md)を参照してください。
- クライアント コンピューターには、Windows 10、Windows 8.1、Windows 8、Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 を実行する必要があります。

## 手順 1: 最適化されたグループ ポリシーでの移動を有効にします。

フォルダー リダイレクト データの再配置を最適化するには、**有効にするには、フォルダー リダイレクト サーバーのパスの変更のオフライン ファイルのキャッシュに内容の移動が最適化されています。** ポリシー設定の適切なグループ ポリシー オブジェクト (GPO) を有効にするのにグループ ポリシーを使用します。 **無効**または**構成されていない**場合は、このポリシー設定を構成すると、クライアントがフォルダー リダイレクトのすべてのコンテンツを新しい場所にコピーし、サーバーのパスが変更された場合に元の場所からコンテンツを削除します。

リダイレクトされたフォルダーの最適化された移動を有効にする方法を以下に示します。

1. グループ ポリシーの管理] で (たとえば、**フォルダー リダイレクト、および移動ユーザー プロファイルの設定**)、フォルダー リダイレクト設定の作成および**編集**] を選択した GPO を右クリックします。
2. [**ユーザーの構成****ポリシー**]、 **[管理用テンプレート**]、**システム**、**フォルダー リダイレクト**を移動します。
3. **有効にするには、フォルダー リダイレクト サーバーのパスの変更のオフライン ファイルのキャッシュに内容の移動が最適化されています**が、右クリックし、**編集**します。
4. **Enabled**] を選択し、 **[ok]** を選択します。

## 手順 2: リダイレクトされたフォルダーのファイル共有を再配置します。

リダイレクトされたフォルダーをユーザーが含まれているファイル共有を移動して、インポート、フォルダーが適切に再配置するように注意することです。

>[!IMPORTANT]
>場合は、ユーザーのファイルには使用または移行で、完全なファイルの状態は保存されない場合、オフライン ファイル、またはデータの損失でもによって生成された同期の競合、ネットワーク経由でファイルがコピーされるユーザー エクスペリエンス パフォーマンスが低下可能性があります。

1. ユーザーに事前に通知、リダイレクトされたフォルダーをホストするサーバーは変更し、次の操作を実行することをお勧めします。

      - オフライン ファイルのキャッシュの内容を同期および競合を解決します。
      - 管理者特権のコマンド プロンプトを開き、 **GpUpdate/Target:User ファイル名**を入力しますとし、サインアウトしてもう一度サインインして、クライアント コンピューターを最新のグループ ポリシー設定が適用されることを確認します。

        >[!NOTE]
        >既定では、クライアント コンピューター グループ ポリシーを更新 90 分ごとに、ためクライアントの更新後のポリシーを受信するコンピューターに十分な時間を許可する場合は**GpUpdate**を使用するユーザーに確認する必要はありません。
2. ファイル共有内のファイルが使用中にないことを確認するサーバーからファイル共有を削除します。 これにはサーバー マネージャーで、ファイル サービスおよび記憶域サービスの**共有**のページで、適切なファイル共有を右クリックし、**削除**] を選択します。

    ユーザーは、オフライン移行が完了し、更新されたフォルダー リダイレクト設定グループ ポリシーから受信するまでにオフライン ファイルを使用して動作します。

3. バックアップ特権を持つアカウントを使用して、ファイル共有の内容をバックアップなど、ファイルのタイムスタンプを保持するメソッドを使用してファイルを新しい場所に移動し、ユーティリティを復元します。 **Robocopy**コマンドを使用して、管理者特権のコマンド プロンプトを開き、次のコマンドを入力する場所```<Source>```は、ファイル共有の現在の場所と```<Destination>```新しい場所には。

    ```PowerShell
    Robocopy /B <Source> <Destination> /Copyall /MIR /EFSRAW
    ```

    >[!NOTE]
    >**Xcopy**コマンドはすべてのファイルの状態を保持されません。
4. フォルダー リダイレクト ポリシー設定は、各リダイレクトされたフォルダーに移動するのには、ターゲット フォルダーの場所の更新を編集します。 詳しくは、[オフライン ファイルとフォルダー リダイレクトの展開](deploy-folder-redirection.md)の手順 4 を参照してください。
5. リダイレクトされたフォルダーをホストするサーバーが変更されているでもう一度サインインするには、更新された構成を取得し、適切なファイルの同期を再開して、 **GpUpdate/Target:User/Force**コマンドを使用し、サインアウトする必要がありますが、ユーザーを通知します。

    ユーザーする必要がありますサインインすべてのコンピューターに少なくとも 1 回データの取得各オフライン ファイルのキャッシュで正しく再配置することを確認します。

## 詳細

* [オフライン ファイルとフォルダーのリダイレクトを展開します。](deploy-folder-redirection.md)
* [移動ユーザー プロファイルを展開します。](deploy-roaming-user-profiles.md)
* [フォルダー リダイレクト、オフライン ファイル、および移動ユーザー プロファイルの概要](folder-redirection-rup-overview.md)