---
ms.assetid: 663a2482-33d1-4c19-8607-2e24eef89fcb
title: "フェデレーション サーバー ファームが WID を使用します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: bb4e5f88f3d62511b185a2b4317416169717c860
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="federation-server-farm-using-wid"></a>フェデレーション サーバー ファームが WID を使用します。

>適用対象: Windows Server 2012

Active Directory フェデレーション サービス \(AD FS\) の既定のトポロジは、最大で 5 つのフェデレーション サーバーが、組織のフェデレーション サービスをホストしているので構成される Windows Internal Database \(WID\) を使用して、フェデレーション サーバー ファームです。 このトポロジでは、AD FS は、そのファームに参加しているすべてのフェデレーション サーバーの AD FS 構成データベースのストアとして WID を使用します。 ファームでは、レプリケートし、ファーム内の各サーバー間で、構成データベース内のフェデレーション サービス データを保持します。  
  
ファームに最初のフェデレーション サーバーを作成するには、新しいフェデレーション サービスも作成します。 AD FS 構成データベースの WID を使用する場合、ファームで作成した最初のフェデレーション サーバーと呼びます、*プライマリ フェデレーション サーバー*します。 これは、このコンピューターに AD FS 構成データベースの読み取り/書き込みコピーで構成されていることを意味します。  
  
このファーム用に構成するその他のすべてのフェデレーション サーバーと呼びます*セカンダリ フェデレーション サーバー*ためがローカルに格納する AD FS 構成データベースの読み取り専用コピーにプライマリ フェデレーション サーバーに対して行われた変更をレプリケートする必要があります。  
  
> [!NOTE]  
> 少なくとも 2 台のフェデレーション サーバー load\ 分散構成で使用することをお勧めします。  
  
## <a name="deployment-considerations"></a>展開に関する考慮事項  
このセクションでは、対象となるユーザー、利点、およびこの展開トポロジに関連付けられている制限事項についてさまざまな考慮事項について説明します。  
  
### <a name="who-should-use-this-topology"></a>このトポロジを使用している必要がありますか。  
  
-   組織で 100 台以下の構成済みの信頼関係を内部ユーザーを提供する必要がある \ (企業ネットワークに物理的に接続されているコンピューターにログオン) 単一 sign\ で \(SSO\) アクセス権を持つ、フェデレーション アプリケーションまたはサービス  
  
-   ユーザーに提供するその内部 SSO アクセス権を持つ Microsoft Online Services または Microsoft Office 365 に組織  
  
-   冗長なでスケーラブルなサービスを必要とする小規模な組織  
  
> [!NOTE]  
> 大規模なデータベースを使用する組織は、使用を検討する必要があります、[フェデレーション サーバー ファームを使用して SQL Server](Federation-Server-Farm-Using-SQL-Server.md)展開トポロジは、このセクションで後から説明します。 ネットワークの外部からログイン ユーザーと組織では、いずれかを使用して検討してください、[フェデレーション サーバー ファームを使用して WID とプロキシ](Federation-Server-Farm-Using-WID-and-Proxies.md)トポロジまたは[フェデレーション サーバー ファームを使用して SQL Server](Federation-Server-Farm-Using-SQL-Server.md)トポロジです。  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>このトポロジを使用する利点は何ですか。  
  
-   内部ユーザーへの SSO アクセスを提供します。  
  
-   データとフェデレーション サービスの冗長性 \ (各フェデレーション サーバーは、同じ farm\ 内の他のフェデレーション サーバーに変更をレプリケート)  
  
-   ファームをスケール アウトをする最大で 5 つのフェデレーション サーバーを追加します。  
  
-   WID の Windows に含まれるそのため、必要がない SQL Server を購入するには  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>このトポロジを使用する場合の制限事項とは何ですか。  
  
-   WID ファームには 5 台のフェデレーション サーバーに制限します。 詳細については、次を参照してください。[AD FS 展開トポロジに関する考慮事項](AD-FS-Deployment-Topology-Considerations.md)します。  
  
-   WID ファームはトークン リプレイ検出またはアーティファクトの解像度をサポートしていない \ (Security Assertion Markup Language \(SAML\) protocol\ の一部)。  
  
## <a name="server-placement-and-network-layout-recommendations"></a>サーバーの配置とネットワーク レイアウトの推奨事項  
このトポロジで、ネットワークの展開を開始する準備ができたら、専用のクラスターのドメイン ネーム システム \(DNS\) 名とクラスター IP アドレスを使用した NLB クラスターの構成可能なネットワーク負荷分散 \(NLB\) ホストの背後にある企業ネットワーク内のすべてのフェデレーション サーバーを配置するように計画してください。  
  
> [!NOTE]  
> このクラスター DNS 名は、フェデレーション サービス名、たとえば、fs.fabrikam.com と一致する必要があります。  
  
NLB ホストは、クライアントの要求を個々 のフェデレーション サーバーを割り当てるには、この NLB クラスターで定義されている設定を使用できます。 次の図は、架空の企業で Fabrikam, inc. が定めたが two\ コンピューターのフェデレーション サーバー ファームを使用してその展開の最初のフェーズをセットアップする方法を示しています。\(fs1 and fs2\) WID と DNS サーバーと、企業ネットワークに配線されている 1 台の NLB ホストの配置します。  
  
![サーバー ファームが WID を使用します。](media/FarmWID.gif)  
  
> [!NOTE]  
> この単一の NLB ホストに障害がある場合は、ユーザーはフェデレーション アプリケーションまたはサービスにアクセスできません。 お客様のビジネス要件は単一障害点の発生を許可していない場合は、別の NLB ホストを追加します。  
  
フェデレーション サーバーで使用するため、ネットワーク環境を構成する方法の詳細については、次を参照してください。[フェデレーション サーバーの名前解決要件](Name-Resolution-Requirements-for-Federation-Servers.md)AD FS 設計ガイドにします。  
  
## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)