---
title: ソフトウェアの制限のポリシーの技術概要
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-software-restriction-policies
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc7013b0-0efd-40fd-bd6d-75128adbd0b8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: d007d55ced9c6a18581eaedb4edb66db9eeccab9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830853"
---
# <a name="software-restriction-policies-technical-overview"></a>ソフトウェアの制限のポリシーの技術概要

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックで説明ソフトウェア制限ポリシーでは、どのような変更が過去のリリースで実装されているし、作成し、以降では、Windows ソフトウェアの制限のポリシーを展開するのに役立つその他のリソースへのリンクを提供します機能を使用するタイミングと方法。Server 2008 および Windows Vista の場合は。

## <a name="introduction"></a>概要
ソフトウェアの制限のポリシーでは、管理者がソフトウェアを特定し、ローカル コンピューター上で実行するには、その機能を制御するグループ ポリシー ベースのメカニズムに提供します。 既知の競合に対して、Microsoft Windows オペレーティング システム (Windows Server 2003 および Windows XP Professional で始まる) を実行しているコンピューターを保護し、悪意のあるウイルスなどのセキュリティの脅威からコンピューターを保護するこれらのポリシーを使用できます。トロイの木馬です。 ソフトウェアの制限のポリシーを使えば、コンピューターの構成に厳格な制限を加え、指定したアプリケーションに限って実行を許可することもできます。 ソフトウェアの制限のポリシーは、Microsoft Active Directory とグループ ポリシーに統合されています。 スタンドアロン コンピューター上でソフトウェアの制限のポリシーを作成することも可能です。

ソフトウェアの制限のポリシーは信頼ポリシーであり、スクリプトなどの必ずしも信頼できないコードの実行を制限するために管理者が設定する規則です。 ソフトウェア制限ポリシーの拡張機能には、ローカル グループ ポリシー エディターは、ローカル コンピューターまたはドメイン全体からアプリケーションの使用を制限するための設定を管理できる単一のユーザー インターフェイスを提供します。

## <a name="procedures"></a>手順

-   [ソフトウェア制限ポリシーを管理します。](administer-software-restriction-policies.md)

    -   [ソフトウェア制限ポリシーの許可/拒否リストおよびアプリケーション インベントリを確認します。](determine-allow-deny-list-and-application-inventory-for-software-restriction-policies.md)

    -   [ソフトウェア制限ポリシー ルールを操作します。](work-with-software-restriction-policies-rules.md)

    -   [ソフトウェア制限ポリシーを使用した電子メール ウイルスからコンピューターを保護するには](use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus.md)

-   [ソフトウェア制限ポリシーをトラブルシューティングします。](troubleshoot-software-restriction-policies.md)

## <a name="software-restriction-policy-usage-scenarios"></a>ソフトウェア制限ポリシーの使用シナリオ
ビジネス ユーザーは、電子メール、インスタント メッセージング、およびピア ツー ピア アプリケーションを使用して共同作業します。 特に business computing 』 で、インターネットを使用して、このようなコラボレーションを増やすと、ワーム、ウイルス、および悪意のあるユーザーまたは攻撃者の脅威などの悪意のあるコードからの脅威の操作を行いますので。

ユーザーは、スクリプト (.vbs ファイル) などにネイティブ Windows 実行可能ファイル (.exe ファイル) から (.doc ファイルなど)、ドキュメント内のマクロに至るまで、さまざまな形式で悪意のあるコードがあります。 悪意のあるユーザーや攻撃者多くの場合、ウイルスやワームを格納しているコードを実行するのにユーザーを取得するのにソーシャル エンジニア リング メソッドを使用します。 (ソーシャル エンジニア リングとは、ユーザーを騙して、パスワードやいくつかの形式のセキュリティ情報を聞き出すの用語です)。このようなコードがアクティブになる場合、ネットワーク上のサービス拒否攻撃を生成、インターネットに機密情報や個人データを送信、危険では、コンピューターのセキュリティにさらすこともできます、ハード ディスク ドライブの内容が破損します。

IT 組織とユーザーは必要のあるソフトウェアが実行しても安全とではないを決定できる必要があります。 膨大な数と悪意のあるコードが実行できるフォームでは、困難な作業になります。

