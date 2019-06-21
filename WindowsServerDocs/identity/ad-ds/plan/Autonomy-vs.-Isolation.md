---
ms.assetid: ef63d40c-a262-4a18-938d-b95c10680c0b
title: 自律性とします。分離性
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 765a25d3d1ffdb4df473e1fb5bb65e532934aca9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867573"
---
# <a name="autonomy-vs-isolation"></a>自律性とします。分離性

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

次のいずれかを実現するために、Active Directory 論理構造を設計できます。  
  
-   **自律性**します。 リソースの独立したが限定されてコントロールが含まれます。 管理者がリソースを個別に管理する権限を持っていると、自律性を実現します。ただし、ユーザーもこれらのリソースを制御および必要に応じてコントロールを離れたかかることができます、大きい権限を持つ管理者が存在します。 次の種類の自律性を実現するために、Active Directory 論理構造を設計することができます。  
  
    -   **サービスの自律性**します。 この種類自律性にはには、サービス管理のすべてまたは一部の制御が含まれます。  
  
    -   **データの自律性**します。 この種類自律性にはには、ディレクトリまたはディレクトリに参加しているメンバー コンピューターに格納されたデータの一部またはすべての制御が含まれます。  
  
-   **分離**します。 リソースの独立した排他的に制御が含まれます。 分離を実現するときに管理者がリソースを個別に管理権限を持っているし、その他の管理者を取り上げることがないリソースの制御。 次の種類の分離を実現するために、Active Directory 論理構造を設計することができます。  
  
    -   **サービスの分離**します。 (サービス管理の制御を具体的には指定されている管理者) 以外の管理者の制御やサービスの管理に干渉できないようにします。  
  
    -   **データの分離**します。 (以外のコントロールまたはビューのデータを明確に指定されている管理者) の管理者は制御またはディレクトリまたはディレクトリに参加しているメンバー コンピューターは、データのサブセットを表示できなくなります。  
  
自律性のみが必要な管理者では、以上の管理権限を持つ他の管理者は、サービスまたはデータの管理制御以上であるがそのまま使用します。 分離が必要な管理者では、サービスまたはデータの管理を排他的に制御があります。 自律性を実現する設計の作成は、通常の分離を実現するためにデザインを作成するよりも安価です。  
  
Active Directory Domain Services (AD DS)、管理者は、両方のサービスの管理と自律性または組織間の分離を実現するために、データ管理を委任できます。 サービス管理の組み合わせ、組織のデータ管理、自律性、および分離要件管理を委任するために使用する Active Directory コンテナーに影響します。  
  
## <a name="isolation-and-autonomy-requirements"></a>分離と自律性の要件  
展開する必要があるフォレストの数は、組織内のグループごとの自律性と分離要件に基づきます。 フォレスト設計要件を識別するために、組織内のすべてのグループの自律性と分離要件を識別する必要があります。 具体的には、データの分離、データの自律性、サービスの分離、およびサービスの自律性のニーズを特定する必要があります。 組織内の接続が制限の領域を識別することもする必要があります。  
  
### <a name="data-isolation"></a>データの分離  
データの分離には、グループまたはデータを所有している組織でデータを排他的に制御が含まれます。 サービス管理者がデータ管理者の間のリソースを制御する機能があることに注意してください。 重要です。 およびデータ管理者には、サービス管理者が管理しているリソースにアクセスすることを防止する機能はありません。 そのため、組織内の別のグループがサービスの管理を担当は、データの分離を実現できません。 グループには、データの分離が必要とする場合、そのグループにサービスの管理責任を負うものはもします。  
  
データと AD DS に格納されているため、AD DS に参加しているコンピューターをサービス管理者から分離することはできません、完全なデータの分離を実現するために、組織内のグループの唯一の方法は、そのデータの別のフォレストを作成します。 悪意のあるソフトウェア、または、資格情報を持つサービス管理者によって攻撃による影響は多くの組織は、データの分離を実現するために別のフォレストを作成することもできます。 法的な要件は、通常この種類のデータの分離の必要性を作成します。 次に、例を示します。  
  
