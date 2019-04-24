---
title: nfsshare
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 437a2615-335a-442f-9713-d50d5f3983a3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 50df88a3fddbceb1595f328bdd4e3c6f526e3a2c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881693"
---
# <a name="nfsshare"></a>nfsshare



使用する **nfsshare** Network File System (NFS) 共有コントロールにします。

## <a name="syntax"></a>構文

```
nfsshare <ShareName>=<Drive:Path> [-o <Option=value>...]
nfsshare {<ShareName> | <Drive>:<Path> | * } /delete
```

## <a name="description"></a>説明

引数を指定せず、 **nfsshare** コマンド ライン ユーティリティは、nfs サーバーによってエクスポートされたすべての Network File System (NFS) 共有を一覧表示します。 *ShareName* 唯一の引数として **nfsshare** で識別される、NFS 共有のプロパティを一覧表示 *ShareName*します。 ときに*ShareName*と*ドライブ ***:*** パス*提供される**nfsshare**で識別されるフォルダーにエクスポート*のドライブ ***:*** パス*として*ShareName*します。 ときに、 **/delete** オプションを使用すると、指定したフォルダーが不要になった利用 NFS クライアントです。

## <a name="options"></a>オプション

**Nfsshare** コマンドは次のオプションと引数。

|用語|定義|
|----|----------|
|-o anon {[はい] を = | No}|匿名 (マップされていない) ユーザーが共有ディレクトリにアクセスできるかどうかを指定します。 既定値は **ない**します。|
|-o rw[=\<Host>[:<Host>]...]|指定されたグループのホストまたはクライアントによって、共有ディレクトリに読み取り/書き込みアクセスを提供 *ホスト*します。 ホストとグループ名、コロンで区切ります (**:**)。 場合 *ホスト* が指定されていないすべてのホストとクライアント グループ (で指定された文字を除く、 **ro** オプション) 読み取り/書き込みアクセス権を持ちます。 どちらの場合、 **ro** も **rw** オプションが設定されている、すべてのクライアントが共有ディレクトリへの読み取り/書き込みアクセス権を持ちます。|
|-o ro [=\<ホスト > [:<Host>]...]|指定されたグループのホストまたはクライアントによって、共有ディレクトリに読み取り専用のアクセスを提供 *ホスト*します。 ホストとグループ名、コロンで区切ります (**:**)。 場合 *ホスト* が指定されていないすべてのクライアント (で指定された文字を除く、 **rw** オプション) 読み取り専用アクセスします。 場合、 **ro** オプションが 1 つまたは複数のクライアントの設定が、 **rw** で指定されたクライアントのみのオプションが設定されていない、 **ro** オプションは、共有ディレクトリへのアクセス権を持ちます。|
|-o encoding={big5|-euc-jp|euc-kr|-euc-tw|gb2312-80|ksc5601|シフト jis}|既定のエンコーディングのファイルとディレクトリ名に使用し、使用する場合は、次のいずれかに設定する必要を指定します。</br>-   **big5** (中国語)</br>-   **-euc-jp** (日本語)</br>-   **-euc-kr** (韓国語)</br>-   **-euc-tw** (中国語)</br>-   **gb2312 80** (簡体字中国語)</br>-   **ksc5601** (韓国語)</br>-   **シフト jis** (日本語)</br>オプションである場合は設定された場合、既定のエンコード方式は ANSI ではないか、既定のエンコード方式は、ロケールの英語以外のロケールで構成されているシステム。 指定されたロケールの既定のエンコード スキームを次に示します。</br>日本語。シフト JIS</br>-韓国語:KS_C_5601-1987</br>-簡体字中国語:GB2312-80</br>繁体字中国語:BIG5|
|-o anongid=\<gid>|共有ディレクトリを使用して、匿名 (マップされていない) ユーザーがアクセスすることを指定 *gid* グループ識別子 (GID) として。 既定値は-2 です。 匿名 GID は、匿名アクセスが無効になっている場合でも、マップされていないユーザーが所有するファイルの所有者をレポートするときに使用されます。|
|-o  anonuid=\<uid>|共有ディレクトリを使用して、匿名 (マップされていない) ユーザーがアクセスすることを指定 *uid* として、ユーザー識別子 (UID)。 既定値は-2 です。 匿名 UID は、匿名アクセスが無効になっている場合でも、マップされていないユーザーが所有するファイルの所有者をレポートするときに使用されます。|
|-o root[=\<Host>[:<Host>]...]|指定されたグループのホストまたはクライアントによって、共有ディレクトリにルート アクセスを提供 *ホスト*します。 ホストとグループ名、コロンで区切ります (**:**)。 場合 *ホスト* が指定されていない、すべてのクライアントは、ルート アクセス権を持ちます。 場合、 **ルート** オプションが設定されていない、クライアントには、共有ディレクトリへのルート アクセスはありません。|
|/delete|場合*ShareName*または*ドライブ ***:*** パス*指定すると、指定された共有を削除します。 場合は * 指定した場合、すべての NFS 共有を削除します。|

> [!NOTE]
> このコマンドの完全な構文を表示するには、コマンド プロンプトで次のように入力します。</br>> **nfsshare/でしょうか。**

##

[Services for Network File System コマンド リファレンス](services-for-network-file-system-command-reference.md)も参照してください