悪意のあるコードや不明なまたはサポートされていないソフトウェアの両方からネットワーク コンピューターを保護するため、組織は、全体的なセキュリティ戦略の一環としてソフトウェアの制限のポリシーを実装できます。

管理者は次のタスクにソフトウェアの制限のポリシーを使用できます。

-   信頼できるコードの定義

-   スクリプト、実行可能ファイル、および ActiveX コントロールの制御用の柔軟なグループ ポリシーの設計

ソフトウェアの制限のポリシーは、ソフトウェアの制限のポリシーに準拠しているオペレーティング システムとアプリケーション (スクリプト アプリケーションなど) によって適用されます。

具体的には、管理者は次の用途にソフトウェアの制限のポリシーを使用できます。

-   クライアント コンピューターで実行できるソフトウェア (実行可能ファイル) を指定します。

-   共有のコンピューター上でユーザーによって特定のプログラムが実行されるのを防ぐ

-   信頼された発行元をクライアント コンピューターに追加できるユーザーを指定します。

-   (ポリシーがすべてのユーザーに影響するかどうか、またはクライアント コンピューター上のユーザーのサブセットを指定)、ソフトウェア制限ポリシーのスコープを設定します。

-   実行可能ファイルがローカル コンピューター、組織単位 (OU)、サイト、ドメインで実行されるのを防ぐ。 悪意のあるユーザーによって引き起こされる問題の予防にソフトウェアの制限のポリシーを使っていない場合には、これが適しています。

## <a name="BKMK_Diffs_Changes"></a>相違点と機能の変更点
Windows Server 2012 の SRP と Windows 8 の機能の変更はありません。

**サポートされているバージョン**

ソフトウェア制限ポリシーはのみで構成されているし、少なくとも実行しているコンピューターに適用される Windows Server 2003、Windows Server 2012 などと、少なくとも Windows XP、Windows 8 を含むです。

> [!NOTE]
> Windows Vista と Windows クライアント オペレーティング システムの先頭の特定のエディションには、ソフトウェアの制限のポリシーはありません。 グループ ポリシーによってドメインで管理しないコンピューターは、分散型のポリシーを受け取りません可能性があります。

**ソフトウェア制限ポリシーと AppLocker のアプリケーション制御機能の比較**

次の表は、ソフトウェア制限ポリシー (SRP) の機能と AppLocker の機能を比較します。

