---
title: 領域名
description: このトピックでは、ネットワーク ポリシー サーバーの接続要求が Windows Server 2016 での処理で領域名の使用の概要を示します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d011eaad-f72a-4a83-8099-8589c4ee8994
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 65a272873a60d74efcf417a16fdc84670f5878da
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447005"
---
# <a name="realm-names"></a>領域名

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)


このトピックでは、ネットワーク ポリシー サーバーの接続要求の処理で領域名の使用の概要については使用できます。

User-name RADIUS 属性は、通常のユーザー アカウントの場所とユーザー アカウント名を含む文字列です。 ユーザー アカウントの場所を使用して、領域または領域名も呼ばれ、DNS ドメイン、Active Directory® ドメイン、および Windows NT 4.0 ドメインを含むドメインの概念と同義です。 たとえば、ユーザー アカウントが example.com という名前のドメインのユーザー アカウント データベースにある場合、領域名は example.com にします。

User-name RADIUS 属性には、ユーザー名が含まれている場合、別の例ではuser1@example.comuser1 が、ユーザー アカウント名、および、example.com が領域名。 プレフィックスまたはサフィックスとして、ユーザー名に領域名を表示できます。

- **Example \user1**します。 この例では、領域名で**例**; プレフィックスであり、Active Directory の名前も&reg;Domain Services \(AD DS\)ドメイン。

- <strong>user1@example.com</strong>. この例では、領域名で**example.com**サフィックスは、DNS ドメイン名または AD DS ドメインの名前のいずれかになります。

設計および RADIUS インフラストラクチャの展開中に、接続要求ポリシーで構成されている領域名を使用するは RADIUS サーバーに、ネットワーク アクセス サーバーとも呼ばれます。 RADIUS クライアントから接続要求がルーティングされることを確認するには認証し、接続要求を承認します。

既定の接続要求ポリシーの RADIUS サーバーとして NPS を構成すると、NPS は NPS は、メンバーのドメインと信頼されたドメインの接続要求を処理します。

で信頼されていないドメインに転送接続要求を RADIUS プロキシとして機能する NPS を構成するには、新しい接続要求ポリシーを作成する必要があります。 新しい接続要求ポリシー、転送する接続要求の User-name 属性が含まれる領域の名前とユーザー名 属性を構成することにあります。 リモート RADIUS サーバー グループと、接続要求ポリシーを構成することも必要があります。 接続要求ポリシーは、NPS が User-name 属性の領域部分に基づいてリモート RADIUS サーバー グループに転送する接続要求を計算できます。

## <a name="acquiring-the-realm-name"></a>領域名を取得

ユーザー名の領域名部分は、領域名を自動的に提供するユーザーのコンピューターに接続マネージャー (CM) プロファイルが構成されている場合、またはときの接続中にユーザーの種類パスワードに基づく資格情報が提供されます。

ネットワーク接続の試行中に、資格情報を入力するときに、ネットワークのユーザーが、領域名を指定するを指定することができます。

たとえば、ユーザーのユーザー アカウント名と、領域名を含む、ユーザー名を入力するを必要とする**ユーザー名**で、 **Connect**ダイヤルアップまたは仮想プライベート ネットワーク (VPN) を行うときに、ダイアログ ボックス接続します。

さらに、接続マネージャー管理キット (CMAK) でカスタムのダイヤル パッケージを作成する場合は、ユーザーのコンピューターにインストールされている CM プロファイルにユーザー アカウント名に領域名を自動的に追加することでユーザーを支援することができます。 たとえば、ユーザーが資格情報を入力するときに、ユーザー アカウント名を指定するだけがあるできるように CM プロファイルに領域名とユーザー名の構文を指定できます。 このような状況を習得したり、ユーザー アカウントがドメインに注意してください、ユーザーは必要ありません。

認証プロセス中にユーザーが自分のパスワードに基づく資格情報を入力した後、ユーザー名に渡されますアクセス クライアントからネットワーク アクセス サーバー。 ネットワーク アクセス サーバーは、接続要求を作成し、RADIUS プロキシまたはサーバーに送信されるアクセス要求メッセージの User-name RADIUS 属性内の領域名が含まれています。

NPS を RADIUS サーバーには、アクセス要求メッセージが構成されている接続要求ポリシーのセットに対して評価されます。 接続要求ポリシーの条件には、ユーザー名 属性の内容の仕様を含めることができます。

一連の受信メッセージの User-name 属性内の領域名に固有の接続要求ポリシーを構成することができます。 これにより、NPS が RADIUS プロキシとして使用する場合は、RADIUS メッセージを RADIUS サーバーの特定のセットに特定の領域名を転送するルーティング規則を作成することができます。

## <a name="attribute-manipulation-rules"></a>属性の操作規則

RADIUS メッセージが処理 (ときにローカル NPS が RADIUS サーバーとして使用されている) か、別の RADIUS サーバー (NPS を RADIUS プロキシとして使用されている) 場合に転送、前に、属性の操作規則によって、メッセージでユーザー名属性を変更できます。 ユーザー名属性の属性の操作規則を選択して構成できます**ユーザー名**上、**条件**タブで、接続要求ポリシーのプロパティ。 NPS 属性の操作規則は、正規表現構文を使用します。

次を変更するユーザー名属性の属性の操作規則を構成できます。

- ユーザー名から領域名を削除\(realm stripping とも呼ばれます\)します。 たとえば、ユーザー名user1@example.comuser1 に変更されます。

- 構文は、領域名を変更します。 たとえば、ユーザー名user1@example.comに変更がuser1@wcoast.example.comします。

- 領域名の構文を変更します。 たとえば、ユーザー名 example \user1 に変更user1@example.comします。

最初に一致する接続要求ポリシーの追加の設定を使用して決定を構成する属性の操作規則に従って、ユーザー名属性が変更されると後、かどうか。

- (ときにローカル NPS が RADIUS サーバーとして使用されている)、NPS は、アクセス要求メッセージを処理します。

- NPS は、(NPS を RADIUS プロキシとして使用されている) 場合に、別の RADIUS サーバーにメッセージを転送します。

## <a name="configuring-the-nps-supplied-domain-name"></a>NPS が提供するドメイン名を構成します。

ユーザー名にドメイン名が含まれていない場合、NPS は 1 つを提供します。 既定では、NPS が提供するドメイン名は、NPS がメンバーであるドメインです。 次のレジストリ設定、NPS が提供するドメイン名を指定できます。

    
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\RasMan\PPP\ControlProtocols\BuiltIn\DefaultDomain
    

>[!CAUTION]
>レジストリを誤って編集すると、システムに重大な障害をもたらす可能性があります。 レジストリを変更する前に、コンピューター上の重要なデータのバックアップを作成する必要があります。

一部の Microsoft 以外のネットワーク アクセス サーバーでは、削除またはユーザーによって指定されたドメイン名を変更します。 その結果、ネットワーク アクセス要求は、ユーザーのアカウントのドメインができない可能性がある既定のドメインに対して認証されます。 この問題を解決するには、正確なドメイン名を持つ正しい形式でユーザー名を変更するのには、RADIUS サーバーを構成します。