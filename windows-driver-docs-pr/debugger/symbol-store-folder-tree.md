---
title: シンボル ストアのフォルダー ツリー
description: SMB と HTTP の要求をバックアップするシンボル ストアは、ローカル ディスク上に存在するフォルダー ツリーです。
ms.assetid: AB23A180-71C3-4EBE-A3DE-765D264EF130
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b25b29a516c09eab1232b66df7416c5dd439b29d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574266"
---
# <a name="symbol-store-folder-tree"></a>シンボル ストアのフォルダー ツリー


SMB と HTTP の要求をバックアップするシンボル ストアは、ローカル ディスク上に存在するフォルダー ツリーです。

管理をシンプルにするには、サブ フォルダー名 (シンボルの除去など) はも、仮想ディレクトリ名とファイル共有の名前として使用します。 新しいサブ フォルダー d: の下で行われる新しいシンボル ストアを追加する場合は、\\SymStore と新しいファイル共有とその名前の仮想ディレクトリをクライアントにストアを公開する行われます。

ディスクのファイル システムとは、フォルダー ツリーの場所を慎重に選択する必要があります。 シンボル ストア (内部) からファイルのキャッシュ サーバーとインターネットをビルドするときに、非常に大きい (テラバイト) を取得できます。 フォルダー ツリーは、多数の読み取りと書き込みの数が少ないのは対応しているディスク上に存在する必要があります。 ファイル システムは、パフォーマンスに影響を与える - ReFS は NTFS よりもパフォーマンスが向上し、大規模な展開を調査する必要があります。 同様に、クライアントからの負荷を処理するための十分な速度、ネットワーク、サーバーをある必要がありもキャッシュの作成用のシンボルを取得するアップ ストリームのシンボルへの負荷が格納されます。

## <a name="span-idsymbolstoresingle-tierortwo-tierstructurespanspan-idsymbolstoresingle-tierortwo-tierstructurespanspan-idsymbolstoresingle-tierortwo-tierstructurespansymbol-store-single-tier-or-two-tier-structure"></a><span id="Symbol_Store_Single-Tier_or_Two-Tier_Structure"></span><span id="symbol_store_single-tier_or_two-tier_structure"></span><span id="SYMBOL_STORE_SINGLE-TIER_OR_TWO-TIER_STRUCTURE"></span>シンボル ストア 1 階層または 2 階層の構造


通常のファイルは、キャッシュされたファイル名ごとに 1 つのサブディレクトリが存在する 1 つの層のディレクトリ構造に配置されます。 各ファイル名フォルダーの下、各バージョンのファイルを格納する追加のフォルダーがされます。 ツリーには、この構造体があります。

```console
D:\SymStore\Symbols\ntdll.dll\...\
D:\SymStore\Symbols\ntdll.pdb\...\
D:\SymStore\Symbols\kernel32.dll\...\
D:\SymStore\Symbols\kernel32.pdb\...\
```

多数のファイルを格納する場合は、シンボル ストアのルートにある 2 階層構造体を使用できます。 ファイル名の最初の 2 つの文字は、中間フォルダー名として使用されます。

2 階層構造体を使用するには、d: のルートに index2.txt をという名前のファイルを配置\\SymStore\\シンボル。 ファイルの内容はない重要です。 このファイルが存在する場合、symsrv.dll は作成し、この構造体を使用して 2 層のツリーからのファイルを使用します。

```console
D:\SymStore\Symbols\nt\ntdll.dll\...\
D:\SymStore\Symbols\nt\ntdll.pdb\...\
D:\SymStore\Symbols\ke\kernel32.dll\...\
D:\SymStore\Symbols\ke\kernel32.pdb\...\
```

シンボル ストアを作成した後、構造体に変換する場合は、デバッガーのフォルダーに convertstore.exe アプリケーションを使用します。 を使用するツールを許可するのには、ルート フォルダーに 000Admin をという名前のフォルダーを作成します。 このフォルダーは、シンボル ストアのロックを制御できるように、convertstore.exe で必要です。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[シンボル ストアの HTTP](http-symbol-stores.md)

[ファイル共有 (SMB) のシンボル サーバー](file-share--smb--symbol-server.md)

 

 