|アプリケーション制御機能|SRP|AppLocker|
|----------------|----|-------|
|Scope|SRP ポリシーは、Windows XP および Windows Server 2003 以降のすべての Windows オペレーティング システムに適用できます。|AppLocker ポリシーは、Windows Server 2008 R2、Windows Server 2012、Windows 7、および Windows 8 にのみ適用されます。|
|ポリシーの作成|SRP ポリシーはグループ ポリシーで管理され、GPO の管理者のみが SRP ポリシーを更新できます。 ローカル コンピューターの管理者は、ローカル GPO で定義された SRP ポリシーを変更できます。|AppLocker ポリシーはグループ ポリシーで管理され、GPO の管理者のみがポリシーを更新できます。 ローカル コンピューターの管理者は、ローカル GPO で定義された AppLocker ポリシーを変更できます。<br /><br />エラー メッセージをカスタマイズして、ヘルプの Web ページをユーザーに表示できます。|
|ポリシーの保守|SRP ポリシーを更新するには、ローカル セキュリティ ポリシー スナップイン (ポリシーがローカルに作成されている場合) またはグループ ポリシー管理コンソール (GPMC) を使う必要があります。|AppLocker ポリシーは、ローカル セキュリティ ポリシー スナップイン (ポリシーがローカルに作成されている場合)、GPMC、または Windows PowerShell の AppLocker コマンドレットを使って更新できます。|
|ポリシーの適用|SRP ポリシーは、グループ ポリシーを介して配布されます。|AppLocker ポリシーは、グループ ポリシーを介して配布されます。|
|実施モード|SRP は、「拒否リスト モード」の管理者が既定では、実行を許可、ファイルの残りの部分は、このエンタープライズで使用できるようにしないファイルのルールを作成できます。<br /><br />SRP は、「許可リスト モード」で構成することもように、既定ですべてのファイルがブロックされているし、管理者を作成する必要がありますを許可するかファイルの規則を許可します。|AppLocker によって、「モードを許可する ボックスの一覧」がありますが、一致する許可規則を実行するファイルのみが許可された場所での既定のしくみです。|
|制御できるファイルの種類|SRP では、次のファイルの種類を制御できます。<br /><br />実行可能ファイル<br />-Dll<br />-スクリプト<br />-Windows インストーラー<br /><br />SRP では、ファイルの種類を個別に制御できません。 SRP の規則すべてが 1 つの規則のコレクションに含まれます。|AppLocker では、次のファイルの種類を制御できます。<br /><br />実行可能ファイル<br />-Dll<br />-スクリプト<br />-Windows インストーラー<br />パッケージ化されたアプリとインストーラー (Windows Server 2012 および Windows 8)<br /><br />AppLocker は、5 つのファイルの種類それぞれに対して、個別の規則のコレクションを保持します。|
|指定されたファイルの種類|SRP では、実行可能なファイルの種類の一覧をサポートしています。この一覧は拡張できます。 管理者は、実行可能と見なす必要があるファイルの拡張子を追加できます。|AppLocker では、この機能はサポートされません。 AppLocker では、現在、次のファイル拡張子がサポートされます。<br /><br />実行可能ファイル (.exe、.com)<br />-Dll (.ocx、.dll)<br />-   Scripts (.vbs, .js, .ps1, .cmd, .bat)<br />-Windows インストーラー (.msi、.mst、.msp)<br />-パッケージ アプリ インストーラー (.appx)|
|規則の種類|SRP では、4 つの規則の種類がサポートされます。<br /><br />-ハッシュ<br />パス<br />署名<br />インターネット ゾーン|AppLocker では、3 つの規則の種類がサポートされます。<br /><br />-ハッシュ<br />パス<br />-パブリッシャー|
|ハッシュ値の編集|SRP では、カスタムのハッシュ値を指定することができます。|AppLocker では、ハッシュ値自体が計算されます。 内部的にポータブル実行可能 (Exe および Dll) と Windows インストーラーおよび SHA1 のフラット ファイル ハッシュ、残りの部分を Authenticode の SHA1 ハッシュを使用します。|
|さまざまなセキュリティ レベルのサポート|SRP では、管理者はアプリを実行できるアクセス許可を指定できます。 管理者がこのようなルールを構成するそのため、そのメモ帳が実行されるは常に制限されたアクセス許可と、管理者特権を持つことはありません。<br /><br />Windows Vista 以前の SRP では、複数のセキュリティ レベルがサポートされます。 Windows 7 でその一覧は、2 つのレベルに限られていました。許可されておらず、無制限に (基本的なユーザーは [許可しない] に変換されます)。|AppLocker では、セキュリティ レベルがサポートされません。|
|パッケージ アプリおよびパッケージ アプリ インストーラーを管理します。|利用できません。|.appx は、AppLocker が管理できる有効なファイルの種類です。|
|ユーザーまたはユーザー グループへの規則のターゲット設定|SRP の規則は、特定のコンピューター上のすべてのユーザーに適用されます。|AppLocker 規則は、特定のユーザーまたはユーザー グループを対象にできます。|
|規則の例外のサポート|SRP では、規則の例外がサポートされません。|AppLocker の規則は、"を許可するすべての Windows 以外の Regedit.exe"などのルールを作成する管理者を許可する例外を持つことができます。|
|監査モードのサポート|SRP では、監査モードがサポートされません。 SRP ポリシーをテストする唯一の方法は、テスト環境をセットアップして、何回か試してみることです。|AppLocker では、監査モードがサポートされます。このモードでは、管理者はユーザー エクスペリエンスに影響を与えずに、実際の運用環境でポリシーの影響をテストできます。 結果に問題がなければ、ポリシーの実施を開始できます。|
|ポリシーのエクスポートとインポートのサポート|SRP では、ポリシーのインポート/エクスポートがサポートされません。|AppLocker では、ポリシーのインポートとエクスポートがサポートされます。 これにより、サンプル コンピューターで AppLocker ポリシーを作成し、テストしてから、そのポリシーをエクスポートし、目的の GPO にインポートすることができます。|
|規則の実施|内部的に、SRP の規則は、安全性の低いユーザー モードで実施されます。|内部的には、Exe および Dll 用の AppLocker 規則は、ユーザー モードで使用を強制するよりも安全であるカーネル モードで適用されます。|

