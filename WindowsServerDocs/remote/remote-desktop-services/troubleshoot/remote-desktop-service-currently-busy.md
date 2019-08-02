---
title: 接続時に、リモート デスクトップ サービスは現在ビジー状態であるというメッセージをユーザーが受け取る
description: ユーザーがリモートデスクトップ接続を開始したときのリモート デスクトップ サービスは現在ビジー状態であるというエラーのトラブルシューティング。
audience: itpro
ms.custom: na
ms.reviewer: rklemen
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: troubleshooting
ms.assetid: ''
author: kaushika-msft
manager: ''
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 889fd83925081ac1dce386b1cd18fbef59586eb5
ms.sourcegitcommit: f6503e503d8f08ba8000db9c5eda890551d4db37
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/26/2019
ms.locfileid: "68529902"
---
# <a name="on-connecting-user-receives-remote-desktop-service-is-currently-busy-message"></a>接続時に、ユーザーが "Remote Desktop Service is currently busy" (リモート デスクトップ サービスは現在ビジー状態です) というメッセージを受け取る

この問題に対する適切な対応を見極めるには、次のことを確認してください。

- リモート デスクトップ サービスのサービスは、応答しなくなりますか (たとえば、リモート デスクトップ クライアントがようこそ画面で "ハング" しているように見える)。  
   - サービスが応答しなくなる場合は、「[RDSH サーバーのメモリの問題](#rdsh-server-memory-issue)」をご覧ください。
   - クライアントは通常どおりサービスとやり取りしているように見える場合は、次の手順に進みます。
- 1 人または複数のユーザーがリモート デスクトップ セッションを切断した場合、ユーザーは再び接続できますか。  
   - 何人のユーザーがセッションを切断しても引き続きサービスで接続が拒否される場合は、「[RD リスナーの問題](#rd-listener-issue)」をご覧ください。
   - 何人かのユーザーがセッションを切断すると、サービスでの接続の受け付けが始まる場合は、「[接続制限ポリシーを確認する](#check-the-connection-limit-policy)」をご覧ください。

## <a name="rdsh-server-memory-issue"></a>RDSH サーバーのメモリの問題

一部の Windows Server 2012 R2 RDSH サーバーでは、メモリ リークが検出されています。 時間の経過と共に、これらのサーバーでは、リモート デスクトップ接続とローカル コンソール サインインの両方が、次のようなメッセージで拒否されるようになります。

> リモート デスクトップ サービスが現在ビジー状態のため、実行しようとしている操作を完了できません。 しばらくたってからもう一度試してください。 他のユーザーはログオンできます。

また、接続しようとしているリモート デスクトップ クライアントは、応答しなくなります。

この問題を回避するには、RDSH サーバーを再起動します。

この問題を解決するには、KB 4093114、[2018 年 4 月 10 日 - KB4093114 (マンスリー ロールアップ)](https://support.microsoft.com/help/4093114/) を RDSH サーバーに適用します。

## <a name="rd-listener-issue"></a>RD リスナーの問題

Windows Server 2008 R2 から Windows Server 2012 R2 または Windows Server 2016 に直接アップグレードした一部の RDSH サーバーで問題が確認されています。 リモート デスクトップ クライアントが RDSH サーバーに接続すると、RDSH サーバーによってそのユーザー セッションに対する RD リスナーが作成されます。 影響を受けるサーバーでは RD リスナーのカウントが保持されており、ユーザーが接続すると増やされますが、減らされることはありません。

この問題に対しては、次の方法で対処できます。

  - RDSH サーバーを再起動して、RD リスナーのカウントをリセットします
  - 接続制限ポリシーを変更し、非常に大きな値に設定します。 接続制限ポリシーの管理について詳しくは、「[接続制限ポリシーを確認する](#check-the-connection-limit-policy)」をご覧ください。

この問題を解決するには、次の更新プログラムを RDSH サーバーに適用します。

  - Windows Server 2012 R2KB 4343891、[2018 年 8 月 30 日 — KB4343891 (マンスリー ロールアップのプレビュー)](https://support.microsoft.com/help/4343891/windows-81-update-kb4343891)
  - Windows Server 2016: KB 4343884、[2018 年 8 月 30 日 — KB4343884 (OS ビルド 14393.2457)](https://support.microsoft.com/help/4343884/windows-10-update-kb4343884)

## <a name="check-the-connection-limit-policy"></a>接続制限ポリシーを確認する

個々のコンピューター レベルで、またはグループ ポリシー オブジェクト (GPO) を構成することにより、同時リモート デスクトップ接続の数に制限を設定できます。 既定では、制限は設定されていません。

RDSH サーバーで現在の設定を確認し、既存の GPO を特定するには、管理者としてコマンド プロンプト ウィンドウを開き、次のコマンドを入力します。
  
```cmd
gpresult /H c:\gpresult.html
```
   
このコマンドの終了後、**gpresult.html** を開きます。 **[コンピューターの構成]\\[管理用テンプレート]\\[Windows コンポーネント]\\[リモート デスクトップ サービス]\\[リモート デスクトップ セッション ホスト]\\[接続]** で、 **[接続数を制限する]** ポリシーを見つけます。

  - このポリシーの設定が **[無効]** になっている場合、グループ ポリシーでは RDP 接続の数は制限されていません。
  - このポリシー設定が **[有効]** になっている場合は、 **[優勢な GPO]** を確認します。 接続の制限を削除または変更する必要がある場合は、この GPO を編集します。

ポリシーの変更を適用するには、影響を受けるコンピューターでコマンド プロンプト ウィンドウを開き、次のコマンドを入力します。
  
```cmd
gpupdate /force
```
  