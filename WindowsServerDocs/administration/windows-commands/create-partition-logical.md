---
title: 論理パーティションを作成します。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1f59b79a-d690-4d0e-ad38-40df5a0ce38e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6b347581773a086d525bb005edeca2efa31e1848
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886053"
---
# <a name="create-partition-logical"></a>論理パーティションを作成します。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既存の拡張パーティションに論理パーティションを作成します。 このコマンドは、マスター ブート レコードにのみ使用できます\(MBR\)ディスク。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
create partition logical [size=<n>] [offset=<n>] [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|サイズ\=<n>|論理パーティションのサイズをメガバイト単位で指定\(MB\)、拡張パーティションよりも小さくする必要があります。 サイズを指定しない場合、パーティションが拡張パーティションの空き領域があるまで続行されます。|  
|オフセット\=<n>|キロバイト単位のオフセットを指定します。 \(KB\)、でパーティションを作成します。 オフセットはシリンダー サイズの使用が完全にいっぱいに丸めます。 オフセットを指定しない場合、パーティションは保持するのに十分な大きさである最初のディスク エクステントで配置されます。 パーティションで指定された数 (バイト単位) を少なくとも限り**サイズ\=<n>** します。 論理パーティションのサイズを指定する場合は、拡張パーティションよりも小さい場合があります。|  
|配置\=<n>|すべてのボリュームまたはパーティション範囲近いシリンダー境界に揃えて配置します。 ハードウェア RAID の論理ユニット番号で通常使用\(LUN\)パフォーマンスを向上させるために配列。  <n> キロバイト数は、 \(KB\)近いシリンダー境界にディスクの先頭から。|  
|noerr|スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|  
  
## <a name="remarks"></a>注釈  
  
-   場合、**サイズ**と**オフセット**パラメーターが指定されていない、拡張パーティションで使用可能な最大ディスク エクステントの論理パーティションを作成します。  
  
-   パーティションが作成された後、フォーカスは自動的に新しい論理パーティションに移動します。  
  
-   この操作を成功させるのには、ベーシック MBR ディスクを選択してください。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。  
  
## <a name="BKMK_examples"></a>例  
選択したディスクの拡張パーティション内のサイズで 1000 メガバイト単位の論理パーティションを作成するには、次のように入力します。  
  
```  
create partition logical size=1000  
```  
  
#### <a name="additional-references"></a>その他の参照  
[コマンドライン構文キー](command-line-syntax-key.md)  
  

  