## <a name="system-requirements"></a>システム要件
ソフトウェア制限ポリシーはのみで構成されているし、少なくとも実行しているコンピューターに適用される Windows Server 2003、および少なくとも Windows XP。 ソフトウェア制限ポリシーを含むグループ ポリシー オブジェクトを配布するには、グループ ポリシーが必要です。

## <a name="software-restriction-policies-components-and-architecture"></a>ソフトウェア制限ポリシー コンポーネントとアーキテクチャ
ソフトウェア制限ポリシーは、オペレーティング システムおよびアプリケーション ソフトウェアの制限のポリシーに準拠しているソフトウェア プログラムの実行時の実行を制限するためのメカニズムを提供します。

大まかに言えば、ソフトウェア制限ポリシーは、次のコンポーネントで構成されます。

-   ソフトウェア制限ポリシー API。 作成して、ソフトウェア制限ポリシーを構成するルールを構成するアプリケーション プログラミング インターフェイス (Api) が使用されます。 さらに、ソフトウェア制限ポリシー Api のクエリを実行する、処理、およびソフトウェア制限ポリシーを適用します。

-   ソフトウェア制限ポリシーの管理ツール。 これから成る、**ソフトウェア制限ポリシー**の拡張機能、**ローカル グループ ポリシー オブジェクト エディター**スナップインで、管理者が使用して作成し、ソフトウェアの制限のポリシーを編集します。

-   アプリケーションとオペレーティング システムの Api のセットは、ソフトウェア制限ポリシーを実行時に、ソフトウェア制限ポリシーの適用を提供する Api を呼び出します。

-   Active Directory とグループ ポリシー。 ソフトウェア制限ポリシーは、Active Directory からソフトウェア制限ポリシーのスコープ設定して、これらのポリシーを適切なアプリケーションをフィルター処理、適切なクライアントに反映されるまでに、グループ ポリシー インフラストラクチャによって異なります。対象のコンピューター。

-   Authenticode と WinVerify 信頼署名付き実行可能ファイルの処理に使用する Api。

-   イベント ビューアー。 ソフトウェア制限ポリシーのログ イベントをイベント ビューアーのログで使用される関数。

-   結果のポリシー セット (RSoP) をクライアントに適用される有効なポリシーの診断に役立ちます。

