---
title: .pdb ファイル内のソース インデックス ストリームの変更
description: .pdb ファイル内のソース インデックス ストリームの変更
ms.assetid: 9c319667-fc71-4baf-ad12-a20e18b67d40
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d82119e1214b6c09f4017d0586c2d77b0d4ea938
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387076"
---
# <a name="modifying-the-source-indexing-streams-in-a-pdb-file"></a>.pdb ファイル内のソース インデックス ストリームの変更


SrcSrv の Web サイトを使用するデバッガー クライアント、それを指す .pdb ファイルを変更する必要があります。 手動で行うは、それらを変更することを - Web サイト自体では、通常は別の場所から利用できるようにするすべての .pdb ファイルのコピーを作成します。

デバッグ ツールの Windows には、.pdb ファイルの再構成に支援するために 3 つのファイルが提供されます。 Cv2http.cmd と Cv2http.pl ファイルは、SrcSrv ストリームを抽出し、Perl スクリプトを使用して変更して、.pdb ファイルに戻り、変更されたストリームを配置します。 構文は次のとおりです。

```console
cv2http.cmd PDB Alias URL
```

場所*PDB*を変更する .pdbfile の名前を指定します*エイリアス*、Web サイトに適用する論理名を指定および*URL*サイトの完全な URL を指定します。 なお、*エイリアス*パラメーターは PDB に格納されて、クライアント、デバッガーの Scrsrv.ini、オーバーライド可能な変数名としてはこれまで移動する Web サイトの場所。

このスクリプトでは、標準 SrcSrv ツールがすべて使用できるパスに付けて SrcTool と PDBStr の両方を呼び出すので、必要があります。 Cv2http.pl は Perl スクリプトし、ニーズに合わせて変更することができますを注意してください。

3 番目のファイル、ウォーク (walk.cmd) スクリプトは、.pdb ファイルのセット全体を変更します。 次に、例を示します。

```console
walk.cmd *.pdb cv2http.cmd HttpAlias https:///source
```

上記のコマンドはエイリアスの HttpAlias を使用して、ツリー内のすべての .pdb ファイルで Cv2http.cmd を呼び出すと https://server/sourceurl。 チュートリアルの詳細については、次を参照してください。[ソース ファイルの抽出](extracting-source-files.md)します。

.Pdb ファイルのツリーにこのコマンドを実行した後、Web サイトまたは配置したい任意の場所にインストールする準備が整いました。 付けて SrcTool と PDBStr を使用、.pdb ファイルへの変更を確認することに注意してください。

 

 





