---
title: UNC 共有を使用
description: UNC 共有を使用
ms.assetid: 7baf157d-e8c3-4ad5-a56e-58f8983da4d9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1621fd19ba2a159becf52babce7c7b87bac5b617
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529405"
---
# <a name="using-unc-shares"></a>UNC 共有を使用


Cv2http.cmd、Cv2http.pl、およびウォーク (Walk.cmd) 単純な UNC 共有からソース ファイルを提供するスクリプトを使用します。 Cv2http.cmd および Cv2http.pl ファイルは、SrcSrv ストリームを抽出し、Perl スクリプトを使用して変更して、.pdb ファイルに戻り、変更されたストリームを配置します。 構文は次のとおりです。

`cv2http.cmd PDB Alias SourceRoot`

場所*PDB*を変更する .pdbfile の名前を指定します*エイリアス*、Web サイトに適用する論理名を指定し、*ソース ルート*UNC 共有のルートを指定しますソース ファイルを展開します。 なお、*エイリアス*パラメーターは PDB に格納されて、クライアント、デバッガーの Scrsrv.ini、オーバーライド可能な変数を用意名としてはこれまで移動する Web サイトの場所。

このスクリプトでは、標準 SrcSrv ツールがすべて使用できるパスに付けて SrcTool と PDBStr の両方を呼び出すので、必要があります。 Cv2http.pl は Perl スクリプトし、ニーズに合わせて変更することができますを注意してください。

3 番目のファイル、ウォーク (walk.cmd) スクリプトは、.pdb ファイルのセット全体を変更します。 次に、例を示します。

```console
walk.cmd *.pdb cv2http.cmd SourceRoot \\server\share
```

上記のコマンドはエイリアスのソース ルートを使用して、ツリー内のすべての .pdb ファイルで Cv2http.cmd を呼び出すと\\ \\server\\UNC 共有の共有します。 チュートリアルの詳細については、次を参照してください。[ソース ファイルの抽出](extracting-source-files.md)します。

.Pdb ファイルのツリーにこのコマンドを実行した後、Web サイトまたは配置したい任意の場所にインストールする準備が整いました。 付けて SrcTool と PDBStr を使用、.pdb ファイルへの変更を確認することに注意してください。

 

 





