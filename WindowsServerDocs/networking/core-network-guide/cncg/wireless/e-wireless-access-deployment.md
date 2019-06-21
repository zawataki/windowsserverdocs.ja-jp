---
title: ワイヤレス アクセスの展開
description: このトピックは Windows Server 2016 のネットワー キング ガイド「デプロイ パスワード ベース 802.1 X 認証済みワイヤレス アクセス」の一部です。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 4b66f517-b17d-408c-828f-a3793086bc1f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b2e237cee6eac6be809add37a2ac29fdf1c92118
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446497"
---
# <a name="wireless-access-deployment"></a>ワイヤレス アクセスの展開

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

ワイヤレス アクセスの展開に次の手順に従います。

- [展開し、ワイヤレス Ap の構成](#bkmk_aps)

- [ワイヤレス ユーザー セキュリティ グループを作成します。](#bkmk_groups)

- [ワイヤレス ネットワークを構成する\(IEEE 802.11\)ポリシー](#bkmk_policies)

- [NPSs を構成します。](#bkmk_nps)

- [新しいワイヤレス コンピューターをドメインに参加させる](#bkmk_domain)

## <a name="bkmk_aps"></a>展開し、ワイヤレス Ap の構成

展開して、ワイヤレス Ap の構成手順に従います。

- [ワイヤレス AP のチャネルの周波数を指定します。](#bkmk_channel)

- [ワイヤレス Ap を構成します。](#bkmk_wirelessaps)

>[!NOTE]
>このガイドの手順は含まれていません場合に、 **ユーザー アカウント制御** 続行の許可を要求するダイアログ ボックスが開きます。 このダイアログ ボックスを開いているながら、このガイドの手順を実行して、お客様の操作に応答 ダイアログ ボックスが開かれた場合はクリックして場合 **続行**します。

### <a name="bkmk_channel"></a>ワイヤレス AP のチャネルの周波数を指定します。

1 つの地理的なサイトで複数のワイヤレス Ap を展開するときに、一意のチャネルの周波数を使用して、ワイヤレス Ap 間の干渉を減らすシグナルを重複しているワイヤレス Ap を構成する必要があります。

ワイヤレス ネットワークの地理的位置にあるその他のワイヤレス ネットワークと競合しないチャネル周波数の選択を支援するために、次のガイドラインを使用できます。

- ある場合にオフィスがあるその他の組織が近接を閉じるか、お客様の組織として同じビル、これらの組織が所有するすべてのワイヤレス ネットワークがあるかどうかを識別します。 Ap のチャネルのさまざまな周波数を割り当てる必要があるとアジア太平洋をインストールする最適な場所を決定する必要があるためにのワイヤレス AP の周波数を割り当てられているチャネルおよび配置を調べる

- 組織内の隣接するフロアでのワイヤレス信号の重複を識別します。 識別する、ワイヤレス Ap のチャネルの周波数を割り当てるカバレッジ領域の外側と、組織内で重複している、任意の 2 つのことを確認するワイヤレス Ap と重複するカバレッジ割り当てられている別のチャネルの頻度。

### <a name="bkmk_wirelessaps"></a>ワイヤレス Ap を構成します。

ワイヤレス AP の製造元によって提供される製品のドキュメントと共に、次の情報を使用すると、ワイヤレス Ap を構成できます。

この手順では、通常のワイヤレス AP で構成されている項目を列挙します。 項目名は、ブランドおよびモデルによって異なる場合し、次の一覧とは異なる場合があります。 特定の詳細については、ワイヤレス AP のマニュアルを参照してください。

#### <a name="to-configure-your-wireless-aps"></a>ワイヤレス Ap を構成するには  

- **SSID**します。 ワイヤレス ネットワークの名前を指定\(s\) \(など ExampleWLAN\)します。 これは、ワイヤレス クライアントに通知される名前です。

- **暗号化**します。 WPA2 を指定\-Enterprise\(優先\)または WPA\-Enterprise、およびどちら AES\(優先\)または TKIP 暗号化用の暗号でサポートされるバージョンに応じて、ワイヤレス クライアント コンピューターのネットワーク アダプター。

- **ワイヤレス AP の IP アドレス\(静的\)** します。 AP ごとに、サブネットの DHCP スコープの除外範囲内にある一意の静的 IP アドレスを構成します。 DHCP によって割り当てから除外されているアドレスを使用して、DHCP サーバーがコンピューターまたはその他のデバイスに同じ IP アドレスを割り当てることを防ぎます。

- **サブネット マスク**します。 ワイヤレス AP を接続する LAN のサブネット マスクの設定に一致するようにこれを構成します。  

- **DNS 名**します。 一部のワイヤレス Ap は、DNS 名で構成できます。 ネットワーク上の DNS サービスは、IP アドレスに DNS 名を解決できます。 この機能をサポートする各ワイヤレス AP 上には、DNS 解決のための一意の名前を入力します。  

- **DHCP サービス**します。 組み込まれている場合は、ワイヤレス AP\-、DHCP サービスで無効にします。  

- **RADIUS 共有シークレット**します。 APs をグループ別の NPS の RADIUS クライアントとして構成する予定がなければ、各ワイヤレス AP の一意の RADIUS 共有シークレットを使用します。 NPS でグループによってアクセス ポイントを構成する場合は、グループのすべてのメンバーで同じ共有シークレットがある必要があります。 さらに、各共有シークレットを使用するには、少なくとも 22 文字の大文字が混在して小文字の英字、数字、および句読点のランダム シーケンス必要があります。 ランダム性を確保するには、NPS で見つかった文字のランダム ジェネレーターなどのランダムな文字ジェネレーターを使用することができます**構成 802.1 X**ウィザードで、共有シークレットを作成します。

>[!TIP]
>各ワイヤレス AP の共有シークレットを記録し、安全なオフィスなどのセキュリティで保護された場所に保管します。 NPS を RADIUS クライアントを構成するときは、各ワイヤレス AP の共有シークレットが必要です。  

- **RADIUS サーバーの IP アドレス**します。 NPS を実行しているサーバーの IP アドレスを入力します。

- **UDP ポート\(s\)** します。 既定では、NPS は、認証メッセージおよび UDP ポート 1813 および 1646 アカウンティング メッセージ用の UDP ポート 1812 および 1645 を使用します。 これらの同じ UDP ポートを使用して、Ap 上は別のポートを使用する正当な理由がある場合は、新しいポート番号を持つ、アクセス ポイントを構成するだけでなく、すべての Ap と同じポート番号を使用する、NPSs の再構成もことを確認することをお勧めします。 Ap と、NPSs は、同じ UDP ポートが構成されていない、NPS が受信または、Ap からの接続要求を処理することはできず、ネットワーク上のすべてのワイヤレス接続試行は失敗します。

- **Vsa**します。 一部のワイヤレス Ap がベンダーを必要と\-特定の属性\(Vsa\)完全ワイヤレス AP の機能を提供します。 NPS ネットワーク ポリシーでは、Vsa が追加されます。

- **DHCP フィルター**します。 ワイヤレス Ap、ワイヤレス AP の製造元によって説明されているように UDP ポート 68 からネットワークに IP パケットの送信からのワイヤレス クライアントをブロックするを構成します。

- **DNS フィルタ リング**します。 ワイヤレス Ap、ワイヤレス AP の製造元によって説明されているように TCP または UDP ポート 53 からネットワークに IP パケットの送信からのワイヤレス クライアントをブロックするを構成します。

## <a name="create-security-groups-for-wireless-users"></a>ワイヤレス ユーザーのセキュリティ グループを作成します。

セキュリティ グループ、1 つまたは複数のワイヤレス ユーザーを作成する次の手順を適切なワイヤレス ユーザー セキュリティ グループにユーザーを追加します。

- [ワイヤレス ユーザー セキュリティ グループを作成します。](#bkmk_groups)

- [ワイヤレス セキュリティ グループにユーザーを追加します。](#bkmk_addusers)

### <a name="bkmk_groups"></a>ワイヤレス ユーザー セキュリティ グループを作成します。

この手順を使用するには、Active Directory ユーザーとコンピューターの Microsoft 管理コンソールでワイヤレス セキュリティ グループを作成する\(MMC\)スナップ\-でします。  

この手順を実行するには、**Domain Admins** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

#### <a name="to-create-a-wireless-users-security-group"></a>ワイヤレス ユーザー セキュリティ グループを作成するには

1. **[スタート]** 、 **[管理ツール]** の順にクリックし、 **[Active Directory ユーザーとコンピュータ]** をクリックします。 Active Directory ユーザーとコンピューター スナップイン\-が開きます。 ドメインが選択されていない場合は、ドメインのノードをクリックします。 たとえば、ドメインが example.com の場合は、クリックして**example.com**します。

2. 詳細ペインで右\-新しいグループを追加するフォルダーをクリックします\(など、右\-クリック**ユーザー**\)、 をポイント**新規**、。クリックして**グループ**します。

3. **[新しいオブジェクト - グループ]** の **[グループ名]** に、新しいグループの名前を入力します。 たとえば、「**ワイヤレス グループ**します。

4. **グループのスコープ**、次のオプションのいずれかを選択します。

    - **ドメイン ローカル**

    - **グローバル**

    - **ユニバーサル**

5. **[グループの種類]** で、 **[セキュリティ]** をクリックします。

6. **[OK]** をクリックします。

ワイヤレス ユーザーのセキュリティ グループを 1 つ以上必要がある場合は、追加のワイヤレス ユーザー グループを作成する手順を繰り返します。 後で異なるアクセス許可との接続規則を提供する、各グループにさまざまな条件と制約を適用する NPS で、個々 のネットワーク ポリシーを作成できます。

### <a name="bkmk_addusers"></a> ワイヤレス ユーザーのセキュリティ グループにユーザーを追加します。

この手順を使用するには、Active Directory ユーザーとコンピューターの Microsoft 管理コンソールでのワイヤレス セキュリティ グループにユーザー、コンピューター、またはグループを追加する\(MMC\)スナップ\-でします。

この手順を実行するには、**Domain Admins** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

#### <a name="to-add-users-to-the-wireless-security-group"></a>ワイヤレス セキュリティ グループにユーザーを追加するには

1. **[スタート]** 、 **[管理ツール]** の順にクリックし、 **[Active Directory ユーザーとコンピュータ]** をクリックします。 [Active Directory ユーザーとコンピューター] MMC が開きます。 ドメインが選択されていない場合は、ドメインのノードをクリックします。 たとえば、ドメインが example.com の場合は、クリックして**example.com**します。

2. 詳細ウィンドウでダブルクリック\-ワイヤレス セキュリティ グループを含むフォルダーをクリックします。

3. 詳細ペインで右\-、ワイヤレス セキュリティ グループをクリックし、クリックして**プロパティ**します。 **プロパティ**のセキュリティ グループ ダイアログ ボックスが表示されます。

4. **メンバー** ] タブで [**追加**、し、コンピューターを追加するか、ユーザーまたはグループを追加するには、次の手順のいずれかを完了します。

##### <a name="to-add-a-user-or-group"></a>ユーザーまたはグループを追加するには

1. **を選択するオブジェクト名の入力**、ユーザーの名前を入力またはグループを追加して順にクリックします**OK**します。

2. グループのメンバーシップを他のユーザーまたはグループに割り当てるには、この手順の手順 1. を繰り返します。  

##### <a name="to-add-a-computer"></a>コンピューターを追加するには

1. **[オブジェクトの種類]** をクリックします。 **オブジェクトの種類** ダイアログ ボックスが表示されます。

2. **オブジェクトの種類**を選択します**コンピューター**、 をクリックし、 **OK**。

3. **選択するオブジェクト名を入力します。** 、クリックして、追加するコンピューターの名前を入力**OK**。

4. 他のコンピューターに割り当てるグループのメンバーシップには、手順 1 を繰り返します\-3。

## <a name="bkmk_policies"></a>ワイヤレス ネットワークを構成する\(IEEE 802.11\)ポリシー

ワイヤレス ネットワークを構成する次の手順に従って\(IEEE 802.11\)ポリシーのグループ ポリシーの拡張機能。

- [グループ ポリシー オブジェクトを開くまたは追加して開く](#bkmk_opengpme)

- [既定のワイヤレス ネットワークをアクティブ化\(IEEE 802.11\)ポリシー](#bkmk_activate)

- [新しいワイヤレス ネットワーク ポリシーを構成します。](#bkmk_policyconfig)

### <a name="bkmk_opengpme"></a>グループ ポリシー オブジェクトを開くまたは追加して開く

Active Directory Domain Services と Windows Server 2016 を実行するコンピューターで既定では、グループ ポリシー管理機能がインストールされている\(AD DS\)サーバーの役割がインストールされているし、サーバーがドメイン コント ローラーとして構成されます。 次の手順をグループ ポリシー管理コンソールを開く方法を説明する\(GPMC\)ドメイン コント ローラー。 既存のドメインを開くか、手順について説明し、\-レベルのグループ ポリシー オブジェクト\(GPO\)の編集、または新しいドメインの GPO を作成および編集用に開きます。

この手順を実行するには、**Domain Admins** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

#### <a name="to-open-or-add-and-open-a-group-policy-object"></a>開くかを追加してグループ ポリシー オブジェクトを開く

1. ドメイン コント ローラーで次のようにクリックします。**開始**、 をクリック**Windows 管理ツール**、順にクリックします**グループ ポリシー管理**します。 グループ ポリシー管理コンソールを開きます。  

2. 左側のウィンドウでダブルクリック\-[フォレスト] をクリックします。 たとえば、ダブルクリック\-クリックして**フォレスト: example.com**します。  

3. 左側のウィンドウでダブルクリック\-クリックして**ドメイン**、2 倍して\-グループ ポリシー オブジェクトを管理するドメインをクリックします。 たとえば、ダブルクリック\-クリックして**example.com**します。  

4. 次のいずれかの操作を行います。

    -   **既存のドメインを開くには\-GPO を編集するためレベル**、権限を管理するグループ ポリシー オブジェクトを含むドメインをダブルクリックします\-既定のドメイン ポリシーなど、管理するドメイン ポリシー をクリックしてクリックして**編集**します。 **グループ ポリシー管理エディター**が開きます。

    -   **新しいグループ ポリシー オブジェクトを作成して編集用に開か**、右\-クリックして新しいグループ ポリシー オブジェクトを作成するドメインをクリックします。**このドメインに GPO を作成し、リンクする**します。

        **新しい GPO**で、**名前**新しいグループ ポリシー オブジェクトの名前を入力し、クリックして**OK**します。

        右\-、新しいグループ ポリシー オブジェクトをクリックし、クリックして**編集**します。 **グループ ポリシー管理エディター**が開きます。

次のセクションでは、ワイヤレス ポリシーを作成するのにグループ ポリシー管理エディターを使用します。

### <a name="bkmk_activate"></a>既定のワイヤレス ネットワークをアクティブ化\(IEEE 802.11\)ポリシー

この手順は、既定のワイヤレス ネットワークをアクティブ化する方法を説明します。 \(IEEE 802.11\) 、グループ ポリシー管理エディターを使用してポリシー \(GPME\)します。

>[!NOTE]
>アクティブ化した後、 **Windows Vista および以降のリリース**ワイヤレス ネットワークのバージョン\(IEEE 802.11\)ポリシーまたは**Windows XP**バージョンについては、バージョン オプションは、右するときに、オプションの一覧から自動的に削除\-クリックして**ワイヤレス ネットワーク\(IEEE 802.11\)ポリシー**します。 これは、ため、選択すると、GPME の詳細ウィンドウで、ポリシーを追加するポリシーのバージョンを選択した後に発生、**ワイヤレス ネットワーク\(IEEE 802.11\)ポリシー**ノード。 ワイヤレス ポリシーのバージョンが、右に返します時点で、ワイヤレス ポリシーを削除する場合を除き、この状態のまま\-メニューをクリックして**ワイヤレス ネットワーク\(IEEE 802.11\)ポリシー** GPME で. さらに、ワイヤレス ポリシーが GPME 詳細ペインに一覧表示のみと、**ワイヤレス ネットワーク\(IEEE 802.11\)ポリシー**ノードを選択します。

この手順を実行するには、**Domain Admins** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

#### <a name="to-activate-default-wireless-network-ieee-80211-policies"></a>既定のワイヤレス ネットワークをアクティブ化する\(IEEE 802.11\)ポリシー  

1. 前の手順に従います**を開くかを追加してグループ ポリシー オブジェクトを開く**GPME を開きます。

2. 左側のウィンドウで、GPME でダブルクリック\- をクリックして**コンピューターの構成**、二重\- をクリックして**ポリシー**、二重\-クリックして**Windows の設定**、2 倍して\-クリックして**セキュリティ設定**します。

![802.1 X ワイヤレス グループ ポリシー](../../../media/Wireless-GP/Wireless-GP.jpg)

3. **セキュリティ設定**、右\-クリックして**ワイヤレス ネットワーク\(IEEE 802.11\)ポリシー**、順にクリックします**の新しいワイヤレス ポリシーの作成Windows Vista およびそれ以降のリリース**します。 

![802.1 x ワイヤレス ポリシー](../../../media/Wireless-Policy/Wireless-Policy.jpg)

4. **新しいワイヤレス ネットワーク ポリシー プロパティ** ダイアログ ボックスが表示されます。 **ポリシー名**ポリシーの新しい名前を入力するか既定の名前します。 クリックして**OK**ポリシーを保存します。 既定のポリシーをアクティブ化し、指定した新しい名前で、既定の名前または GPME の詳細ウィンドウに示さ**新しいワイヤレス ネットワーク ポリシー**します。

![新しいワイヤレス ネットワーク ポリシーのプロパティ](../../../media/Wireless-Policy-Properties/Wireless-Policy-Properties.jpg)

5. 詳細ウィンドウでダブルクリック\-クリックして**新しいワイヤレス ネットワーク ポリシー**を開きます。

次のセクションでは、ポリシーの構成、ポリシーの処理の優先順位、およびネットワークのアクセス許可を実行できます。

### <a name="bkmk_policyconfig"></a>新しいワイヤレス ネットワーク ポリシーを構成します。

このセクションでは、プロシージャを使用するワイヤレス ネットワークを構成する\(IEEE 802.11\)ポリシー。 このポリシーを使用すると、セキュリティと認証の設定を構成、ワイヤレス プロファイルを管理および優先ネットワークとして構成されていないワイヤレス ネットワークのアクセス許可を指定できます。

- [PEAP のワイヤレス接続プロファイルを構成する\-MS\-CHAP v2](#bkmk_configureprofile)  

- [ワイヤレス接続プロファイルの優先順位を設定します。](#bkmk_preferenceorder)  

- [ネットワークのアクセス許可を定義します。](#bkmk_permissions)  

#### <a name="bkmk_configureprofile"></a>PEAP のワイヤレス接続プロファイルを構成する\-MS\-CHAP v2

この手順は、PEAP を構成するための手順を提供します。\-MS\-CHAP v2 ワイヤレス プロファイルです。  

この手順を完了するには、少なくとも **Domain Admins** グループ、またはそれと同等のメンバーシップが必要です。

##### <a name="to-configure-a-wireless-connection-profile-for-peap-ms-chap-v2"></a>PEAP のワイヤレス接続プロファイルを構成する\-MS\-CHAP v2

1. GPME、先ほど作成した、ポリシーのワイヤレス ネットワークのプロパティ ダイアログ ボックスで、**全般** タブおよび**説明**ポリシーの簡単な説明を入力します。

2. WLAN AutoConfig を使用して、ワイヤレス ネットワーク アダプター設定を構成することを指定することを確認します**クライアントを使用して Windows WLAN AutoConfig サービス**が選択されています。  

3. **以下のプロファイルの順序で利用可能なネットワークに接続する**、] をクリックして**追加**、し、[**インフラストラクチャ**します。 **新しいプロファイルのプロパティ** ダイアログ ボックスが表示されます。

4. **新しいプロファイルのプロパティ** ダイアログ ボックスで、**接続** タブで、**プロファイル名**フィールドに、プロファイルの新しい名前を入力します。 たとえば、「 **Windows 10 の Example.com WLAN プロファイル**します。

5. **ネットワーク名\(s\) \(SSID\)** 、ワイヤレス Ap で構成されている SSID に対応する SSID を入力し、クリックして**追加**します。

    展開で複数の SSID を使用し、各ワイヤレス AP で同じワイヤレス セキュリティ設定を使用する場合は、この手順を繰り返して、このプロファイルを適用する各ワイヤレス AP の SSID を追加します。

    展開で複数の SSID を使用するが、各 SSID のセキュリティ設定が一致していない場合は、同じセキュリティ設定を使用する SSID のグループごとに別々のプロファイルを構成します。 たとえばがある場合は、ワイヤレス Ap の 1 つのグループは WPA2 を使用するよう構成\-エンタープライズと AES、WPA を使用するワイヤレス Ap の別のグループ\-エンタープライズおよび TKIP、ワイヤレス Ap のグループごとにプロファイルを構成します。

6. 場合、既定のテキスト**NEWSSID**が存在し、それを選択し をクリックし、**削除**します。

7. ブロードキャスト ビーコンを抑制するように構成されたワイヤレス アクセス ポイントの展開が完了している場合は、 **[ネットワークがブロードキャストを行っていない場合でも接続する]** をオンにします。

    > [!NOTE]
    > このオプションを有効にすると、ワイヤレス クライアントはのプローブし、任意のワイヤレス ネットワークに接続を試みるため、セキュリティ上のリスクを作成できます。 既定では、この設定は有効になりません。  

8. **[セキュリティ]** タブ、 **[詳細設定]** の順にクリックして、次の内容を構成します。

    1. **[IEEE 802.1X]** で 802.1X の詳細設定を構成するには、 **[802.1X の詳細設定を強制する]** を選択します。

        ときに 802.1 X の詳細設定を強制する場合、既定値**最大 Eapol\-開始メッセージ**、**保持期間**、**開始期間**、および**認証期間**は一般的なワイヤレス展開します。 このため、これを行うための特定の理由がない限り、既定値を変更する必要はありません。

    2. シングル サイン オンを有効にするには、 **[このネットワークに対するシングル サインオンを有効にする]** をオンにします。

    3. **[シングル サインオン]** の残りの既定値は、代表的なワイヤレス展開に十分対応します。

    4. **高速ローミング**より前に、ワイヤレス AP が構成されている場合、\-認証で、**以前を使用して\-認証**します。

9. ワイヤレス通信が FIPS 140 を満たしていることを指定する\-2 標準**FIPS 140 で暗号化を実行\-2 認定モード**します。

10. **[OK]** をクリックして、 **[セキュリティ]** タブに戻ります。**このネットワークのセキュリティ メソッドの選択**の**認証**を選択します**WPA2\-Enterprise**ワイヤレス AP およびワイヤレスはサポートされている場合クライアント ネットワーク アダプター。 それ以外の場合、選択**WPA\-Enterprise**します。

11. **暗号化**サポート、ワイヤレス AP およびワイヤレス クライアント ネットワーク アダプターを選択している場合、 **AES CCMP**します。 アクセス ポイントと 802.11 ac をサポートするワイヤレス ネットワーク アダプターを使用している場合は、選択**AES GCMP**します。 サポートされていない場合は、 **[TKIP]** を選択します。

    > [!NOTE]  
    > 設定は両方とも**認証**と**暗号化**ワイヤレス Ap で構成設定に一致する必要があります。 既定の設定**認証モード**、**認証エラーの最大数**、および**このネットワークへの後続の接続のユーザー情報をキャッシュ**は代表的なワイヤレス展開のための十分です。  

12. **ネットワーク認証方法の選択**を選択します**保護された EAP \(PEAP\)** 、 をクリックし、**プロパティ**します。 **保護された EAP プロパティ** ダイアログ ボックスが表示されます。

13. **保護された EAP プロパティ**、ことを確認します**証明書の検証によって、サーバーの id を確認**が選択されています。

14. **信頼されたルート証明機関**、信頼されたルート証明機関を選択します。 \(CA\) 、nps サーバー証明書を発行します。

    > [!NOTE]  
    > この設定により、クライアントが信頼するルート CA は、選択した CA に限定されます。 信頼されたルート Ca が選択されていない場合クライアントは、すべてのルート Ca が信頼されたルート証明機関の証明書ストアに一覧表示で信頼されます。  

15. **認証方法を選択**一覧で、選択**セキュリティで保護されたパスワード\(EAP\-MS\-CHAP v2\)** します。

16. をクリックして**構成**です。 **EAP MSCHAPv2 のプロパティ**] ダイアログ ボックスで、確認 **[Windows のログオン名とパスワードを使用して、自動的に\(およびドメイン\)** が選択されているし、をクリックして **[Ok]** します。

17. PEAP 高速再接続を有効にすることを確認します**高速再接続を有効にする**が選択されています。

18. サーバー暗号化バインドの TLV 接続の試行を要求するには、オン**サーバーに暗号化バインドの TLV がない場合は切断**します。

19. 認証の第 1 フェーズでユーザー id をマスクすることを指定するには、選択**Id プライバシーを有効にする**、およびテキスト ボックスに、テキスト ボックスを空白のままにまたは、匿名 id の名前を入力します。

    > 注意事項
    > - NPS を使用して 802.1 X ワイヤレスの NPS ポリシーを作成する必要があります**接続要求ポリシー**します。 NPS ポリシーは NPS を使用して作成された場合**ネットワーク ポリシー**id のプライバシーは機能しません。
    > - EAP id プライバシーが、空、または匿名の id に特定の EAP メソッドによって提供される\(実際の id と異なる\)は、EAP id 要求への応答で送信されます。 PEAP では、認証中に 2 回、id を送信します。 最初のフェーズでは、id はプレーン テキストで送信し、この id はクライアント認証ではなく、ルーティングの目的で使用します。 実際の id、認証に使用される — は最初のフェーズで規定されているセキュリティで保護されたトンネル内で、認証の 2 番目のフェーズ中に送信します。 場合**Id プライバシーを有効にする**チェック ボックスが選択されている場合、ユーザー名は、テキスト ボックスで指定されたエントリに置き換えられます。 たとえば、 **Id プライバシーを有効にする**が選択されていると id のプライバシーに関する別名**匿名**は、テキスト ボックスで指定します。 実際の id の別名を持つユーザーの<strong>jdoe@example.com</strong>、認証の最初のフェーズで送信された id に変更されます <strong>anonymous@example.com</strong>します。 ルーティングの目的で使用されているために、第 1 フェーズ id の領域の部分は変更されません。  

20. をクリックして**OK**を閉じる、**保護された EAP プロパティ** ダイアログ ボックス。
21. をクリックして**OK**を閉じる、**セキュリティ**タブ。
22. 追加プロファイルを作成する場合は、クリックして**追加**、およびワイヤレス クライアントとネットワークのプロファイルの適用先の各プロファイルをカスタマイズするさまざまな選択を行う前の手順を繰り返します。 追加のプロファイルが完了したら、クリックして**OK**ワイヤレス ネットワーク ポリシーのプロパティ ダイアログ ボックスを閉じます。

次のセクションでは、最適なセキュリティ ポリシーのプロファイルを注文できます。

#### <a name="bkmk_preferenceorder"></a>ワイヤレス接続プロファイルの優先順位を設定します。
ワイヤレス ネットワーク ポリシーで複数のワイヤレス プロファイルを作成して、最適な有効性とセキュリティ用のプロファイルを注文する場合は、この手順を使用することができます。

サポートできるようにするセキュリティの最高レベルでのワイヤレス クライアントの接続を確認するには、一覧の上部にある、最も制限の厳しいポリシーを配置します。

たとえば、WPA2 をサポートするクライアントのいずれかと、WPA をサポートするクライアント用の 2 つのプロファイルがある場合は、一覧に高い WPA2 プロファイルを配置します。 これにより、WPA2 をサポートするクライアントがそのメソッドを使用して安全性の低い WPA ではなく、接続のことです。

この手順では、ドメイン メンバー ワイヤレス クライアントをワイヤレス ネットワークに接続するワイヤレス接続プロファイルを使用する順序を指定する方法を説明します。

この手順を完了するには、少なくとも **Domain Admins** グループ、またはそれと同等のメンバーシップが必要です。

##### <a name="to-set-the-preference-order-for-wireless-connection-profiles"></a>ワイヤレス接続プロファイルの優先順位を設定するには

1. 構成したポリシーのワイヤレス ネットワークのプロパティ ダイアログ ボックスで、GPME でクリックして、**全般**タブ。

2. **全般**] タブの [**以下のプロファイルの順序で利用可能なネットワークに接続する**一覧内で移動するプロファイルを選択し、いずれか、"上向き矢印"ボタンをクリックして、または"下向きの矢印"プロファイルを一覧で目的の場所に移動するボタンをクリックします。

3.  リスト内に移動したいプロファイルごとに手順 2. を繰り返します。  

4.  をクリックして**OK**すべての変更を保存します。

次のセクションでは、ワイヤレス ポリシーのネットワークのアクセス許可を定義できます。

#### <a name="bkmk_permissions"></a>ネットワークのアクセス許可を定義します。
設定を構成することができます、**ネットワークのアクセス許可**ワイヤレス ネットワークにドメイン メンバーのタブ\(IEEE 802.11\)ポリシーを適用します。

のみが構成されていないワイヤレス ネットワークの次の設定を適用することができます、**全般** タブで、**ワイヤレス ネットワーク ポリシーのプロパティ**ページ。

- 許可または特定のワイヤレス ネットワークを指定するネットワークの種類、サービス セット識別子への接続を拒否\(SSID\)

- 許可または拒否のアドホック ネットワークへの接続

- 許可または拒否インフラストラクチャ ネットワークへの接続

- ユーザーのネットワークの種類を表示する許可または拒否\(アドホックまたはインフラストラクチャ\)アクセスが拒否されています。

- ユーザーのすべてのユーザーに適用されるプロファイルの作成を許可または拒否

- グループ ポリシー プロファイルを使用して、ユーザーは許可されているネットワークに接続のみできます。

メンバーシップ**Domain Admins**、またはそれと同等がこれらの手順を完了するために必要な最低限です。

##### <a name="to-allow-or-deny-connections-to-specific-wireless-networks"></a>許可するか、特定のワイヤレス ネットワークへの接続を拒否するには

1. ワイヤレス ネットワークのプロパティ ダイアログ ボックスで、GPME でクリックして、**ネットワークのアクセス許可**タブ。

2. **ネットワークのアクセス許可**] タブで [**追加**します。 **新しいアクセス許可エントリ** ダイアログ ボックスが表示されます。

3. **新しいアクセス許可エントリ** ダイアログ ボックスで、**ネットワーク名\(SSID\)** フィールドに、ネットワーク、ネットワークの SSID を入力するアクセス許可を定義します。

4.  **ネットワークの種類**、**インフラストラクチャ**または**アドホック**します。

    > [!NOTE]  
    > ブロードキャスト ネットワークが、インフラストラクチャまたはアドホック ネットワークがかどうかが不明な場合は、ネットワークの種類ごとに 1 つずつ、2 つのネットワーク アクセス許可エントリを構成できます。

5. **権限**を選択します**許可**または**Deny**します。

6. クリックして**OK**に戻るには、**ネットワークのアクセス許可** タブ。

##### <a name="to-specify-additional-network-permissions-optional"></a>追加のネットワーク アクセス許可を指定する\((省略可能)\)

1.  **ネットワークのアクセス許可** タブで、次の一部またはすべてを構成します。  

    -   選択するドメイン メンバーがアドホック ネットワークへのアクセスを拒否する**ad に接続しない\-アドホック ネットワーク**します。

    -   選択するドメイン メンバーがインフラストラクチャ ネットワークへのアクセスを拒否する**インフラストラクチャ ネットワークに接続しない**します。  

    -   ネットワークの種類を表示するドメインのメンバーに\(アドホックまたはインフラストラクチャ\)選択へのアクセスが拒否されている**拒否されたネットワークを表示するユーザーをできるようにする**します。

    -   すべてのユーザーに適用されるプロファイルを作成するユーザーを許可するのには、選択**ユーザーがすべてのユーザー プロファイルを作成できる**します。

    -   ユーザーが許可されたグループ ポリシー プロファイルを使用してネットワークにのみ接続できることを指定するには、選択**のみグループ ポリシー プロファイルを使用して、許可されたネットワークの**します。

## <a name="bkmk_nps"></a>NPSs を構成します。
ワイヤレス アクセス用の 802.1 X 認証を実行する NPSs を構成するこれらの手順に従います。

- [Active Directory Domain Services に NPS を登録します。](#bkmk_npsreg)

- [NPS の RADIUS クライアントとしてワイヤレス AP を構成します。](#bkmk_radiusclient)

- [ウィザードを使用して、802.1 X ワイヤレスの NPS ポリシーを作成します。](#bkmk_npspolicy)

### <a name="bkmk_npsreg"></a>Active Directory Domain Services に NPS を登録します。
ネットワーク ポリシー サーバーを実行しているサーバーを登録するこの手順を使用する\(NPS\) Active Directory Domain Services で\(AD DS\) NPS がメンバーのドメインにします。 ダイヤルを読み取る権限を許可する NPSs の\-承認プロセス中にユーザー アカウントのプロパティで、各 NPS を AD DS に登録する必要があります。 サーバーを追加、NPS の登録、 **RAS and IAS Servers** AD DS のセキュリティ グループ。

>[!NOTE]
>ドメイン コント ローラーまたは専用のサーバーに NPS をインストールできます。 まだ行っていない場合、NPS をインストールする次の Windows PowerShell コマンドを実行します。
    
    Install-WindowsFeature NPAS -IncludeManagementTools
    
この手順を完了するには、少なくとも **Domain Admins** グループ、またはそれと同等のメンバーシップが必要です。

#### <a name="to-register-an-nps-in-its-default-domain"></a>既定のドメインに NPS を登録するには

1. NPS では、上で**サーバー マネージャー**、 をクリックして**ツール**、 をクリックし、**ネットワーク ポリシー サーバー**します。 NPS スナップイン\-が開きます。

2. 右\-クリックして**NPS\(ローカル\)** 、 をクリックし、 **Active Directory でサーバーの登録**。 **[ネットワーク ポリシー サーバー]** ダイアログ ボックスが開きます。

3. **[ネットワーク ポリシー サーバー]** の **[OK]** をクリックし、もう一度 **[OK]** をクリックします。

### <a name="bkmk_radiusclient"></a>NPS の RADIUS クライアントとしてワイヤレス AP を構成します。
呼ばれる、AP を構成するこの手順を使用することができます、*ネットワーク アクセス サーバー \(NAS\)* 、リモート認証ダイヤルインとして\-User Service \(RADIUS\)NPS スナップインを使用してクライアント\-でします。 

>[!IMPORTANT]
>クライアント コンピューター (ワイヤレス ポータブル コンピューターなど、クライアント オペレーティング システムを実行しているコンピューター) は、RADIUS クライアントではありません。 RADIUS クライアントはネットワーク アクセス サーバー、ワイヤレス アクセス ポイント、802.1 X など\-対応のスイッチ、仮想プライベート ネットワーク\(VPN\)サーバー、およびダイヤル\-サーバーのセットアップ-に RADIUS プロトコルを使用するためNPSs などの RADIUS サーバーと通信します。

この手順を完了するには、少なくとも **Domain Admins** グループ、またはそれと同等のメンバーシップが必要です。

#### <a name="to-add-a-network-access-server-as-a-radius-client-in-nps"></a>NPS を RADIUS クライアントとしてネットワーク アクセス サーバーを追加するには

1. NPS では、上で**サーバー マネージャー**、 をクリックして**ツール**、 をクリックし、**ネットワーク ポリシー サーバー**します。 NPS スナップイン\-が開きます。

2. NPS でスナップ\-、二重\-クリックして**RADIUS クライアントとサーバー**。 右\-クリックして**RADIUS クライアント**、 をクリックし、**新規**。

3. **新しい RADIUS クライアント**、いることを確認、**この RADIUS クライアントを有効にする** チェック ボックスをオンします。

4. **新しい RADIUS クライアント**の**フレンドリ名**、ワイヤレス アクセス ポイントの表示名を入力します。

    たとえば、ワイヤレス アクセス ポイントを追加する\(アジア太平洋\)AP という名前\-01、型**AP\-01**。

5. **アドレス\(IP または DNS\)** 、IP アドレスまたは完全修飾ドメイン名を入力\(FQDN\) NAS の。

    FQDN を入力すると、名前が正しいことと、有効な IP アドレスにマップすることを確認する] をクリックして**を確認してください**、し、[**アドレスの確認**の**アドレス**フィールドでをクリックします。**解決**します。 FQDN 名は、有効な IP アドレスにマップして、NAS の IP アドレスが自動的に表示されますで**IP アドレス**します。 FQDN が解決しない場合、IP アドレスにこのようなホストは不明ことを示すメッセージが表示されます。 このような場合は、正しい AP 名があることと、アジア太平洋電源が入っていてネットワークに接続されていることを確認します。  

    をクリックして**OK**を閉じる**アドレスのことを確認**します。  

6. **新しい RADIUS クライアント**の**共有シークレット**次のいずれかの操作します。  

    -   RADIUS 共有シークレットを手動で構成するには、次のように選択します。**手動**、し、**共有シークレット**、NAS にも入力されている強力なパスワードを入力します。 共有シークレットを再入力**共有シークレットの確認入力**します。  

    -   共有シークレットを自動的に生成するには、次のように選択します。、**生成**チェック ボックスをオンにして、**生成**ボタンをクリックします。 生成された共有シークレットを保存し、しその値を使用して、NPS と通信できるように、NAS を構成します。  

        >[!IMPORTANT]
        >RADIUS 共有シークレット、仮想 AP の NPS に用に入力したが、ワイヤレス AP の実際に構成されている RADIUS 共有シークレットと正確に一致する必要があります。 RADIUS 共有シークレットを生成する NPS オプションを使用する場合は、NPS によって生成された RADIUS 共有シークレットを使用して、一致する実際のワイヤレス AP を構成する必要があります。

7. **新しい RADIUS クライアント**の**詳細**] タブの [**仕入先名**NAS の製造元の名前を指定します。 NAS の製造元の名前の確信できない場合は、選択**RADIUS 標準**します。

8. **追加オプション**EAP および PEAP、以外の認証方法を使用して、NAS は、メッセージ認証属性の使用をサポートしている場合は、選択すると、**アクセス要求メッセージを含める必要があります、メッセージ\-認証属性**します。

9. **[OK]** をクリックします。 NAS は、NPS で構成されている RADIUS クライアントの一覧に表示されます。

### <a name="bkmk_npspolicy"></a>ウィザードを使用して、802.1 X ワイヤレスの NPS ポリシーを作成します。
この手順を使用するには、接続要求ポリシーを作成し、ネットワークのいずれかの 802.1 X を展開するために必要なポリシー\-対応ワイヤレス アクセス ポイントをリモート認証ダイヤルインとして\-User Service \(RADIUS\)ネットワーク ポリシー サーバーを実行する RADIUS サーバーにクライアント\(NPS\)します。  
ウィザードを実行した後、次のポリシーが作成されます。

- 1 つの接続要求ポリシー

- 1 つのネットワーク ポリシー

>[!NOTE]
>802.1 X 認証済みアクセス用の新しいポリシーを作成する必要があるたびに、新しい IEEE 802.1 X ワイヤードおよびワイヤレス接続ウィザードを実行することができます。

この手順を完了するには、少なくとも **Domain Admins** グループ、またはそれと同等のメンバーシップが必要です。

#### <a name="create-policies-for-8021x-authenticated-wireless-by-using-a-wizard"></a>ウィザードを使用して 802.1 X 認証済みワイヤレス ポリシーを作成します。

1. 開いている、NPS スナップイン\-でします。 選択されていない場合はクリックして**NPS\(ローカル\)** します。 NPS MMC スナップインを実行している場合\-でリモート NPS でポリシーを作成、サーバーを選択するとします。

2. **Getting Started**の**標準構成**を選択します **「RADIUS server for 802.1 X Wireless or Wired Connections**します。 テキストとテキストの変更、選択内容を反映するために以下のリンク。

3. クリックして**構成 802.1 X**します。 構成 802.1 X のウィザードが開きます。

4.  **802.1 X 接続の種類を選択します**ウィザード ページの**802.1 X 接続の種類**を選択します**ワイヤレス接続のセキュリティで保護された**、し、**名前**。、ポリシーの名前を入力、または、既定の名前をそのまま**ワイヤレス接続のセキュリティで保護された**します。 **[次へ]** をクリックします。

5.  **802.1 X スイッチを指定**ウィザード ページの**RADIUS クライアント**、すべての 802.1 X スイッチおよび RADIUS クライアントとして NPS スナップインに追加しているワイヤレス アクセス ポイント\-で表示されます。 次のいずれかを行います。

    -   追加のネットワーク アクセス サーバーを追加する\(Nas\)のワイヤレス Ap などで**RADIUS クライアント**、] をクリックして**追加**、し、[**新しい RADIUS クライアント**の情報を入力します。**フレンドリ名**、**アドレス\(IP または DNS\)** 、および**共有シークレット**します。

    -   任意の NAS の設定を変更する**RADIUS クライアント**、選択、設定を変更し AP**編集**。 必要に応じて設定を変更します。

    -   一覧から、NAS を削除する**RADIUS クライアント**、NAS を選択し、クリックして**削除**します。

        >[!WARNING]
        >内からの RADIUS クライアントの削除、**構成 802.1 X**ウィザードは、NPS の構成からクライアントを削除します。 すべての追加、変更、および削除中で行われる、**構成 802.1 X** 、nps を RADIUS クライアント ウィザードが反映されますスナップイン\-で、 **RADIUS クライアント**下のノード**NPS** \/ **RADIUS クライアントとサーバー**します。 たとえば、ウィザードを使用して、802.1 X スイッチを削除する場合、スイッチはからも削除、NPS スナップイン\-でします。

6. **[次へ]** をクリックします。 **認証方法を構成**ウィザード ページの**型\(アクセスおよびネットワーク構成のメソッドに基づく\)** を選択します**Microsoft:保護された EAP \(PEAP\)** 、 をクリックし、**構成**します。

    >[!TIP]
    >証明書を使用するために見つかりません、認証方式、まず、ネットワーク上の RAS および IAS サーバーに証明書を自動的に発行する、Active Directory Certificate Services を構成していることを示すエラー メッセージが表示される場合Active Directory Domain services では、NPS を登録する手順を実行し、次の手順を使用して、グループ ポリシー更新することを確認します。をクリックして**開始**、 をクリックして**Windows システム**、 をクリックして**実行**、し、**オープン**、型**gpupdate**、し、ENTER キーを押します。 コマンドがユーザーとコンピューターのグループ ポリシーの両方が正常に更新があることを示す結果を返す場合、選択**Microsoft:保護された EAP \(PEAP\)**  、もう一度クリックして**構成**します。
    >
    >証明書を見つからないことを使用する認証方法とを示すエラー メッセージを受信する続行するグループ ポリシーを更新した後、証明書が表示されない、最小のサーバー証明書が満たしていません。コア ネットワーク必携ガイドに記載されているの要件:[802.1 X ワイヤード (有線) およびワイヤレス展開にサーバー証明書展開](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments)します。 NPS 構成を中止、NPS に発行された証明書を失効する必要がありますこの場合、\(s\)、サーバー証明書の展開ガイドを使用して、新しい証明書を構成する手順に従います。

7.  **保護された EAP のプロパティの編集**ウィザード ページの**発行された証明書**、正しい NPS 証明書が選択されているし、次の操作であることを確認します。

    >[!NOTE]
    >いることを確認の値**発行者**で選択されている証明書の正しい**発行された証明書**します。 Active Directory Certificate Services を実行している CA によって発行された証明書の想定される発行者など\(AD CS\) corp\DC1、contoso.com ドメインで名前付き**corp\-DC1\-CA**.

    -   新しい AP に関連付けられるたびに再認証する必要がないアクセス ポイント間でワイヤレス コンピューターを移動できるように、次のように選択します。**高速再接続を有効にする**します。

    -   接続するワイヤレス クライアントがネットワーク認証プロセスを終了 RADIUS サーバーに暗号化バインドの種類が存在しない場合を指定する\-長さ\-値\(TLV\)、**切断暗号化バインドのないクライアント**します。  

    -   ポリシーを変更する設定、EAP の種類**EAP の種類**、 をクリックして**編集**の**EAP MSCHAPv2 のプロパティ**、必要に応じて設定を変更し、クリックして**OK**します。  

8.  **[OK]** をクリックします。 保護された EAP プロパティの編集 ダイアログ ボックスが閉じに戻ります、**構成 802.1 X**ウィザード。 **[次へ]** をクリックします。

9. **ユーザー グループの指定**、 をクリックして**追加**、セキュリティ グループを Active Directory ユーザーのワイヤレス クライアントを構成し、コンピューターのスナップインの名前を入力し、\-でします。 たとえば、ワイヤレス グループのワイヤレス セキュリティ グループの名前を付けた場合「**ワイヤレス グループ**します。 **[次へ]** をクリックします。

10. クリックして**構成**RADIUS 標準属性と仕入先を構成する\-仮想 LAN の特定の属性\(VLAN\)としてし、必要に応じてが提供するドキュメントで指定された、ワイヤレス AP ハードウェアの製造元。 **[次へ]** をクリックします。

11. 構成の概要詳細を確認し、クリックして**完了**します。

NPS ポリシーが作成され、ワイヤレス コンピューターをドメインに参加する上で移動できます。

## <a name="bkmk_domain"></a>新しいワイヤレス コンピューターをドメインに参加させる
新しいワイヤレス コンピューターをドメインに参加する最も簡単な方法は、ワイヤード (有線) LAN のセグメントに、コンピューターを物理的に接続する\(、802.1 X スイッチによって制御されないセグメント\)コンピューターをドメインに参加する前にします。 これは、ワイヤレス グループ ポリシー設定が自動的にし、すぐに適用され、独自の PKI を展開している場合、コンピューターが CA 証明書を受け取るし、信頼されたルート証明機関の証明書ストアに配置するために最も簡単ですワイヤレス クライアントが、CA によって発行されたサーバー証明書 NPSs を信頼することができます。

同様に後新しいワイヤレス コンピューターがドメインに参加しているドメインにログオンするユーザーの推奨される方法はで、ネットワークにワイヤード (有線) 接続を使用してログを実行します。

### <a name="other-domain-join-methods"></a>その他のドメイン参加方法
これができない場合にワイヤード (有線) イーサネット接続を使用して、ユーザーがログインできない場合や、コンピューターをドメインに参加するは実用的ワイヤード (有線) 接続を使用して初めてのドメインにログオンする必要がありますメソッドを使用する代替。

- **IT スタッフのコンピューターの構成**します。 IT スタッフのメンバーでは、ワイヤレス コンピューターをドメインに参加させます。 し、シングル サインオンのブートス トラップ ワイヤレス プロファイルを構成します。 この方法では、IT 管理者は、ワイヤレス コンピューターをワイヤード (有線) イーサネット ネットワークに接続し、コンピューターをドメインに参加させます。 管理者がユーザーにコンピューターを配布します。 ワイヤード (有線) 接続、ユーザー ログオンの手動で指定されたドメインの資格情報を使用せず、コンピューターが両方に使用される、ユーザーが開始は、ドメインにログオンして、ワイヤレス ネットワークへの接続を確立する場合。

詳細については、セクションをご覧ください[IT スタッフのコンピューターの構成方法を使用して、ドメインとログオンを参加させる。](#bkmk_itstaff)

-   **ユーザーがワイヤレス プロファイルの構成をブートス トラップ**します。 ユーザーは手動でブートス トラップ ワイヤレス プロファイルを使用して、ワイヤレス コンピューターを構成し、IT 管理者から取得した指示に基づいて、ドメインに参加させます。 ワイヤレス プロファイルのブートス トラップは、ワイヤレス接続を確立し、ドメインに参加できます。 コンピューターをドメインに参加させる、コンピューターを再起動すると、ユーザー ログオンできますをドメインにワイヤレス接続とドメイン アカウントの資格情報を使用しています。

詳細については、セクションをご覧ください。[のドメインとログオンをユーザーがブートス トラップ ワイヤレス プロファイルの構成を使用して参加](#bkmk_userbootstrap)します。

### <a name="bkmk_itstaff"></a>IT スタッフのコンピューターの構成方法を使用して、ドメインとログオンを参加させる
ドメインとドメイン メンバーのユーザー\-参加しているワイヤレス クライアント コンピューター、その一時的なワイヤレス プロファイルを使用して、802.1 X 接続\-ワイヤード (有線) LAN に最初に接続しなくても、ワイヤレス ネットワークを認証します。 この一時的なワイヤレス プロファイルと呼ばれる、*ワイヤレス プロファイルをブートス トラップ*します。

ブートス トラップ ワイヤレス プロファイルが、ユーザー アカウントの資格情報のドメイン ユーザーを手動で指定する必要があり、リモート認証ダイヤルインの証明書を検証しません\-User Service \(RADIUS\)サーバーネットワーク ポリシー サーバーを実行している\(NPS\)します。

ワイヤレス接続が確立されると、ワイヤレス クライアント コンピューターでは、グループ ポリシーを適用し、新しいワイヤレス プロファイルが自動的に発行します。 新しいポリシーは、クライアント認証用のコンピューターとユーザー アカウントの資格情報を使用します。 

また、PEAP の一部として\-MS\-CHAP v2 の相互認証がブートス トラップのプロファイルでは、クライアントではなく、新しいプロファイルを使用して、RADIUS サーバーの資格情報を検証します。

コンピューターをドメインに参加すると後、は、この手順を使用して、ワイヤレス コンピューターをドメインに配布する前に、シングル サインオンのブートス トラップ ワイヤレス プロファイルを構成する\-メンバー ユーザー。

#### <a name="to-configure-a-single-sign-on-bootstrap-wireless-profile"></a>シングル サインオンのブートス トラップ ワイヤレス プロファイルを構成するには

1. という名前のこのガイドの手順を使用してブートス トラップのプロファイルを作成[PEAP のワイヤレス接続プロファイルを構成\-MS\-CHAP v2](#bkmk_configureprofile)、し、次の設定を使用します。

    - PEAP\-MS\-CHAP v2 認証

    - RADIUS サーバーの証明書の無効を検証します。

    - シングル サインオンを有効になっています。

2. 新しいのブートス トラップのプロファイルの作成をワイヤレス ネットワーク ポリシーのプロパティで、**全般**タブ、ブートス トラップのプロファイルを選択してクリックして**エクスポート**するプロファイルをエクスポートする、ネットワーク共有、USB フラッシュ ドライブ、または簡単にアクセスできるその他の場所。 プロファイルは、指定した場所を *.xml ファイルとして保存されます。

3. 新しいワイヤレス コンピューターをドメインに参加\(IEEE 802.1 X を必要としないイーサネット接続を使用して認証\)を使用して、コンピューターに、ブートス トラップ ワイヤレス プロファイルを追加、 **netsh wlanプロファイルを追加する**コマンド。

    >[!NOTE]
    >詳細についてを参照してください Netsh Commands for Wireless Local Area Network \(WLAN\)で[http:\/\/technet.microsoft.com\/ライブラリ\/dd744890.aspx](https://technet.microsoft.com/library/dd744890).

4. 「Windows 10 を実行しているコンピューターを使用して、ドメインにログオンします」する手順と、ユーザーに新しいワイヤレス コンピューターを配布します。

ユーザーは、コンピューターを起動するときに Windows ドメイン ユーザー アカウント名とパスワードを入力するように求めるプロンプトを表示します。 シングル サインオンが有効になって、コンピューターは、まずワイヤレス ネットワークとドメインにログオンしとの接続を確立するためにドメイン ユーザー アカウントの資格情報を使用します。

#### <a name="bkmk_w10"></a>Windows 10 を実行しているコンピューターを使用してドメインにログオンします。

1. コンピューターからログオフするか、コンピューターを再起動します。

2. キーボードの任意のキーを押してまたはデスクトップをクリックします。 表示される、ローカル ユーザー アカウント名とパスワードの入力フィールド名の下で、ログオン画面が表示されます。 ローカル ユーザー アカウントでログオンしないでください。

3. 画面の左下隅でクリックして**その他のユーザー**します。 その他のユーザーのログオン画面は、ユーザー名とパスワードの 2 つのフィールドが表示されます。 以下のパスワード フィールドには、テキスト**にサインオンします。** クリックし、コンピューターが参加しているドメインの名前。 たとえば、example.com ドメインの名前が場合、テキストは**にサインオンします。例**します。

4. **ユーザー名**、ドメイン ユーザー名を入力します。

5. **[パスワード]** にドメインのパスワードを入力し、矢印をクリックするか、Enter キーを押します。

>[!NOTE]
>場合、**その他のユーザー**画面では、テキストは含まれません**にサインオン:** と、ドメイン名の形式でユーザー名を入力する必要があります*ドメイン\\ユーザー*します。 という名前のアカウントで example.com というドメインにログオンするなど、**ユーザー\-01**、型**例\\ユーザー\-01**します。

### <a name="bkmk_userbootstrap"></a>ユーザーがブートス トラップ ワイヤレス プロファイルの構成を使用して、ドメインとログオンを参加させる
一般的な手順 セクションで手順を完了するこの方法を使用し、ドメインを指定する\-メンバーのユーザーを手動でブートス トラップ ワイヤレス プロファイルを使用して、ワイヤレス コンピューターを構成する方法についての説明。 ワイヤレス プロファイルのブートス トラップは、ワイヤレス接続を確立し、ドメインに参加できます。 コンピューターがドメインに参加し、再起動後、ユーザーは、ワイヤレス接続を介してドメインにログオンできます。

#### <a name="general-steps"></a>一般的な手順

1. ローカル コンピューターの管理者アカウントを構成する**コントロール パネルの** ユーザーの。

    >[!IMPORTANT]
    >コンピューターをドメインに参加するには、ユーザーをローカルの Administrator アカウントでコンピューターにログオンする必要があります。 または、ユーザーは、コンピューター、ドメインへの参加のプロセス中に、ローカルの Administrator アカウントの資格情報を指定する必要があります。 さらに、ユーザーは、ユーザーがコンピューターを参加させる必要があるドメイン ユーザー アカウントが必要です。 ドメイン アカウントの資格情報のコンピューターをドメインに参加させるプロセス中に、ユーザーが求められます\(ユーザー名とパスワード\)します。

2. 次の手順に記載されているブートス トラップのワイヤレス プロファイルを構成するための手順をドメイン ユーザーに提供**ブートス トラップ ワイヤレス プロファイルを構成する**します。
3. さらに、ローカル コンピューター資格情報をユーザーに提供\(ユーザー名とパスワード\)、およびドメインの資格情報\(ドメイン ユーザー アカウント名とパスワード\)形式で*DomainName\\UserName*、「コンピューターをドメインに参加する」する手順と"ログオンして、ドメイン"では、Windows Server 2016 にまとめられている[コア ネットワーク ガイド](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide)します。

#### <a name="to-configure-a-bootstrap-wireless-profile"></a>ブートス トラップ ワイヤレス プロファイルを構成するには

1. ネットワーク管理者または IT サポートによって提供される資格情報を使用して、ローカル コンピューターの管理者アカウントでコンピューターにログオンするプロフェッショナル。

2. 右\-デスクトップで、ネットワーク アイコンをクリックし、をクリックして**オープン ネットワークと共有センター**します。 **[ネットワークと共有センター]** が開きます。 **ネットワーク設定を変更**、 をクリックして**を設定すると、新しい接続またはネットワーク**します。 **接続をセットアップまたはネットワーク** ダイアログ ボックスが表示されます。

3. をクリックして**ワイヤレス ネットワークに手動で接続**、順にクリックします**次**します。

4. **ワイヤレス ネットワークに手動で接続**の**ネットワーク名**AP の SSID の名前を入力します。  

5. **セキュリティの種類**、管理者によって提供される設定を選択します。

6. **暗号化の種類**と**セキュリティ キー**、選択するか、管理者によって指定される設定を入力します。

7. 選択**この接続を自動的に開始**、順にクリックします**次**します。

8. **が正常に追加 * * *、ネットワークの SSID*、 をクリックして**接続設定を変更**します。

9. クリックして**接続設定を変更**します。 *Your ネットワーク SSID*ワイヤレス ネットワークのプロパティ ダイアログ ボックスが表示されます。

10. をクリックして、**セキュリティ**] タブで、し、[**ネットワーク認証方法の選択**を選択します**保護された EAP \(PEAP\)** します。

11. **[設定]** をクリックします。 **保護された EAP \(PEAP\)プロパティ**ページが開きます。

12. **保護された EAP \(PEAP\)プロパティ**いることを確認 ページで、**サーバー証明書を検証**が選択されていない場合、をクリックして**ok** 2 回とクリックして**閉じる**します。

13. Windows は、ワイヤレス ネットワークに接続を試みます。 ブートス トラップ ワイヤレス プロファイルの設定では、ドメインの資格情報を提供する必要がありますを指定します。 Windows では、アカウント名とパスワードの入力を求められたら、次のように、ドメイン アカウントの資格情報を入力します。*ドメイン名\\ユーザー名*、*ドメイン パスワード*します。

##### <a name="to-join-a-computer-to-the-domain"></a>コンピューターをドメインに参加させる

1. ローカルの Administrator アカウントでコンピューターにログオンします。

2. 検索テキスト ボックスに「 **PowerShell**します。 右クリックし、検索結果で**Windows PowerShell**、 をクリックし、**管理者として実行**します。 Windows PowerShell は、管理者特権のプロンプトを開きます。

3. Windows PowerShell で次のコマンドを入力し、ENTER キーを押します。 参加するドメインの名前を持つ変数のドメイン名を置き換えることを確認します。
    
    コンピューターの追加のドメイン名
    
4. 表示されたら、ドメイン ユーザー名とパスワードを入力し、をクリックして**OK**します。
5. コンピューターを再起動します。
6. 前のセクションの指示に従って、 [Windows 10 を実行しているコンピューターを使用してドメインにログオン](#bkmk_w10)します。