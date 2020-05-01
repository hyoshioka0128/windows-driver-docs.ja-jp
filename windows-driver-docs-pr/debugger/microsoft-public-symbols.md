---
title: Microsoft パブリック シンボル サーバー
description: Microsoft シンボル サーバーを使用すると、Windows デバッガー シンボルが公開されます。
ms.assetid: b0d38104-c386-4d20-8d9c-7701347c1643
keywords:
- SymSrv, パブリック Microsoft シンボル
- シンボル サーバー, パブリック Microsoft シンボル
- パブリック シンボル ストア
- Microsoft シンボル ストア
ms.date: 04/26/2018
ms.localizationpriority: High
ms.openlocfilehash: 01d18916e96b2d96aab3b839e85b0fdfb7a7dcaf
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "72980745"
---
# <a name="microsoft-public-symbol-server"></a>Microsoft パブリック シンボル サーバー


**サーバーの状態:** 既知の問題はありません :white_check_mark: <br> Microsoft パブリック シンボル サーバーは完全に動作しています。 <br>
既知の問題については、[windbgfb@microsoft.com](mailto:windbgfb@microsoft.com) にご報告ください。 

---

Microsoft シンボル サーバーを使用すると、Windows デバッガー シンボルが公開されます。

シンボル パスに含まれるパブリック シンボル サーバーは、次の方法で直接参照できます。

```console
set _NT_SYMBOL_PATH=srv*DownstreamStore*https://msdl.microsoft.com/download/symbols
```

*DownstreamStore* は、シンボルをキャッシュするために使用されるローカル コンピューターまたはネットワーク上のディレクトリを指定する必要があります。 このダウンストリーム ストアには、デバッガーがアクセス済みのシンボルが保持されています。未アクセスの大部分のシンボルは、Microsoft のシンボル ストアに保持されます。 これにより、ダウンストリーム ストアのサイズが比較的小さく保たれ、シンボル サーバーは各ファイルを 1 回ダウンロードするだけですばやく動作できます。

この長いシンボル パスを入力しないようにするには、[ **.symfix (シンボル ストア パスの設定)** ](-symfix--set-symbol-store-path-.md) コマンドを使用します。 次のコマンドは、既存のシンボル パスにパブリック シンボル ストアを追加します。

```dbgcmd
.symfix+ C:\MySymbols
```

ローカル シンボル キャッシュの場所を省略した場合は、デバッガー インストール ディレクトリの sym サブディレクトリが使用されます。

完全なシンボル パスを表示するには、[ **.sympath (シンボル ストア パスの設定)** ](-symfix--set-symbol-store-path-.md) コマンドを使用します。 次の例に、symfix を使用してローカル シンボル キャッシュを作成し、Microsoft http シンボル サーバーを使用する方法を示します。

```dbgcmd
0: kd> .symfix c:\MyCache
0: kd> .sympath
Symbol search path is: srv*
Expanded Symbol search path is: cache*c:\MyCache;SRV*https://msdl.microsoft.com/download/symbols
```

シンボルの使用方法の詳細については、「[Windows デバッガーのシンボル パス](https://docs.microsoft.com/windows-hardware/drivers/debugger/symbol-path)」を参照してください。

**シンボル ファイルの圧縮**

Microsoft シンボル サーバーは、圧縮したシンボル ファイルを提供します。 このファイルには、ファイル名の拡張子の末尾に、圧縮されていることを示すアンダースコアが付きます。 たとえば、ntdll.dll の PDB は ntdll.pd\_ として利用できます。 SymProxy は、圧縮されたファイルをダウンロードすると、そのファイルを圧縮解除してローカル ファイル システムに保存します。 DontUncompress レジストリ キーを設定すると、SymProxy のこの動作を無効にできます。

SymStore.exe/compress を使用して、圧縮された独自のシンボルをシンボル サーバーに格納する方法については、デバッガーのトピック「[SymStore](symstore.md)」を参照してください。

 

 





