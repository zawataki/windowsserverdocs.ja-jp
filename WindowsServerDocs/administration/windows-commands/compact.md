---
title: compact
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 429b3752-df0a-43a4-a210-df2f3ad03c3b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5e73369d69912437875a0151b1d9cfcfc85a30da
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379183"
---
# <a name="compact"></a>compact



NTFS パーティション上のファイルまたはディレクトリの圧縮を表示または変更します。 パラメーターを指定せずに使用した場合、現在のディレクトリとそれに含まれているファイルの圧縮状態**が表示されます**。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
compact [/c | /u] [/s[:<Dir>]] [/a] [/i] [/f] [/q] [<FileName>[...]]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/c|指定したディレクトリまたはファイルを圧縮します。|
|/u|指定したディレクトリまたはファイルの圧縮を解除します。|
|/s [: \<Dir >]|指定されたディレクトリのすべてのサブディレクトリ (指定されていない場合は、現在のディレクトリ) に**compact**コマンドを適用します。|
|/a|非表示またはシステムファイルを表示します。|
|/i|エラーを無視します。|
|/f|指定したディレクトリまたはファイルの圧縮または圧縮解除を強制的に実行します。 **/f**は、システムのクラッシュによって操作が中断されたときに部分的に圧縮されたファイルの場合に使用されます。 ファイル全体を強制的に圧縮するには、 **/c**および **/f**パラメーターを使用して、部分的に圧縮されたファイルを指定します。|
|/q|最も重要な情報のみを報告します。|
|\<ファイル名 >|ファイルまたはディレクトリを指定します。 複数の **&#42;** ファイル名、およびとを使用でき**ます。** ワイルドカード文字。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>コメント

-   **Compact**コマンドは、NTFS ファイルシステム圧縮機能のコマンドラインバージョンです。 ディレクトリの圧縮状態は、ファイルがディレクトリに追加されたときに自動的に圧縮されるかどうかを示します。 ディレクトリの圧縮状態を設定しても、必ずしもディレクトリに既に存在するファイルの圧縮状態が変更されるわけではありません。
-   ドライブドライブまたは DoubleSpace を使用して圧縮されたボリュームの読み取り、書き込み、またはマウントに**compact**を使用することはできません。
-   **Compact**を使用してファイルアロケーションテーブル (FAT) または FAT32 パーティションを圧縮することはできません。

## <a name="BKMK_examples"></a>例

現在のディレクトリ、そのサブディレクトリ、および既存のファイルの圧縮状態を設定するには、次のように入力します。
```
compact /c /s 
```
現在のディレクトリ内のファイルとサブディレクトリの圧縮状態を設定するには、次のように入力します。
```
compact /c /s *.*
```
ボリュームを圧縮するには、ボリュームのルートディレクトリから次のように入力します。
```
compact /c /i /s:\
```

> [!NOTE]
> この例では、すべてのディレクトリ (ボリューム上のルートディレクトリを含む) の圧縮状態を設定し、ボリューム上のすべてのファイルを圧縮します。 **/I**パラメーターを指定すると、エラーメッセージによって圧縮プロセスが中断されません。

¥ Tmp ディレクトリにあるファイル名拡張子が .bmp のすべてのファイルと、\ tmp のすべてのサブディレクトリにあるすべてのファイルを圧縮するには、次のように入力します。
```
compact /c /s:\tmp *.bmp
```
システムクラッシュ中に部分的に圧縮されたファイルゼブラの完全な圧縮を強制的に実行するには、次のように入力します。
```
compact /c /f zebra.bmp
```
圧縮された属性をディレクトリ C:\ Tmp から削除するには、そのディレクトリ内のファイルの圧縮状態を変更せずに、次のように入力します。
```
compact /u c:\tmp
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)