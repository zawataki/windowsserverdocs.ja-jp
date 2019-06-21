---
ms.assetid: eb600904-24b8-4488-a278-c1c971dc2f2d
title: 地域ドメイン コント ローラーの配置の計画
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: bec8595ab6eae8eb6cedaf9307ab97ac9c8316b8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880443"
---
# <a name="planning-regional-domain-controller-placement"></a>地域ドメイン コント ローラーの配置の計画

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

コスト効率のためには、できるだけ少ないの地域別のドメイン コント ローラーを配置する予定です。 最初に、確認で使用される「地理的な場所との通信リンク」(DSSTOPO_1.doc) ワークシート [ネットワーク情報の収集](../../ad-ds/plan/Collecting-Network-Information.md) 場所がハブであるかどうかを確認します。  
  
各ハブ上の場所で表されるドメインごとに地域ドメイン コント ローラーを配置する予定です。 すべての拠点で地域ドメイン コント ローラーを配置した後は、サテライト オフィスに地域別のドメイン コント ローラーを配置することの必要性を評価します。 サテライト オフィスから不要な地域ドメイン コント ローラーを排除することと、リモート サーバー インフラストラクチャを保守するために必要なサポート コストが削減されます。  
  
未承認の人物がアクセスできないように、ハブとサテライトの場所にドメイン コント ローラーの物理的なセキュリティがさらを確認します。 書き込み可能なドメイン コント ローラーがドメイン コント ローラーの物理的なセキュリティを保証できないハブおよびサテライトの場所に置かないでください。 書き込み可能なドメイン コント ローラーに物理的にアクセスを持っているユーザーでシステムを攻撃できます。  
  
- ドメイン コント ローラーで別のオペレーティング システムを起動して、物理ディスクにアクセスします。  
- ドメイン コント ローラーに物理ディスクを削除する (および置換可能性があります)。  
- 取得して、ドメイン コント ローラーのシステム状態バックアップのコピーの操作です。  
  
物理的なセキュリティを保証できる場所にのみ書き込み可能な地域ドメイン コント ローラーを追加します。  
  
物理的なセキュリティを不適切な場所に読み取り専用ドメイン コント ローラー (RODC) を展開するには、推奨されるソリューションです。 RODC は、アカウント パスワードを除いて、すべての Active Directory オブジェクトと、書き込み可能なドメイン コント ローラーを保持する属性を保持します。 ただし、RODC に格納されているデータベースに変更を行うことはできません。 変更は、書き込み可能なドメイン コント ローラーに対して実行され、RODC にレプリケートされるする必要があります。  
  
クライアントのログオンとローカル ファイル サーバーへのアクセスを認証には、ほとんどの組織は、特定の場所で表されているすべての地域ドメインの地域別のドメイン コント ローラーを配置します。 ただし、事業所がそのクライアントのローカル認証する必要がありますか、クライアントがワイド エリア ネットワーク (WAN) リンク経由で認証とクエリに依存できるかどうかを評価するときに、多数の変数を考慮する必要があります。 次の図は、サテライト オフィスにドメイン コント ローラーを配置するかどうかを決定する方法を示します。  
  
![プランの地域の dc の配置](media/Planning-Regional-Domain-Controller-Placement/49892c8c-2c99-4aab-92ba-808dbc8048e2.gif)  
  
## <a name="onsite-technical-expertise-availability"></a>オンサイトの技術的な専門知識の可用性

ドメイン コント ローラーは、さまざまな理由で継続的に管理する必要があります。 地域ドメイン コント ローラーをドメイン コント ローラーを管理したり、ドメイン コント ローラーをリモートで管理できることを確認する担当者が含まれている場所でのみ配置します。  
  
不適切な通常の物理的なセキュリティとブランチ オフィス環境およびほとんどの情報テクノロジの知識を持つ担当者で RODC を展開する、推奨されるソリューションでは多くの場合です。 RODC のローカルの管理アクセス許可は、ドメインまたはその他のドメイン コント ローラーに対するユーザー権利をそのユーザーに付与されません任意のドメイン ユーザーに委任できます。 これにより、ローカル ブランチ ユーザーが RODC にログオンし、ドライバーをアップグレードするなど、サーバーでメンテナンスを実行できます。 ただし、ブランチ ユーザーはその他のドメイン コント ローラーにログオンまたはドメイン内の他の管理タスクを実行できません。 この方法で、ブランチ ユーザーができる他のドメインやフォレストのセキュリティを損なうことがなく、ブランチ オフィスで RODC を効果的に管理する権限が委任します。  
  
## <a name="wan-link-availability"></a>WAN リンクの可用性

頻繁に障害が発生する WAN リンクが生産性を大幅失われることをユーザーに場所にユーザーを認証できるドメイン コント ローラーが含まれていない場合。 WAN リンク可用性は、100%、リモートのサイトは、サービスの停止を許容できない場合は、ユーザーがログオンまたは WAN リンクがダウンしたときに、サーバーへのアクセスを交換する機能を必要とする場所に地域別のドメイン コント ローラーを配置します。  
  