-   金融機関は、ユーザー、コンピューター、およびそのにいる管理者を特定の管轄区域内のクライアントに属するデータへのアクセスを制限する法律で必要です。 教育機関は、アクセス制限に違反した場合、保護された領域の外部で動作するサービス管理者を信頼するが、教育機関はその管轄区域で事業を行うことできなきます。 そのため、金融機関は、その管轄外のサービス管理者からのデータを切り離す必要があります。 暗号化するには代わりにこのソリューションにはない常に注意してください。 暗号化は、サービス管理者からデータを保護する場合がありますされません。  
  
-   防御者は、ユーザーの指定されたセットにプロジェクトのデータへのアクセスを制限する法律で必要です。 請負業者は、その他のプロジェクトに関連するコンピューター システムを制御するサービス管理者を信頼するが、このアクセス制限に違反には、契約者にビジネスの損失が発生します。  
  
    > [!NOTE]  
    > データ分離要件がある場合は、データ管理者と通常のユーザーから、またはサービス管理者からデータを分離する必要があるかどうかを決める必要があります。 分離要件は、データ管理者と通常のユーザーからの分離に基づいている場合は、データを分離するアクセス制御リスト (Acl) を使用できます。 この設計プロセスのためには、データ管理者と通常のユーザーから分離しても、データ分離要件はありません。  
  
### <a name="data-autonomy"></a>データの自律性  
データの自律性には、データに関する管理の決定を行う別の機関からの承認を必要としない場合は、必要な管理タスクを実行するなど、独自のデータを管理するグループまたは組織の機能が含まれます。  
  
データの自律性は、データへのアクセスをフォレスト内のサービス管理者を妨げません。 たとえば、大規模な組織の研究グループは、自体のプロジェクトに固有のデータを管理できるようにするが、フォレスト内の他の管理者からのデータをセキュリティで保護する必要はありません。  
  
### <a name="service-isolation"></a>サービスの分離  
サービスの分離には、Active Directory インフラストラクチャの排他的制御が含まれます。 サービスの分離が必要なグループでは、こと、グループ外の管理者はディレクトリ サービスの操作に干渉できないが必要です。  
  
運用上または法律上の要件は、通常サービスの分離の必要性を作成します。 例:  
  
-   製造会社が工場フロアの機器を制御する重要なアプリケーションをしています。 組織のネットワークの他の部分で、サービスの中断を許可して、工場フロアの操作に干渉することはできません。  
  
-   ホスティング企業は、複数のクライアントにサービスを提供します。 各クライアントでは、1 台のクライアントに影響するサービスの中断では、他のクライアントには影響しませんが、サービスの分離が必要です。  
  
### <a name="service-autonomy"></a>サービスの独立性  
サービスの自律性にし、不要の排他的制御; インフラストラクチャを管理する機能が含まれますたとえば、グループが場合 (追加、またはドメインを削除する、ドメイン ネーム システム (DNS) 名前空間を変更またはスキーマの変更) などのインフラストラクチャを変更するのにフォレストの所有者の承認なし。  
  
サービスの自律性 (を追加して、必要に応じて、ドメイン コント ローラーを削除する) を AD DS のサービス レベルを制御することを望んでいるグループまたはディレクトリ対応アプリケーションをインストールすることが必要なグループの組織内で必要となる可能性をスキーマの拡張機能が必要です。  
  
## <a name="limited-connectivity"></a>接続が制限  
組織内のグループに制限するか (ファイアウォールやネットワーク アドレス変換 (NAT) デバイス) のネットワーク間の接続を制限しているデバイスで区切られたネットワークが所有している場合、フォレストの設計に影響する可能性です。 フォレスト設計要件を識別するときに必ずネットワーク接続が制限されている場所に注意してください。 この情報は、フォレストの設計に関する決定を有効にする必要があります。  
  

