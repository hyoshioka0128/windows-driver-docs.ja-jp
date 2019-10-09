---
title: Microsoft パブリック シンボル サーバー
description: Microsoft シンボルサーバーを使用すると、Windows デバッガーシンボルが公開されます。
ms.assetid: b0d38104-c386-4d20-8d9c-7701347c1643
keywords:
- SymSrv、パブリック Microsoft シンボル
- シンボルサーバー、パブリック Microsoft シンボル
- パブリックシンボルストア
- Microsoft シンボルストア
ms.date: 04/26/2018
ms.localizationpriority: High
ms.openlocfilehash: 01d18916e96b2d96aab3b839e85b0fdfb7a7dcaf
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007557"
---
# <a name="microsoft-public-symbol-server"></a>Microsoft パブリック シンボル サーバー


**サーバーの状態:** 既知の問題はありません: white_check_mark: <br> Microsoft パブリックシンボルサーバーは完全に動作しています。 <br>
既知の問題を[windbgfb@microsoft.com](mailto:windbgfb@microsoft.com)に報告してください。 

---

Microsoft シンボルサーバーを使用すると、Windows デバッガーシンボルが公開されます。

シンボルパスでパブリックシンボルサーバーを直接参照するには、次の方法があります。

```console
set _NT_SYMBOL_PATH=srv*DownstreamStore*https://msdl.microsoft.com/download/symbols
```

*Downstreamstore*では、シンボルをキャッシュするために使用されるローカルコンピューターまたはネットワーク上のディレクトリを指定する必要があります。 このダウンストリームストアには、デバッガーによってアクセスされたシンボルが保持されます。まだアクセスされていないシンボルの大部分は、Microsoft のシンボルストアに残ります。 これにより、ダウンストリームストアのサイズを比較的小さく保ち、シンボルサーバーをすばやく動作させることができ、各ファイルを1回だけダウンロードできます。

この長いシンボルパスを入力しないようにするには、 [ **. symfix (シンボルストアパスの設定)** ](-symfix--set-symbol-store-path-.md)コマンドを使用します。 次のコマンドは、既存のシンボルパスにパブリックシンボルストアを追加します。

```dbgcmd
.symfix+ C:\MySymbols
```

ローカルシンボルキャッシュの場所を省略した場合は、デバッガーのインストールディレクトリの sym サブディレクトリが使用されます。

完全なシンボルパスを表示するには、 [ **. sympath (シンボルストアパスの設定)** ](-symfix--set-symbol-store-path-.md)コマンドを使用します。 この例では、symfix を使用してローカルシンボルキャッシュを作成し、Microsoft http シンボルサーバーを使用する方法を示します。

```dbgcmd
0: kd> .symfix c:\MyCache
0: kd> .sympath
Symbol search path is: srv*
Expanded Symbol search path is: cache*c:\MyCache;SRV*https://msdl.microsoft.com/download/symbols
```

シンボルの使用方法の詳細については、「 [Windows デバッガーのシンボルパス](https://docs.microsoft.com/windows-hardware/drivers/debugger/symbol-path)」を参照してください。

**シンボルファイルの圧縮**

Microsoft シンボルサーバーは、シンボルファイルの圧縮バージョンを提供します。 ファイルの拡張子の末尾には、圧縮されていることを示すアンダースコアが付きます。 たとえば、ntdll の PDB は、ntdll @ no__t-0 として使用できます。 SymProxy は、圧縮されたファイルをダウンロードするときに、圧縮解除されたファイルをローカルファイルシステムに保存します。 DontUncompress レジストリキーを設定して、SymProxy でこの動作を無効にすることができます。

SymStore/compress を使用してシンボルサーバーに圧縮された独自のシンボルを格納する方法の詳細については、デバッガーのトピック[SymStore](symstore.md)を参照してください。

 

 





