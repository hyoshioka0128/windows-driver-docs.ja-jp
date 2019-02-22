---
title: シンボルとシンボル ファイル
description: シンボルとシンボル ファイル
ms.assetid: b9ace4f0-8363-4dec-806f-798d30983dc1
keywords:
- シンボル, 概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b3f616d83929319c21da3036f2633b346e79ac6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558007"
---
# <a name="symbols-and-symbol-files"></a>シンボルとシンボル ファイル


## <span id="ddk_symbol_files_overview_dbg"></span><span id="DDK_SYMBOL_FILES_OVERVIEW_DBG"></span>


アプリケーション、ライブラリ、ドライバー、またはオペレーティング システムがリンクされている場合、.exe と .dll ファイルを作成するリンカーも数と呼ばれる追加のファイルが作成されます*シンボル ファイル*します。

シンボル ファイルは、さまざまなデータは実際には必要ありません、バイナリの実行時に、デバッグ プロセスで非常に便利になることがありますを保持します。

通常、シンボル ファイルが含まれます。

-   グローバル変数

-   ローカル変数

-   関数の名前とエントリ ポイントのアドレス

-   フレーム ポインターの省略 (FPO) レコード

-   ソース行番号

これらの各項目が呼び出されると、個別に、*シンボル*します。 たとえば、単一のシンボル ファイル Myprogram.pdb には、グローバル変数、関数名、何百ものローカル変数を含む、数百のいくつかのシンボルが含まれます。 多くの場合、各シンボル ファイルの 2 つのバージョンのリリースのソフトウェア会社: 両方を含む完全なシンボル ファイル*パブリック シンボル*と*プライベート シンボル*と削減 (削除) ファイルの親の唯一のパブリックシンボル。 詳細については、次を参照してください。[パブリックおよびプライベート シンボルの](public-and-private-symbols.md)します。

、デバッグ時に、デバッガーがデバッグしているターゲットに関連付けられているシンボル ファイルにアクセスできることを確認する必要があります。 ライブ両方のデバッグとクラッシュ ダンプ ファイルのデバッグ シンボルが必要です。 デバッグするコードの適切なシンボルを取得し、デバッガーにこれらのシンボルを読み込む必要があります。

### <a name="span-idwindowssymbolsspanspan-idwindowssymbolsspanwindows-symbols"></a><span id="windows_symbols"></span><span id="WINDOWS_SYMBOLS"></span>Windows シンボル

Windows では、拡張子 .pdb ファイルにそのシンボルを保持します。

コンパイラとリンカーは、記号の表示形式を制御します。 Visual C リンカーは、.pdb ファイルにすべてのシンボルを配置します。

Windows オペレーティング システムは、2 つのバージョンで構築されます。 *フリー ビルド*(または*リテール ビルド*) が比較的小さいバイナリは、および*チェック済みビルド*(または*デバッグ ビルド*) が大きいバイナリは、コード自体にデバッグ シンボルの詳細。 これらのビルドのそれぞれは、独自のシンボル ファイルがあります。 Windows 上のターゲットをデバッグするときに、ターゲットの Windows のビルドに一致するシンボル ファイルを使用する必要があります。

次の表は、いくつかの標準 Windows シンボルのツリーに存在するディレクトリの一覧。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Directory</th>
<th align="left">シンボル ファイルが含まれています</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ACM</p></td>
<td align="left"><p>Microsoft オーディオ圧縮 Manager ファイル</p></td>
</tr>
<tr class="even">
<td align="left"><p>COM</p></td>
<td align="left"><p>実行可能ファイル (.com)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CPL</p></td>
<td align="left"><p>コントロール パネル プログラム</p></td>
</tr>
<tr class="even">
<td align="left"><p>DLL</p></td>
<td align="left"><p>ダイナミック リンク ライブラリ ファイル (.dll)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DRV</p></td>
<td align="left"><p>ドライバー ファイル (.drv)</p></td>
</tr>
<tr class="even">
<td align="left"><p>実行可能ファイル</p></td>
<td align="left"><p>実行可能ファイル (.exe)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SCR</p></td>
<td align="left"><p>スクリーン セーバー ファイル</p></td>
</tr>
<tr class="even">
<td align="left"><p>SYS</p></td>
<td align="left"><p>ドライバー ファイル (.sys)</p></td>
</tr>
</tbody>
</table>

 

 

 





