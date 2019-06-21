---
ms.assetid: 19feca0e-a6d0-4d27-93b0-cb44f8c26484
title: アカウント OU とリソース OU の管理を委任する
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 70900b44de85774e8e595f9691885d67682fa753
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834263"
---
# <a name="delegating-administration-of-account-ous-and-resource-ous"></a>アカウント OU とリソース OU の管理を委任する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

アカウント組織単位 (Ou) には、ユーザー、グループ、およびコンピューター オブジェクトが含まれます。 リソース Ou には、リソースとそれらのリソースを管理する責任を持っているアカウントが含まれます。 フォレストの所有者はこれらのオブジェクトとリソースを管理する OU 構造の作成と OU の所有者にその構造の制御を委任します。  
  
## <a name="delegating-administration-of-account-ous"></a>アカウント Ou の管理を委任します。  
ユーザー、グループ、およびコンピューター オブジェクト作成および変更する必要がある場合は、アカウント OU 構造をデータ管理者に委任します。 アカウント OU 構造は、各アカウントの種類にない個別に制御する必要がありますには、Ou のサブツリーです。 たとえば、OU の所有者は、アカウント OU のユーザー、コンピューター、グループ、およびサービス アカウント内の子 Ou に、さまざまなデータ管理者に特定のコントロールを委任できます。  
  
次の図は、アカウント OU 構造の 1 つの例を示します。  
  
![管理を委任します。](media/Delegating-Administration-of-Account-OUs-and-Resource-OUs/66d38fbe-e8eb-42d7-abab-9526243bf6d9.gif)  
  
次の表は、アカウント OU 構造で作成できる使用可能な子 Ou の一覧です。  
  
|OU|目的|  
|------|-----------|  
|Users|管理者以外の担当者のユーザー アカウントが含まれています。|  
|サービス アカウント|ネットワーク リソースへのアクセスを必要とする一部のサービスは、ユーザー アカウントとして実行します。 この OU は、別のサービスのユーザー アカウントを users OU に含まれるユーザー アカウントから作成されます。 、さまざまな種類のユーザー アカウントを個別の Ou に配置することもできますが特定の管理の要件に従ってそれらを管理します。|  
|コンピューター|ドメイン コント ローラー以外のコンピューター アカウントが含まれています。|  
|グループ|管理グループは、個別に管理されている以外のすべての種類のグループが含まれています。|  
|Admins|通常のユーザーは別に管理できるようにアカウント OU 構造でデータ管理者のユーザーおよびグループ アカウントが含まれています。 管理ユーザーおよびグループに変更を追跡するように、この OU の監査を有効にします。|  
  
次の図は、アカウント OU 構造の管理グループの設計の 1 つの例を示します。  
  
![管理を委任します。](media/Delegating-Administration-of-Account-OUs-and-Resource-OUs/be2cd2d2-6956-429c-a53a-369e6fe40b2b.gif)  
  
子 Ou を管理するグループのみを管理する責任があるオブジェクトの特定のクラスに対するフル コントロールが付与されます。  
  
OU 構造内の制御を委任するために使用するグループの種類は、アカウントが  ナェィェ ・管理するのには、OU 構造に基づいています。 管理者のユーザー アカウントと、OU 構造をすべて 1 つのドメイン内に存在、委任を使用して作成したグループがグローバル グループにあります。 組織の部門は、独自のユーザー アカウントを管理し、1 つ以上の地理的リージョン内に存在する場合は、アカウントは、複数のドメイン内の Ou の管理を担当するデータ管理者のグループがあります。 すべてのデータ管理者のアカウントが 1 つのドメインに存在する制御を委任する必要があります。 複数のドメインに OU 構造がある場合は、これらの管理者アカウントのグローバル グループのメンバーを作成および各 OU 構造の制御を委任これらのグローバル グループにドメイン。 複数のドメインからのデータの管理者アカウントを OU 構造の制御を委任する場合は、ユニバーサル グループを使用する必要があります。 ユニバーサル グループが別のドメインからユーザーを含めることができ、したがって、複数のドメイン内の制御を委任する使用することができます。  
  
## <a name="delegating-administration-of-resource-ous"></a>リソース Ou の管理を委任します。  
リソース Ou を使用して、リソースへのアクセスを管理できます。 リソース OU の所有者は、ファイル共有、データベース、およびプリンターなどのリソースを含む、ドメインに参加しているサーバーのコンピューター アカウントを作成します。 リソース OU の所有者には、これらのリソースへのアクセスを制御するグループも作成します。  
  
次の図は、リソース OU の 2 つの可能な場所を示します。  
  
![管理を委任します。](media/Delegating-Administration-of-Account-OUs-and-Resource-OUs/6667a5ce-34d6-48a9-9974-b823ba70e2af.gif)  
  
リソース OU を子 OU 管理階層内の対応するアカウント OU の OU またはドメイン ルートの下に配置されていることはできます。 リソース Ou には、すべての標準の子 Ou がありません。 コンピューターおよびグループは、リソース OU に直接配置されます。  
  
リソース OU の所有者は、OU 内のオブジェクトを所有しているが、OU コンテナー自体を所有していません。 リソース OU の所有者は、コンピューターとグループ オブジェクトのみを管理します。オブジェクトは、OU 内の他のクラスを作成することはできませんし、子 Ou を作成できません。  
  
> [!NOTE]  
> 作成者またはオブジェクトの所有者は、親コンテナーから継承されたアクセス許可に関係なくオブジェクトのアクセス制御リスト (ACL) を設定する機能を持っています。 リソース OU の所有者は、OU の ACL をリセットできます、その所有者は、ユーザーを含む、OU 内のオブジェクトの任意のクラスを作成できます。 このため、Ou を作成するリソース OU の所有者が許可されていません。  
  
各リソース ドメイン内の OU には、OU のコンテンツの管理を担当するデータの管理者を表すグローバル グループを作成します。 このグループには、OU 内のグループとコンピューター オブジェクトが OU コンテナー自体ではなく完全に制御します。  
  
次の図は、リソース OU 管理グループの設計を示します。  
  
![管理を委任します。](media/Delegating-Administration-of-Account-OUs-and-Resource-OUs/8a3f7714-a3bf-43f7-b999-6070543248b0.gif)  
  
リソース OU にコンピューター アカウントを配置することが、OU 所有者アカウント オブジェクトを制御、OU 所有者加えません、コンピューターの管理者。 Active Directory ドメインの Domain Admins グループは、既定に配置のすべてのコンピューターのローカルの Administrators グループ。 つまり、サービス管理者には、これらのコンピューター上のコントロールがあります。 リソース OU の所有者は、その Ou 内のコンピューターに対する管理制御権を必要とする場合、フォレストの所有者は、その OU 内のコンピューターで Administrators グループのメンバー リソース OU の所有者にするのに制限されたグループのグループ ポリシーを適用できます。  
  

