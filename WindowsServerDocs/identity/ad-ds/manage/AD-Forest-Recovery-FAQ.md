---
title: "AD フォレストの回復のよく寄せられる質問"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: ac9e5a3d-8b1e-41b7-8e02-f64b7acf1359
ms.technology: identity-adfs
ms.openlocfilehash: 839e01c88b7ced22501154d8752c6c71cc52b696
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---faq"></a>AD フォレストの回復のよく寄せられる質問

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 と 2008 R2、Windows Server 2003 の適用対象:

このドキュメントには、フォレストの回復に関するよく寄せられる質問 (Faq) が含まれています。  
 
## <a name="general-recovery"></a>一般的な回復
  
 
**Q: すれば回復を高速化するか。** 
 
回復の速度がこのガイドの主な目的ではありませんが、回復時間を短縮を実現できます。  
  
-   定期的に更新して、その適正なサイズのシミュレートされたテスト環境で 1 年間に少なくとも 1 回、詳細なフォレストの回復計画を作成します。  
  
-   仮想化ドメイン コントローラー (DC) の複製を使用してください。  
  
     仮想化 DC の複製には、いずれかの DC が各ドメインでのバックアップから復元された後に実行しているその他の Dc を取得するプロセスが見込まれます。 待機時間がかかる可能性がある AD DS のインストールを完了するのではなく、インストール後に、重大でないレプリケーションが完了するの他の仮想化 Dc を複製することができます。  
  
     仮想 Dc がホストされている場所で適切に接続されたデータ センターの数が比較的少ない可能性のあるフォレストは、回復中に複製を最大限に活用します。 ただし、あらゆる環境が、同じドメイン用の複数の仮想化 Dc 併置同じハイパーバイザー ホストであるような利点必要があります。  
  
-   読み取り専用ドメイン コントローラー (Rodc) を展開します。  
  
     Rodc が書き込み可能な Dc と同じように、ネットワークから切断するがあるないために、回復プロセス中に業務の継続性を提供できます。 Rodc は、出力方向のレプリケーションを実行しません。 そのため、それらを提示しないを回復した環境に有害なデータをレプリケートする書き込み可能ドメイン コントローラーとなる同じリスクです。  
  
 フォレストの回復プロセス中に影響するその他の要因は次のとおりです。  
  
-   Dc をバックアップから復元するときにかかる時間。  
  
    -   テープなど、物理的なバックアップ メディアを見つけます。  
  
    -   オペレーティング システムを再インストールします。  
  
    -   バックアップ メディアからのデータを復元します。  
  
     オペレーティング システムを再インストールし、システム状態の復元ではなくサーバーの完全回復を実行することで、バックアップからデータを復元に必要な時間を減らすことができます。 サーバーの完全回復は、バイナリ ベースであるためが完了するとシステム状態の復元よりもはるかに短時間。  
  
     ただし、サーバーに復元したくないシステム状態のデータから除外されているデータが含まれている場合は、サーバーの完全回復できない可能性がありますシステム状態の復元に対する実用的な代替します。 具体的には、サーバーのシステム状態の復元ではなくサーバーの完全回復の実行の利点を検討し、それに従ってを準備する、適切な種類の後で復元するバックアップを実行することでします。  
  
-   Dc を再構築するときに、ネットワーク ベースの昇格のデータをレプリケートする時間がかかります。  
  
 次の手順を実行してドメイン コントローラーを復元するために必要な時間を短縮できます。  
  
