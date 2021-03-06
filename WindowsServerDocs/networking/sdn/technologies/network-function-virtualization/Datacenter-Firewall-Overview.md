---
title: Datacenter Firewall の概要
description: このトピックでは、Windows Server 2016 のネットワーク層、5タプル (プロトコル、発信元と宛先の IP アドレス、送信元と送信先の IP アドレス)、ステートフル、マルチテナントファイアウォールのデータセンターのファイアウォールについて説明します。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 67576533-206b-428a-956c-ed8c53218d9b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9562972f731a553dbc3e5558fcce1d5c51d539d0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405884"
---
# <a name="datacenter-firewall-overview"></a>Datacenter Firewall の概要

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

データセンターのファイアウォールは、Windows Server 2016 に含まれる新しいサービスです。 これは、ネットワーク層、5組 (プロトコル、発信元と宛先のポート番号、送信元と送信先の IP アドレス)、ステートフル、マルチテナントファイアウォールです。 テナント管理者は、サービスプロバイダーによってサービスとして展開され、サービスとして提供されると、インターネットおよびイントラネットネットワークからの不要なトラフィックから仮想ネットワークを保護するために、ファイアウォールポリシーをインストールして構成することができます。  
  
![ネットワークスタックのデータセンターのファイアウォール](../../../media/Datacenter-Firewall-Overview/MultitenantFirewallOverview2.png)  
  
サービスプロバイダー管理者またはテナント管理者は、ネットワークコントローラーと northbound Api を使用してデータセンターのファイアウォールポリシーを管理できます。  
  
データセンターのファイアウォールには、クラウドサービスプロバイダーに関して次のような利点があります。  
  
-   テナントに提供できる、拡張性が高く、管理しやすい、関連のソフトウェアベースのファイアウォールソリューション  
  
-   テナントのファイアウォールポリシーを破壊することなく、テナントの仮想マシンを別のコンピューティングホストに移動する自由度  
  
    -   VSwitch ポートホストエージェントファイアウォールとして展開されます。  
  
    -   テナント仮想マシンは、vSwitch ホストエージェントファイアウォールに割り当てられているポリシーを取得します。  
  
    -   ファイアウォール規則は、仮想マシンを実行している実際のホストに依存しない、各 vSwitch ポートで構成されます。  
  
-   テナントのゲストオペレーティングシステムとは独立して、テナントの仮想マシンの保護を提供します。  
  
データセンターのファイアウォールには、テナントに対して次のような利点があります。  
  
-   仮想ネットワーク上のインターネットに接続するワークロードを保護するためにファイアウォール規則を定義する機能  
  
-   同じ L2 仮想サブネット上の仮想マシン間および異なる L2 仮想サブネット上の仮想マシン間のトラフィックを保護するためにファイアウォール規則を定義する機能  
  
-   サービスプロバイダーでテナントのオンプレミスネットワークと仮想ネットワーク間のネットワークトラフィックを保護および分離するためのファイアウォール規則を定義する機能  
  


