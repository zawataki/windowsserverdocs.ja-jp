---
ms.assetid: aac117a7-aa7a-4322-96ae-e3cc22ada036
title: RID 発行の管理
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 49798f785fe02b5a97fd8bd979c327b86c9ddef2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874223"
---
# <a name="managing-rid-issuance"></a>RID 発行の管理

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、RID マスターの FSMO 役割の変更について説明します。RID マスターの発行と監視に関する新機能や、RID 発行を分析およびトラブルシューティングする方法などが含まれます。  
  
-   [RID 発行の管理](../../ad-ds/manage/Managing-RID-Issuance.md#BKMK_Manage)  
  
-   [RID 発行のトラブルシューティング](../../ad-ds/manage/Managing-RID-Issuance.md#BKMK_Tshoot)  
  
詳細については、 [AskDS ブログ](http://blogs.technet.com/b/askds/archive/2012/08/10/managing-rid-issuance-in-windows-server-2012.aspx)します。  
  
## <a name="BKMK_Manage"></a>RID 発行の管理  
既定で、1 つのドメインには、ユーザー、グループ、コンピューターなど、約 10 億個分のセキュリティ プリンシパルの容量があります。 当然ですが、それだけ多くのアクティブに使用されるオブジェクトを含むドメインなどありません。 しかし、Microsoft カスタマー サポートは、次のような事例を見つけました。  
  
-   ソフトウェアや管理用スクリプトのプロビジョニングによって、ユーザー、グループ、およびコンピューターが誤って一括作成された。  
  
-   多くの使用されないセキュリティ グループと配布グループが、委任されたユーザーによって作成された。  
  
-   多くのドメイン コントローラーが降格、復元、またはメタデータ消去された。  
  
-   フォレストの回復が実行された。  
  
-   InvalidateRidPool 操作が頻繁に実行された。  
  
-   RID ブロック サイズのレジストリ値が不適切に増加された。  
  
このような状況では例外なく RID が不必要に使い果たされ、しかも多くの場合が操作ミスによるものです。 過去において、環境で RID が枯渇した事例は数件あり、その場合は新しいドメインへの移行またはフォレスト回復の実行を余儀なくされました。  
  
Windows Server 2012 では、Active Directory の稼働日数と偏在性に関して最近問題になってきた、RID 割り当ての問題に対処しています。 これらには、イベント ロギングの向上より適切な制限、およびドメインのグローバル RID 空間の全体サイズを 2 倍にする機能、緊急時におけるが含まれます。  
  
### <a name="periodic-consumption-warnings"></a>RID 消費に関する定期的な警告  
Windows Server 2012 には、主要マイルストーンを超えると初期警告を出す、グローバル RID 空間のイベント追跡機能が追加されています。 このモデルでは、グローバル プール内の 10% の使用済みマークが計算され、それに達するとイベントがログに記録されます。 次に、残りの空間の次の 10% が計算され、同様にイベント サイクルが続けられます。 グローバル RID 空間が少なくなるにつれて、減少するプール内での 10% 到達が速まるので、イベントは加速します (ただし、イベント ログ ダンペングによってエントリは 1 時間につき 1 個に制限されます)。 すべてのドメイン コントローラー上のシステム イベント ログは、Directory-Services-SAM 警告イベント 16658 を書き込みます。  
  
既定の 30 ビット グローバル RID 空間を前提とすると、107,374,182<sup></sup> 番目の RID を含むプールを割り当てるときに最初のイベントがログに記録されます。 イベント レートは最後のチェックポイントである 100,000 まで自然に加速し、全部で 110 個のイベントが生成されます。 この動作はロック解除された 31 ビット グローバル RID 空間の場合に似ています。214,748,365 で始まり、117 個のイベントで終わります。  
  
> [!IMPORTANT]  
> このイベントは想定されていません。ドメイン内のユーザー、コンピューター、およびグループの作成プロセスをすぐに調査してください。 1 億個を超える AD DS オブジェクトを作成することは、通常では考えられません。  
  
![RID の発行](media/Managing-RID-Issuance/ADDS_RID_TR_EventWaypoints2.png)  
  
### <a name="rid-pool-invalidation-events"></a>RID プール無効化のイベント  
ローカルの DC RID プールが破棄されたという新しいイベント警告があります。 そのような警告は情報提供を目的としており、特に、新しい VDC 機能が原因で発生することは想定の範囲内です。 イベントの詳細については、後半にあるイベントの一覧を参照してください。  
  
### <a name="BKMK_RIDBlockMaxSize"></a>RID ブロック サイズの制限  
通常、ドメイン コントローラーは RID の割り当て要求を一度に 500 個のブロックで行います。 この既定値を上書きするには、ドメイン コントローラーで次の REG_DWORD レジストリ値を使用します。  
  
```  
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\RID Values  
RID Block Size  
  
```  
  
Windows Server 2012 より前のバージョンでは、暗黙的な DWORD 最大値 (0xffffffff または 4294967295 の値) を除き、このレジストリ キーで適用される最大値はありませんでした。 この値はグローバル RID 空間の合計よりかなり大きくなっています。 管理者が、不適切に、または誤って、グローバル RID が莫大なレートで枯渇するような値を使って RID ブロック サイズを構成することはときどきありました。  
  
Windows Server 2012 では、このレジストリ値に 10 進の 15,000 (16 進の 0x3A98) を超える値を設定することはできません。 これにより、意図しない莫大な RID 割り当てを防ぐことができます。  
  
15,000 *を超える値を設定した場合*、その値は 15,000 として扱われ、値が修正されるまで、ドメイン コントローラーの再起動ごとにディレクトリ サービス イベント ログにイベント 16653 が記録されます。  
  
### <a name="BKMK_GlobalRidSpaceUnlock"></a>グローバル RID 空間サイズのロックを解除します。  
Windows Server 2012 より前のバージョンでは、グローバル RID 空間は合計で 2<sup>30</sup> (つまり 1,073,741,823) 個の RID に制限されていました。 この制限に達した場合は、ドメインを移行するか、古いタイムフレームにフォレストを回復することによってのみ、新しい SID の作成が可能でした。これは、どう考えても障害回復です。 Windows Server 2012 以降では、グローバル プールを 2,147,483,648 個の RID に増やすために、2<sup>31</sup> ビットをロック解除できます。  
  
この設定は AD DS によって、すべてのドメイン コントローラーの RootDSE コンテキストにある **SidCompatibilityVersion** と呼ばれる特殊な非表示属性に格納されます。 この属性は ADSIEdit や LDP などのツールでは判読できません。 グローバル RID 空間の増加を確認するには、システム イベント ログに Directory-Services-SAM からの警告イベント 16655 の有無を調べるか、次の Dcdiag コマンドを使用します。  
  
```  
Dcdiag.exe /TEST:RidManager /v | find /i "Available RID Pool for the Domain"  
  
```  
  
グローバル RID プールを増やすと、利用できるプールは既定の 1,073,741,823 から 2,147,483,647 に変化します。 次に、例を示します。  
  
![RID の発行](media/Managing-RID-Issuance/ADDS_RID_TR_Dcdiag.png)  
  
> [!WARNING]  
> このロック解除は、 RID *の枯渇を防ぐ目的でのみ使用します*。また、RID シーリングの適用 (次のセクションを参照）*との組み合わせでのみ使用します*。 RID の残数が数百万個あり、使用増加率も低い環境では、ロック解除を "事前対策として" 設定しないでください。ロック解除した RID プールから生成される SID との間にアプリケーション互換性の問題が存在する可能性があるためです。  
>   
> このロック解除操作は、フォレストを前のバックアップに完全に回復させる場合を除き、元に戻したり、削除したりすることはできません。  
  
#### <a name="important-caveats"></a>重要な注意事項  
Windows Server 2003 と Windows Server 2008 ドメイン コントローラーは、グローバル RID プールの 31<sup></sup> 番ビットがロック解除されているとき、RID を発行できません。 Windows Server 2008 R2 ドメイン コント ローラー*できます*31 を使用して、<sup>st</sup>ビットの Rid*場合にのみ*修正プログラムがある[サポート技術情報 2642658](https://support.microsoft.com/kb/2642658)をインストールします。 サポートされていない、および修正プログラムが適用されていないドメイン コントローラーは、ロック解除するとグローバル RID プールを枯渇していると見なします。  
  
この機能はドメインのどの機能レベルでも強制されません。Windows Server 2012 または更新された Windows Server 2008 R2 のドメイン コントローラーだけがドメイン内に存在することに注意してください。  
  
#### <a name="implementing-unlocked-global-rid-space"></a>ロック解除されたグローバル RID 空間の実装  
<sup>  </sup>RID シーリングの警告 (下記を参照) を受け取った後に RID プールの 31 番ビットをロック解除するには、次の手順を実行します。  
  
1.  Windows Server 2012 ドメイン コントローラーで RID マスターの役割が実行されていることを確認します。 実行されていない場合は、それを Windows Server 2012 ドメイン コントローラーに転送します。  
  
2.  LDP.exe を実行します。  
  
3.  **[接続]** メニューをクリックし、ポート 389 上の Windows Server 2012 RID マスターの役割について **[接続]** をクリックします。次に、ドメイン管理者として **[バインド]** をクリックします。  
  
4.  **[参照]** メニューの **[変更]** をクリックします。  
  
5.  **[DN]** が空であることを確認します。  
  
6.  **[エントリ属性の編集]** に、次のように入力します。  
  
    ```  
    SidCompatibilityVersion  
    ```  
  
7.  **[値]** に、次のように入力します。  
  
    ```  
    1  
    ```  
  
8.  **[操作]** で **[追加]** が選択されていることを確認し、**[入力]** をクリックします。 これによって **[エントリ一覧]** が更新されます。  
  
9. **[同期]** チェック ボックスと **[拡張]** チェック ボックスをオンにして、**[実行]** をクリックします。  
  
    ![RID の発行](media/Managing-RID-Issuance/ADDS_RID_TR_LDPModify.png)  
  
10. 操作に成功すると、LDP 出力ウィンドウが表示されます。  
  
    ```  
    ***Call Modify...  
     ldap_modify_ext_s(Id, '(null)',[1] attrs, SvrCtrls, ClntCtrls);  
    modified "".  
  
    ```  
  
    ![RID の発行](media/Managing-RID-Issuance/ADDS_RID_TR_LDPModifySuccess.png)  
  
11. そのドメイン コントローラーの Directory-Services-SAM 情報イベント 16655 を調べて、グローバル RID プールが増えていることを確認します。  
  
### <a name="rid-ceiling-enforcement"></a>RID シーリングの適用  
保護措置を提供し、管理意識を高めるため、Windows Server 2012 では、グローバル RID 範囲に対する人為的シーリングが導入され、その値をグローバル空間内の RID 残数の 10% としています。 人工的シーリングの 1% 以内にあるとき、RID プールを要求しているドメイン コントローラーは Directory-Services-SAM 警告イベント 16656 をシステム イベント ログに書き込みます。 RID マスター FSMO の 10% シーリングに達すると、Directory-Services-SAM イベント 16657 をそのシステム イベント ログに書き込み、シーリングを上書きするまで、それ以上の RID プールの割り当ては行われません。 必然的に、ドメイン内の RID マスターの状態を評価し、過度の RID の割り当ての可能性に対処しなければならなくなります。このことは、ドメインの RID 空間全体が枯渇しないように保護することにもなります。  
  
このシーリングは、利用可能な残りの RID 空間の 10% にハードコードされます。 つまり、グローバル RID 空間の 90% に相当するプールを RID マスターが割り当てると、シーリングがアクティブになります。  
  
-   既定のドメインの場合、最初のトリガー ポイントは、2<sup>30</sup>-1 * 0.90 = 966,367,640 個の RID (RID の残数は 107,374,183 個) です。  
  
-   RID 空間の 31 番ビットがロック解除されているドメインの場合、トリガー ポイントは、2<sup>31</sup>-1 * 0.90 = 1,932,735,282 個の RID (RID の残数は 214,748,365) です。  
  
トリガーが発生すると、RID マスターは次のオブジェクトの Active Directory 属性 **msDS-RIDPoolAllocationEnabled** (一般名 **ms-DS-RID-Pool-Allocation-Enabled**) を FALSE に設定します。  
  
CN RID Manager$、CN を = = System, DC =*<domain>*  
  
これによって 16657 イベントが書き込まれ、すべてのドメイン コントローラーに対するそれ以上の RID ブロックの発行は禁止されます。 ドメイン コントローラーは、発行済みの未使用の RID プールの使用を継続します。  
  
ブロックを削除し、RID プール割り当てを続行できるようにするには、この値を TRUE に設定します。 RID マスターによって実行される次回の RID 割り当てで、この属性は既定の NOT SET 値に戻ります。 その後、それ以上のシーリングはなくなり、最終的にグローバル RID 空間は枯渇し、フォレストの回復またはドメインの移行が必要になります。  
  
#### <a name="removing-the-ceiling-block"></a>シーリング ブロックの削除  
人為的シーリングに到達したときにブロックを削除するには、次の手順を実行します。  
  
1.  Windows Server 2012 ドメイン コントローラーで RID マスターの役割が実行されていることを確認します。 実行されていない場合は、それを Windows Server 2012 ドメイン コントローラーに転送します。  
  
2.  LDP.exe を実行します。  
  
3.  **[接続]** メニューをクリックし、ポート 389 上の Windows Server 2012 RID マスターの役割について [*接続*] をクリックします。次に、ドメイン管理者として **[バインド]** をクリックします。  
  
4.  **[表示]** メニューの **[ツリー]** をクリックし、**[ベース DN]** で RID マスターの独自のドメイン名前付けコンテキストを選びます。 **[OK]** をクリックします。  
  
5.  ナビゲーション ウィンドウで、**[CN=System]** コンテナーをドリルダウンし、**[CN=RID Manager$]** オブジェクトをクリックします。 オブジェクトを右クリックし、**[変更]** をクリックします。  
  
6.  [エントリ属性の編集] に、次のように入力します。  
  
    ```  
    MsDS-RidPoolAllocationEnabled  
    ```  
  
7.  **[値]** に、次のように入力します (大文字で)。  
  
    ```  
    TRUE  
    ```  
  
8.  **[操作]** で **[置換]** を選択し、**[入力]** をクリックします。 これによって **[エントリ一覧]** が更新されます。  
  
9. **[同期]** チェック ボックスと **[拡張]** チェック ボックスをオンにして、**[実行]** をクリックします。  
  
    ![RID の発行](media/Managing-RID-Issuance/ADDS_RID_TR_LDPRaiseCeiling.png)  
  
10. 操作に成功すると、LDP 出力ウィンドウが表示されます。  
  
    ```  
    ***Call Modify...  
    ldap_modify_ext_s(ld, 'CN=RID Manager$,CN=System,DC=<domain>',[1] attrs, SvrCtrls, ClntCtrls);  
    Modified "CN=RID Manager$,CN=System,DC=<domain>".  
  
    ```  
  
    ![RID の発行](media/Managing-RID-Issuance/ADDS_RID_TR_LDPRaiseCeilingSuccess.png)  
  
### <a name="other-rid-fixes"></a>その他の RID 修正  
以前の Windows Server オペレーティング システムでは、rIDSetReferences 属性が見つからないとき、RID プールのリークが発生していました。 Windows Server 2008 R2 を実行するドメイン コント ローラーでこの問題を解決するには、修正プログラムをインストール[サポート技術情報 2618669](https://support.microsoft.com/kb/2618669)します。  
  
### <a name="unfixed-rid-issues"></a>未修正の RID の問題  
以前より、アカウントの作成に失敗すると RID のリークが発生します。アカウントを作成するときは、作成に失敗しても RID が使用されます。 最も一般的な例は、複雑さの要件を満たさないパスワードを使ってユーザーを作成する場合です。  
  
### <a name="rid-fixes-for-earlier-versions-of-windows-server"></a>初期バージョンの Windows Server での RID 修正  
上記すべての修正と変更については、Windows Server 2008 R2 の修正プログラムがリリースされています。 現在計画中または作成中の Windows Server 2008 の修正プログラムはありません。  
  
## <a name="BKMK_Tshoot"></a>RID 発行のトラブルシューティング  
  
### <a name="introduction-to-troubleshooting"></a>トラブルシューティングの概要  
RID 発行のトラブルシューティングでは、論理的で一連の手続きで構成される方法が必要になります。 RID が原因でトリガーされる警告やエラーをイベント ログで注意深く監視している場合を除き、問題発生時にまず疑われることはアカウント作成の失敗の可能性です。 RID 発行のトラブルシューティングで重要なことは、症状の発生がどのようなタイミングだと想定内あるいは想定外であるのかを把握することです。RID 発行に関する多くの問題は 1 つのドメイン コントローラーだけに関係する場合があり、コンポーネントの機能強化とは関係がありません。 次の簡単な図は、より明確な意思決定を行うのに役立ちます。  
  
![RID の発行](media/Managing-RID-Issuance/adds_rid_issuance_troubleshooting.png)  
  
### <a name="troubleshooting-options"></a>トラブルシューティングのオプション  
  
#### <a name="logging-options"></a>ログ オプション  
RID 発行でのすべてのログ記録は、システム イベント ログのソース Directory-Services-SAM で行われます。 ログ記録は既定で有効にされ、最大限の詳細情報が収集されるように構成されます。 Windows Server 2012 の新しいコンポーネントの変更についてログに記録されるエントリがない場合は、その問題を、Windows 2008 R2 以前のオペレーティング システムで見受けられた、従来型の (レガシーの、Windows Server 2012 より前の) RID 発行の問題として扱います。  
  
#### <a name="utilities-and-commands-for-troubleshooting"></a>トラブルシューティングのためのユーティリティとコマンド  
前に示したログでは説明のつかない問題、特に RID 発行に関する古い問題をトラブルシューティングするには、次に示すツールを手始めに使用します。  
  
-   Dcdiag.exe  
  
-   Repadmin.exe  
  
-   Network Monitor 3.4  
  
### <a name="general-methodology-for-troubleshooting-domain-controller-configuration"></a>ドメイン コントローラー構成のトラブルシューティングのための一般的な手法  
  
1.  エラーの原因は、権限やドメイン コントローラーの可用性に関する単純な問題ですか。  
  
    1.  必要な権限なしにセキュリティ プリンシパルを作成しようとしていますか。 アクセス拒否エラーの出力を調べます。  
  
    2.  ドメイン コントローラーは利用可能ですか。 返されたエラー、あるいは LDAP またはドメイン コントローラーの可用性に関するメッセージを調べます。  
  
2.  返されたエラーは、具体的な RID を示していて、ガイダンスとして使用するのに十分な具体的情報を含んでいますか。 そうである場合、ガイダンスに従います。  
  
3.  返されたエラーは、具体的な RID を示していても、それ以外に具体的な情報はないですか。 たとえば、"ディレクトリ サービスが相対識別子を割り当てられなかったため、オブジェクトを作成できません" といったようなエラーです。  
  
    1.  「レガシー」(以前の Windows Server 2012) のドメイン コント ローラーでシステム イベント ログを調べて RID イベントに記載された[RID プール要求](https://technet.microsoft.com/library/ee406152(WS.10).aspx)(16642、16643、16644、16645、16656)。  
  
    2.  ドメイン コントローラーおよび RID マスターのシステム イベント ログで、ブロックを示す新しいイベントを調べます。これらのイベントについては、このトピックの後半に詳しい説明があります (16655、16656、16657)。  
  
    3.  Repadmin.exe を使って Active Directory のレプリケーションの正常性を検証し、**Dcdiag.exe /test:ridmanager /v** を使って RID マスターの可用性を検証します。 これらのテストで結論が得られない場合は、ドメイン コントローラーと RID マスターとの間で両側のネットワーク キャプチャを有効にします。  
  
### <a name="troubleshooting-specific-problems"></a>特定の問題のトラブルシューティング  
以下に示す新しいメッセージは、Windows Server 2012 ドメイン コントローラーのシステム イベント ログに記録されます。 System Center Operations Manager などの自動化された AD 正常性追跡システムでは、これらのイベントが監視されます。イベントはすべて重要な問題を示しています。一部のイベントはドメインに関する重大な問題を示しています。  
  
|||  
|-|-|  
|イベント ID|16653|  
|Source|Directory-Services-SAM|  
|重大度|警告|  
|メッセージ|管理者によって構成されたアカウント識別子 (RID) のプールのサイズが、サポートされている最大値を超えています。 ドメイン コントローラーが RID マスターである場合は、最大値 %1 が使用されます。<br /><br />詳細については、「[RID ブロック サイズの制限](../../ad-ds/manage/../../ad-ds/manage/../../ad-ds/manage/../../ad-ds/manage/Managing-RID-Issuance.md#BKMK_RIDBlockMaxSize)」を参照してください。|  
|説明と解決策|RID ブロック サイズの最大値は 10 進の 15000 (16 進の 3A98) になっています。 1 つのドメイン コントローラーで 15,000 個を超える RID を要求することはできません。 このイベントは、この値が最大値以下に設定されるまで、ドメイン コントローラーが起動するごとにログに記録されます。|  
  
|||  
|-|-|  
|イベント ID|16654|  
|Source|Directory-Services-SAM|  
|重大度|情報|  
|メッセージ|アカウント識別子 (RID) のプールが無効化されました。 この問題は、次のような場合に発生することが考えられます:<br /><br />1. ドメイン コントローラーがバックアップから復元される。<br /><br />2. 仮想マシンで実行されているドメイン コントローラーがスナップショットから復元される。<br /><br />3.管理者が手動でプールを無効化した。<br /><br />詳細については、「 https://go.microsoft.com/fwlink/?LinkId=226247」を参照してください。|  
|説明と解決策|このイベントが想定外である場合は、すべてのドメイン管理者に連絡して、操作を行った管理者を特定します。 ディレクトリ サービス イベント ログには、そのいずれかの手順が実行されたタイミングに関する詳しい情報も含まれます。|  
  
|||  
|-|-|  
|イベント ID|16655|  
|Source|Directory-Services-SAM|  
|重大度|情報|  
|メッセージ|アカウント識別子 (RID) のグローバルな最大値が %1 に増加しました。|  
|説明と解決策|このイベントが想定外である場合は、すべてのドメイン管理者に連絡して、操作を行った管理者を特定します。 このイベントは、既定の 2<sup>30</sup> を超える全体的な RID プール サイズの増加を示し、自動的には発生しません。管理操作によってのみ発生します。|  
  
|||  
|-|-|  
|イベント ID|16656|  
|Source|Directory-Services-SAM|  
|重大度|警告|  
|メッセージ|アカウント識別子 (RID) のグローバルな最大値が %1 に増加しました。|  
|説明と解決策|対処が必要です。 アカウント識別子 (RID) プールが、このドメイン コントローラーに割り当てられました。 使用可能なアカウント識別子の総数のうちのかなりの数をこのドメインが消費していることを、プールの値が示しています。<br /><br />ドメインが合計に使用可能なアカウント識別子の残りのしきい値に達すると、保護メカニズムがアクティブにします。 1。  この保護メカニズムでは、RID マスター ドメイン コントローラー上でのアカウント識別子の割り当てを管理者が手動で再度有効にするまで、アカウントの作成ができなくなります。<br /><br />詳細については、「 https://go.microsoft.com/fwlink/?LinkId=228610」を参照してください。|  
  
|||  
|-|-|  
|イベント ID|16657|  
|Source|Directory-Services-SAM|  
|重大度|エラー|  
|メッセージ|対処が必要です。 このドメインは、使用可能なアカウント識別子 (RID) の総数のうちのかなりの数を消費しています。 残りの使用可能なアカウント識別子の総数がX% [人為的シーリングの引数] 未満になったため、保護メカニズムがアクティブ化されました。<br /><br />この保護メカニズムでは、RID マスター ドメイン コントローラー上でのアカウント識別子の割り当てを管理者が手動で再度有効にするまで、アカウントの作成ができません。<br /><br />アカウントの作成を再度有効にする前に、このドメインで異常に高い割合でアカウント識別子が消費されていないことを確認するために、いくつかの診断を行うことは、非常に重要です。 特定された問題は、アカウントの作成を再度有効にする前に解決する必要があります。<br /><br />異常に高い割合でアカウント識別子が消費される原因となっている根本的問題を診断および解決できないと、ドメインのアカウント識別子が使い果たされる可能性があり、枯渇した後は、このドメインでのアカウント作成は永久に無効化されます。<br /><br />詳細については、「 https://go.microsoft.com/fwlink/?LinkId=228610」を参照してください。|  
|説明と解決策|すべてのドメイン管理者に連絡して、この保護を上書きするまで、このドメインではセキュリティ プリンシパルを作成できないことを伝えます。 保護を上書きする方法および可能な場合に RID プール全体を増やす方法については、「[グローバル RID 空間サイズのロック解除](../../ad-ds/manage/../../ad-ds/manage/../../ad-ds/manage/../../ad-ds/manage/Managing-RID-Issuance.md#BKMK_GlobalRidSpaceUnlock)」を参照してください。|  
  
|||  
|-|-|  
|イベント ID|16658|  
|Source|Directory-Services-SAM|  
|重大度|警告|  
|メッセージ|このイベントは、使用可能なアカウント識別子 (RID) の残り総数についての定期的な更新です。 その他のアカウント識別子の数は約: 1。<br /><br />アカウント識別子はアカウントが作成されると使用され、使い果たされると、ドメイン内での新しいアカウントの作成はできなくなる可能性があります。<br /><br />詳細については、「 https://go.microsoft.com/fwlink/?LinkId=228745」を参照してください。|  
|説明と解決策|すべてのドメイン管理者に連絡して、RID 消費が重要なマイルストーンを超えたことを伝えます。これが想定内の動作であるかどうかを判断するには、セキュリティ トラスティの作成パターンを確認します。 このイベントが再度発生することはきわめてまれです。1 億個以上の RID が割り当てられたことを意味するからです。|  
  
## <a name="see-also"></a>関連項目  
[Windows Server 2012 での RID 発行の管理](http://blogs.technet.com/b/askds/archive/2012/08/10/managing-rid-issuance-in-windows-server-2012.aspx)  
  