SRP のアーキテクチャの詳細については SRP では、ルール、プロセスおよび相互作用を管理、方法を参照してください[ソフトウェア制限ポリシーの作業方法](https://technet.microsoft.com/library/cc786941(v=WS.10).aspx)Windows Server 2003 テクニカル ライブラリにします。

## <a name="BKMK_Best_Practices"></a>ベスト プラクティス

### <a name="do-not-modify-the-default-domain-policy"></a>既定のドメイン ポリシーを変更しないでください。

-   既定のドメイン ポリシーを編集しないでください、カスタマイズされたドメイン ポリシーに問題が発生した場合、既定のドメイン ポリシーを再適用するオプションが常にあります。

### <a name="create-a-separate-group-policy-object-for-software-restriction-policies"></a>ソフトウェア制限ポリシーの別のグループ ポリシー オブジェクトを作成します。

-   ソフトウェア制限ポリシーの独立したグループ ポリシー オブジェクト (GPO) を作成する場合は、他のドメイン ポリシーを無効にしなくても緊急時にソフトウェアの制限のポリシーを無効にします。

### <a name="if-you-experience-problems-with-applied-policy-settings-restart-windows-in-safe-mode"></a>適用されたポリシー設定に問題が発生した場合は、Windows をセーフ モードで再起動します。

-   Windows がセーフ モードで開始されると、ソフトウェア制限ポリシーは適用されません。 誤ってソフトウェア制限ポリシーとワークステーションをロックする場合、コンピュータをセーフ モードで再起動、ローカル管理者としてログオン、ポリシーを変更、実行**gpupdate**コンピューターを再起動し、通常どおりにログオンします。

### <a name="use-caution-when-defining-a-default-setting-of-disallowed"></a>[許可しない] の既定の設定を定義するときに、注意を使用します。

-   既定の設定を定義するとき**許可しない**、明示的に許可されているソフトウェアを除くすべてのソフトウェアが許可されません。 開きたい任意のファイルを開くことを許可するソフトウェア制限ポリシーのルールがある必要があります。

-   既定のセキュリティ レベル設定されている場合、システムからロックから管理者を保護する**許可しない**4 つ、レジストリ パスの規則が自動的に作成します。 削除するか、これらのレジストリ パスの規則を変更することができます。ただし、これは推奨されません。

### <a name="for-best-security-use-access-control-lists-in-conjunction-with-software-restriction-policies"></a>安全性を高めるためには、ソフトウェア制限ポリシーと組み合わせてアクセス制御リストを使用します。

-   ユーザーは、名前変更や許可されていないファイルを移動して、または無制限のファイルを上書きすることで、ソフトウェア制限ポリシーを回避しようとする可能性があります。 その結果、これらのタスクを実行するために必要なアクセスを拒否するアクセス制御リスト (Acl) を使用することをお勧めします。

### <a name="test-new-policy-settings-thoroughly-in-test-environments-before-applying-the-policy-settings-to-your-domain"></a>新しいポリシー設定を徹底的にテスト環境でテストをドメインに、ポリシー設定を適用する前にします。

-   新しいポリシー設定が期待どおりに動作可能性があります。 テスト ネットワークでのポリシー設定を展開するときに問題が発生する可能性が低くなります。

-   新しいポリシー設定をテストするための組織のドメインから独立したテストのドメインを設定することができます。 テストの組織単位にリンクすることをテスト用の GPO を作成して、ポリシー設定をテストすることもできます。 徹底的にテスト ユーザーのポリシー設定でテストしたときに、ドメインに、テスト用の GPO をリンクできます。

-   プログラムまたはファイルを設定しないで**許可しない**テストして、効果があります。 特定のファイルでの制限には、コンピューターまたはネットワークの操作に深刻なことができます。

-   期待どおりに実行しないポリシー設定は、入力された情報や入力ミスの発生できます。 新しいポリシー設定を適用する前にテストと、予期しない動作を防ぐことができます。

### <a name="filter-user-policy-settings-based-on-membership-in-security-groups"></a>セキュリティ グループのメンバーシップに基づいてユーザーのポリシー設定をフィルター処理します。

-   ユーザーまたはグループをオフにして適用するポリシー設定をしないを指定することができます、**グループ ポリシーの適用**と**読み取り**上にあるチェック ボックスは、**セキュリティ**、GPO の [プロパティ] ダイアログ ボックスのタブ。

-   読み取りアクセス許可が拒否されたときに、ポリシー設定は、コンピューターによってはダウンロードされません。 その結果、ネットワークをより迅速に機能を有効にする、不要なポリシー設定をダウンロードすることによってより少ない帯域幅が消費されます。 読み取りアクセス許可を拒否する選択**拒否**の**読み取り**上にあるチェック ボックス、**セキュリティ**GPO の [プロパティ] ダイアログ ボックスのタブ。

### <a name="do-not-link-to-a-gpo-in-another-domain-or-site"></a>別のドメインまたはサイト内の GPO にリンクしません。

-   別のドメインまたはサイト内の GPO にリンクすると、パフォーマンスが低下するがあります。

## <a name="additional-resources"></a>その他の資料

|コンテンツの種類|参考資料|
|--------|-------|
|**計画**|[ソフトウェア制限ポリシーのテクニカル リファレンス](https://technet.microsoft.com/library/cc728085(v=WS.10).aspx)|
|**運用**|[ソフトウェア制限ポリシーを管理します。](administer-software-restriction-policies.md)|
|**トラブルシューティング**|[ソフトウェア制限ポリシーのトラブルシューティング (2003)](https://technet.microsoft.com/library/cc737011(v=WS.10).aspx)|
|**セキュリティ**|[脅威と対策ソフトウェアの制限のポリシー (2008)](https://technet.microsoft.com/library/dd349795(v=WS.10).aspx)<br /><br />[脅威と対策ソフトウェアの制限のポリシー (2008 R2)](https://technet.microsoft.com/library/hh125926(v=WS.10).aspx)|
|**ツールと設定**|[ソフトウェア制限ポリシーのツールと設定 (2003)](https://technet.microsoft.com/library/cc782454(v=WS.10).aspx)|
|**コミュニティ リソース**|[ソフトウェア制限ポリシーによるアプリケーションのロックダウン](https://technet.microsoft.com/magazine/2008.06.srp.aspx?pr=blog)|