-   バックアップ メディアを取得するための時間を短縮するには。  
  
    -   Active Directory データベースのマウント ツール (Dsamain.exe) を使用して、復元操作に使用する最適なバックアップを指定します。 ツールを使用して、Active Directory データベースのマウントの詳細については、次を参照してください。、[Active Directory データベースのマウント ツール Step-by-Step Guide](https://go.microsoft.com/fwlink/?LinkId=132577) (https://go.microsoft.com/fwlink/?LinkId=132577)。  
  
    -   バックアップ メディアを明確にラベル付けと、便利で組織的にメディアを保存するまだ安全な場所に高速の取得を許可します。  
  
    -   記憶域エリア ネットワーク (SAN) とボリューム シャドウ コピー サービスを使用して、時間内のさまざまな時点からのバックアップを管理します。 詳細については、次を参照してください。[Windows Server 2003 Active Directory 高速回復ボリューム シャドウ コピー サービスと仮想ディスク サービス](https://go.microsoft.com/fwlink/?LinkId=70781)(https://go.microsoft.com/fwlink/?LinkId=70781)。  
  
-   オペレーティング システムの再インストールではなく Dc から AD DS の削除を強制します。 純粋な AD DS のスコープ内にある、フォレスト全体のエラーの原因を識別した場合、Dc のオペレーティング システムを再インストールするはありません。  
  
     2008 またはそれ以降は、Windows Server を実行している DC から AD DS の削除を強制の詳細については、次を参照してください。[Windows Server 2008 ドメイン コントローラーの強制的な削除](https://go.microsoft.com/fwlink/?LinkId=132627)(https://go.microsoft.com/fwlink/?LinkId=132627)。 Windows Server 2003 を実行している DC から AD DS の削除を強制の詳細については、次を参照してください。[記事 332199](https://go.microsoft.com/fwlink/?LinkId=70780)で、Microsoft サポート技術情報 (https://go.microsoft.com/fwlink/?LinkId=70780)。  
  
-   高速なテープ デバイスを使用してまたはの必要な時間を短縮するディスク バックアップの復元操作します。  
  
 各ドメイン内の Dc を再構築するメディア (IFM) 機能からのインストールを使用して AD DS のインストールを促進することができます。 IFM は、各ドメイン内の Dc を再構築するときに発生したレプリケーションの待機時間を削減できます。  
  
 積極的なサービス レベル アグリーメント (SLA) の企業では、迅速な回復にフォレストの回復の手順を変更することを検討してください。  
  

**Q: フォレストの回復プロセスを自動化するできますか。**  
 複雑なと重大の性質、フォレストの回復プロセス、現在はありません、エンド ツー エンドの自動化します。 フォレストの回復プロセスは、運用および組織のプロセスの自動化の技術的な問題よりもビジネス継続性を復元する課題よりです。 そのため、環境を管理している個人はその環境に固有であるフォレスト回復計画を作成し、正常に自動化できるセクションを自動化し、必要があります。  
  
 コマンド ライン ツールを使用して、ほとんどのフォレストの回復の手順を実行できます。 そのため、ほとんどの手順は、スクリプト可能なです。 たとえば、Ntdsutil.exe はフォレストの回復プロセスで最もよく使用されるツールの 1 つです。  
  
 スクリプトには、回復が高速化できますが実際の環境を適用する前にこれらのスクリプトを十分にテストする必要があります。 また、Active Directory 環境内の新しいドメインまたは DC の追加や新しいバージョンの Active Directory などの変化に応じて更新する必要があります。

## <a name="next-steps"></a>次の手順
-   [AD フォレストの回復の前提条件](AD-Forest-Recovery-Prerequisties.md)  
-   [AD フォレストの回復 - カスタム フォレスト回復計画を立てる](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD フォレストの回復 - 問題の特定](AD-Forest-Recovery-Identify-the-Problem.md)
-   [AD フォレストの回復 - を回復する方法を決定します。](AD-Forest-Recovery-Determine-how-to-Recover.md)
-   [AD フォレストの回復 - 最初の回復を実行](AD-Forest-Recovery-Perform-initial-recovery.md)  
-   [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)  
-   [AD フォレストの回復のよく寄せられる質問](AD-Forest-Recovery-FAQ.md)  
-   [AD フォレストの回復であれば、マルチ ドメイン フォレスト内で 1 つのドメインの回復](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
-   [AD フォレストの回復 - Windows Server 2003 ドメイン コントローラーとフォレストの回復](AD-Forest-Recovery-Windows-Server-2003.md)  