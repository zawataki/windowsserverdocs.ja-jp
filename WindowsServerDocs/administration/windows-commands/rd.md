---
title: rd
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 42e672f6-5bc2-4c16-af25-18e7ed2dd555
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a9190a77369c0a4631db87ab5a5c112b13b37e6f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840043"
---
# <a name="rd"></a>rd



ディレクトリを削除します。 このコマンドと同じ、 **rmdir** コマンドです。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
rd [<Drive>:]<Path> [/s [/q]]
rmdir [<Drive>:]<Path> [/s [/q]]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[\<ドライブ >:]<Path>|場所を削除するディレクトリの名前を指定します。 *パス* が必要です。|
|/s|(指定されたディレクトリとすべてのファイルを含むすべてのサブディレクトリ) は、ディレクトリ ツリーを削除します。|
|/q|クワイエット モードを指定します。 ディレクトリ ツリーを削除するときに、確認を表示しません。 (ことに注意 **/q** 場合にのみ、works **/s** が指定されている)。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   含むファイルを格納するディレクトリを削除することはできません隠しファイルやシステム ファイルです。 削除しようとすると、次のメッセージが表示されます。

    `The directory is not empty`

    使用して、 **dir/a**すべてのファイルを一覧表示するコマンド (を含む非表示とシステム ファイル)。 使用して、 **attrib** コマンドに **-h** 隠しファイル属性を削除する **-s** システム ファイルの属性を削除するか、 **-h-s** 削除両方非表示にしてシステム ファイル属性。 非表示の後にファイルの属性が削除されていると、ファイルを削除することができます。
-   円記号を挿入する場合 (\)の先頭に*パス*、*パス*(現在のディレクトリ) に関係なく、ルート ディレクトリで開始されます。
-   使用することはできません **rd** を現在のディレクトリを削除します。 現在のディレクトリを削除しようとすると、次のエラー メッセージが表示されます。

    `The process cannot access the file because it is being used by another process.`

    (いない、現在のディレクトリのサブディレクトリ)、別のディレクトリに変更をし、使用した場合、このエラー メッセージを受信する必要があります**rd** (指定*パス*必要な場合)。
-   **Rd** コマンドで他のパラメーターは、回復コンソールから利用できます。

## <a name="BKMK_examples"></a>例

現在作業中のディレクトリを削除することはできません。 現在のディレクトリ内にないディレクトリに変更する必要があります。 たとえば、親ディレクトリに変更する、次のように入力します。
```
cd ..
```
目的のディレクトリを安全に削除できます。

使用して、 **/s** ディレクトリ ツリーを削除するにはオプションです。 たとえば、ディレクトリを削除するには、テスト (すべてのサブディレクトリおよびファイル)、現在のディレクトリから、型を名前しました。
```
rd /s test
```
で非表示モードを、前の例を実行するには、次のように入力します。
```
rd /s /q test
```

> [!CAUTION]
> 実行すると **rd/s** quiet モードは、確認なしディレクトリ ツリー全体を削除します。 重要なファイルを移動または使用する前にバックアップすることを確認、 **/q** コマンド ライン オプションです。

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)