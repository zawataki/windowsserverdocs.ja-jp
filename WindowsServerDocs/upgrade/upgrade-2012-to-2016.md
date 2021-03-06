---
title: Windows Server 2012 を Windows Server 2016 にアップグレードするMicrosoft Docs
description: インプレースアップグレードを実行して Windows Server 2012 から Windows Server 2016 に移行する方法について説明します。
ms.prod: windows server
ms.technology: server-general
ms.topic: upgrade
author: RobHindman
ms.author: robhind
ms.date: 09/16/2019
ms.openlocfilehash: 09c5a95e2ccd065f3ebbe551404064c39f803f2a
ms.sourcegitcommit: 27f0caf74e88781054250455c3c1adf06deb6234
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2019
ms.locfileid: "71124722"
---
# <a name="upgrade-windows-server-2012-to-windows-server-2016"></a>Windows Server 2012 を Windows Server 2016 にアップグレードする

サーバーをフラット化せずに、既に設定したものと同じハードウェアとすべてのサーバーの役割を維持する場合は、インプレースアップグレードを実行します。 インプレースアップグレードでは、設定、サーバーの役割、データをそのまま維持しながら、古いオペレーティングシステムから新しいオペレーティングシステムに移行することができます。 この記事では、Windows Server 2012 から Windows Server 2016 に移行する方法について説明します。

Windows Server 2019 にアップグレードするには、このトピックを最初に使用して、Windows Server 2016 にアップグレードした後、windows [server 2016 から Windows server 2019 にアップグレード](upgrade-2016-to-2019.md)します。

## <a name="before-you-begin-your-in-place-upgrade"></a>インプレースアップグレードを開始する前に

Windows Server のアップグレードを開始する前に、診断とトラブルシューティングのためにデバイスから情報を収集することをお勧めします。 この情報は、アップグレードが失敗した場合にのみ使用することを目的としているため、デバイスから取得できる場所に情報を保存しておく必要があります。

### <a name="to-collect-your-info"></a>情報を収集するには

1. コマンドプロンプトを開き、に`c:\Windows\system32`アクセスして、「 **systeminfo**」と入力します。

2. 生成されたシステム情報をデバイスのどこかにコピーして貼り付け、保存します。

3. コマンドプロンプトに「 **ipconfig/all** 」と入力し、結果の構成情報をコピーして、上記と同じ場所に貼り付けます。

4. レジストリエディターを開き、HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion hive に移動します。次に、Windows Server **Buildlabex** (バージョン) と**EditionID** (エディション) をコピーして、上記と同じ場所に貼り付けます。

Windows Server 関連のすべての情報を収集したら、オペレーティングシステム、アプリ、および仮想マシンをバックアップすることを強くお勧めします。 また、サーバーで現在実行されているすべての仮想マシンを**シャットダウン**、**クイックマイグレーション**、または**ライブマイグレーション**する必要があります。 インプレースアップグレード中に仮想マシンを実行することはできません。

## <a name="to-perform-the-upgrade"></a>アップグレードを実行するには

1. **Buildlabex**値に、Windows Server 2012 を実行していることが示されていることを確認します。

2. Windows Server 2016 セットアップメディアを見つけて、 **setup.exe**を選択します。

    ![Setup.exe ファイルが表示されているエクスプローラー](media/upgrade-2012-2016/setup-2016.png)

3. **[はい]** を選択して、セットアッププロセスを開始します。

    ![セットアップを開始するアクセス許可を要求するユーザーアカウント制御](media/upgrade-2012-2016/start-setup-uac-box.png)

4. Windows Server 2016 画面で、**今すぐインストール** を選択します。

5. インターネットに接続されているデバイスの場合は、 **[更新プログラムをダウンロードしてインストールする (推奨)]** を選択します。

    ![重要な Windows 更新プログラムを取得するためにオンラインにすることを選択する画面](media/upgrade-2012-2016/imp-updates-win-setup.png)

6. デバイスの構成が確認され、完了するのを待ってから **[次へ]** を選択します。

7. から Windows Server メディアを受信した配布チャネル (製品版、ボリュームライセンス、OEM、ODM など) とサーバーのライセンスに応じて、ライセンスキーを入力して続行するように求められる場合があります。

    ![プロダクトキーを入力できる画面](media/upgrade-2012-2016/enter-product-key.png)

8. インストールする Windows Server 2016 エディションを選択し、 **[次へ]** を選択します。

    ![インストールする Windows Server 2016 エディションを選択する画面](media/upgrade-2012-2016/select-os-edition.png)

9. 配布チャネル (、Retail、Volume License、OEM、ODM など) に基づいて、ライセンス契約の条項に同意するには、[**同意**する] を選択します。

    ![使用許諾契約書に同意する画面](media/upgrade-2012-2016/license-terms.png)

10. **[個人用ファイルとアプリを保持]** する を選択してインプレースアップグレードを選択し、 **[次へ]** を選択します。

    ![インストールの種類を選択する画面](media/upgrade-2012-2016/choose-install-upgrade.png)

11. アップグレードを推奨しないことを示すページが表示された場合は、無視して **[確認]** を選択できます。 クリーンインストールを求めるメッセージが表示されましたが、必須ではありません。

    ![アップグレードを実行するかどうかを確認するための [確認] ボタンを示す画面](media/upgrade-2012-2016/confirm-upgrade-process.png)

12. セットアップでは、 **[プログラムの追加と削除]** を使用して Microsoft Endpoint Protection を削除するように指示されます。

    この機能は、Windows 10 と互換性がありません。

13. セットアップによってデバイスが分析されると、 **[インストール]** を選択してアップグレードを続行するように求められます。

    ![アップグレードを開始する準備ができていることを示す画面](media/upgrade-2012-2016/ready-to-install.png)

    インプレースアップグレードが開始され、 **Windows のアップグレード**画面が進行状況と共に表示されます。 アップグレードが完了すると、サーバーが再起動します。

    ![アップグレードの進行状況を示す画面](media/upgrade-2012-2016/upgrading-windows-with-progress.png)

## <a name="after-your-upgrade-is-done"></a>アップグレードの完了後

アップグレードが完了したら、Windows Server 2016 へのアップグレードが正常に完了したことを確認する必要があります。

### <a name="to-make-sure-your-upgrade-was-successful"></a>アップグレードが成功したかどうかを確認するには

1. レジストリエディターを開き、HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion hive にアクセスして、 **ProductName**を表示します。 Windows server **2016 Datacenter**などの windows server 2016 のエディションが表示するはずです。

2. すべてのアプリケーションが実行されており、アプリケーションへのクライアント接続が正常に行われていることを確認します。

アップグレード中に問題が発生したと思われる場合は、 `%SystemRoot%\Panther` (通常は`C:\Windows\Panther`) ディレクトリをコピーして zip 形式にし、Microsoft サポートに問い合わせてください。

## <a name="next-steps"></a>次の手順

Windows Server 2016 から Windows Server 2019 に移行するには、もう一度アップグレードを実行します。 詳細な手順については、「 [Windows server 2016 を Windows server 2019 にアップグレードする](upgrade-2016-to-2019.md)」を参照してください。

## <a name="related-articles"></a>関連記事

- Windows Server 2016 の詳細と情報については、「 [Windows server 2016 の概要](https://docs.microsoft.com/windows-server/get-started/server-basics)」を参照してください。