## <a name="authentication-availability"></a>認証の可用性

銀行などの特定の組織では、常にユーザーを認証することが必要です。 地域ドメイン コント ローラーを WAN リンクの状況が 100% の場所に置きますが、ユーザーが常に認証を必要とします。  
  
## <a name="logon-performance-over-wan-links"></a>WAN リンク経由のログオンのパフォーマンス

WAN リンクの可用性が信頼性の高い場合はドメイン コント ローラーを配置する場所に、WAN リンク経由で、ログオンのパフォーマンス要件に依存します。 WAN 経由でログオンのパフォーマンスに影響を与える要因は、リンク速度と利用可能な帯域幅は、ユーザーと使用状況のプロファイル、およびレプリケーション トラフィックではなくログオン ネットワーク トラフィックの量の番号。  
  
### <a name="wan-link-speed-and-bandwidth-utilization"></a>WAN リンクの速度と帯域幅の使用率

1 人のユーザーのアクティビティは、低速の WAN リンクを congest ことができます。 WAN リンク経由でログオンのパフォーマンスが許容されない場合は、ドメイン コント ローラーを場所に配置します。  
  
帯域幅の使用率の割合の平均値では、ネットワーク リンクは、混雑している方法を示します。 ネットワーク リンクの帯域幅の平均使用率が、有効な値より大きい場合は、その場所でドメイン コント ローラーを配置します。  
  
### <a name="number-of-users-and-usage-profiles"></a>ユーザーと使用状況のプロファイルの数

ユーザーと指定の場所に、使用状況のプロファイルの数は、その位置に地域別のドメイン コント ローラーを配置するかどうかを判断するのに役立ちます。 生産性の損失を避けるためには、WAN リンクに失敗した場合に、100 以上のユーザーのある場所に地域ドメイン コント ローラーを配置します。  
  
使用状況のプロファイルでは、ユーザーがネットワーク リソースを使用する方法を示しています。 ドメイン コント ローラーをネットワーク リソースに頻繁にアクセスしない少数のユーザーのみがある場所に配置する必要はありません。  
  
### <a name="logon-network-traffic-vs-replication-traffic"></a>レプリケーションのトラフィックとネットワーク トラフィックのログオン

ドメイン コント ローラーが、Active Directory クライアントと同じ場所内で使用できない場合、クライアントは、ネットワークにログオン トラフィックを作成します。 物理ネットワーク上に作成されたログオン ネットワーク トラフィックの量はグループのメンバーシップのようないくつかの要因によって影響を受けるグループ ポリシー オブジェクト (Gpo); の数とサイズログオン スクリプトです。オフライン フォルダー、フォルダー リダイレクトおよび移動プロファイルなどの機能です。  
  
これに対して、指定の場所に配置されているドメイン コント ローラーは、ネットワーク上のレプリケーション トラフィックを生成します。 頻度とドメイン コント ローラーでホストされているパーティションに対する更新プログラムの量は、ネットワーク上に作成されたレプリケーション トラフィックの量に影響します。 ドメイン コント ローラーでホストされているパーティション上に作成できる更新プログラムのさまざまな種類には、追加やユーザーおよびユーザー属性を変更する、パスワードを変更してを追加するまたはグローバル グループ、プリンター、またはボリュームの変更が含まれます。  
  
地域ドメイン コント ローラーを場所に配置する必要があるかどうかを判断するには、位置、ドメイン コント ローラーを配置することによって作成されたレプリケーション トラフィックのコストとドメイン コント ローラーの場所で作成されたログオン トラフィックのコストを比較します。  
  
たとえば、本社と低速リンクを介して接続されているブランチ オフィスのあるネットワークを考慮し、どのドメイン コント ローラーを追加できる簡単にします。 毎日ログオンおよびディレクトリ検索のトラフィックをリモート サイト ユーザーが、いくつかの分岐にすべての会社のデータをレプリケートするよりもネットワーク トラフィックが多く発生すると、ブランチ オフィスにドメイン コント ローラーの追加を検討してください。  
  
ドメイン コント ローラーを維持するためのコストの削減がネットワーク トラフィックより重要な場合は、そのドメインのドメイン コント ローラーを集中管理ししない位置に、地域別のドメイン コント ローラーを配置するか場所に Rodc を配置することを検討してください。  
  
地域ドメイン コント ローラーと各場所で表される各ドメインのユーザー数の配置を文書化するために、ワークシートでは、次を参照してください[ジョブ エイドの Windows Server 2003 展開キット](https://go.microsoft.com/fwlink/?LinkID=102558)、Job_ のダウンロード。Aids_Designing_and_Deploying_Directory_and_Security_Services.zip、および開いている「ドメイン コント ローラー配置」(DSSTOPO_4.doc)。  
  
地域ドメインを展開するときに、地域別のドメイン コント ローラーを配置する必要がある場所に関する情報を参照する必要があります。 地域ドメインの展開に関する詳細については、次を参照してください。 [を展開する Windows Server 2008 地域ドメイン](https://technet.microsoft.com/library/cc755118.aspx)します。  