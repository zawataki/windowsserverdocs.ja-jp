---
ms.assetid: d04dd17e-a843-46fd-8711-0039918f92d9
title: AD FS 設計計画の実装
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 31c2e048c3c125d0ea60610b049501151d7aa823
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830783"
---
# <a name="implementing-your-ad-fs-design-plan"></a>AD FS 設計計画の実装

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

次の環境の条件と要件は、Active Directory フェデレーション サービスの実装で重要な要因\(AD FS\)設計計画。  
  
-   **サポートされているパートナー:** 通常は、AD FS を使用するには、パートナー組織を使用します。 Id フェデレーションを確立するには、パートナーシップを形成する組織を決定します。 パートナーの追加、パートナーを削除およびパートナー情報を更新、ベースライン AD FS の展開ができたら、パートナーで動作があります。 さまざまな理由からパートナーシップへの変更があります。 たとえば、AD FS 展開必要がありますパートナーシップの更新プログラム、パートナーのビジネスを大幅に変更より大きな組織または組織のフェデレーションの一部となり、組織または組織が異なるによって取得された場合会社です。 複数のドメインからの id の統合をどのようなシナリオで、ドメインを確認する必要があります\(パートナー\)をサポートしていると潜在的なパートナーを表すすべての追加ドメイン。  
  
-   **サポートされているアプリケーションとサービスの種類:**「要求に注意してください」は、他のユーザーにオペレーティング システムのリソースへのアクセスを必要と、一部のアプリケーションとサービス アプリケーションと AD FS をサポートするため、管理の要件を策定するサービスの種類を理解しておく必要があります。  
  
-   **論理および物理アーキテクチャの図またはデプロイ トポロジ:** 知る必要があります。  
  
    -   かどうかのフェデレーション サーバーは、一連のファームのサーバーまたは単一のサーバー上で機能します。  
  
    -   場所、ネットワークは、ファイアウォールとプロキシをデプロイします。  
  
    -   リソースとユーザーは、組織、組織、または両方の外部から、リソースにアクセスするかどうかの場所。  
  
## <a name="how-to-implement-your-ad-fs-design-using-this-guide"></a>このガイドを使用して AD FS 設計を実装する方法  
次の手順で、設計の実装では、どのような順序で各展開のタスクを実行する必要がありますを決定します。 このガイドでは、チェックリストを使用して、設計計画を実装するために必要となるさまざまなサーバーやアプリケーションの展開タスクを順を追って進めることができます。 親と子チェックリストは、特定の AD FS のタスクでは、デザインを処理する必要があります、順序を表すためには必要に応じて使用されます。  
  
組織の推奨される AD FS 設計の実装の展開タスクを慣れてガイドのこのセクションでは、次の親チェックリストを使用します。  
  
-   [チェックリスト:Web SSO 設計の実装](Checklist--Implementing-a-Web-SSO-Design.md)  
  
-   [チェックリスト:フェデレーション Web SSO 設計の実装](Checklist--Implementing-a-Federated-Web-SSO-Design.md)  