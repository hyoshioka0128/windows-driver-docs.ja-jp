---
title: シンボルとシンボル ファイル
description: シンボルとシンボル ファイル
ms.assetid: b9ace4f0-8363-4dec-806f-798d30983dc1
keywords:
- シンボル、概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 921f78713115fb3976e54f577c165ae1793f2140
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209752"
---
# <a name="symbols-and-symbol-files"></a>シンボルとシンボル ファイル


## <span id="ddk_symbol_files_overview_dbg"></span><span id="DDK_SYMBOL_FILES_OVERVIEW_DBG"></span>


アプリケーション、ライブラリ、ドライバー、またはオペレーティングシステムがリンクされている場合は、.exe ファイルと .dll ファイルを作成するリンカーによって、*シンボルファイル*と呼ばれる多くの追加ファイルも作成されます。

シンボルファイルには、バイナリの実行時には実際には必要ではないが、デバッグプロセスで非常に役立つ可能性があるさまざまなデータが格納されます。

通常、シンボルファイルには次のものが含まれます。

-   グローバル変数

-   ローカル変数

-   関数名とエントリポイントのアドレス

-   フレームポインターの省略 (FPO) レコード

-   ソース行番号

これらの各項目は、個別に*シンボル*と呼ばれます。 たとえば、1つのシンボルファイル Myprogram .pdb には、グローバル変数や関数名、数百のローカル変数など、数百の記号が含まれている場合があります。 多くの場合、ソフトウェア企業は、*パブリック*シンボルと*プライベートシンボル*の両方を含む完全なシンボルファイルと、パブリックシンボルのみを含む縮小 (削除) されたファイルという2つのバージョンのシンボルファイルをリリースします。 詳細については、「[パブリックシンボルとプライベートシンボル](public-and-private-symbols.md)」を参照してください。

デバッグ時に、デバッガーがデバッグ対象のターゲットに関連付けられているシンボルファイルにアクセスできることを確認する必要があります。 ライブデバッグとデバッグクラッシュダンプファイルの両方にシンボルが必要です。 デバッグするコードの適切なシンボルを取得し、これらのシンボルをデバッガーに読み込む必要があります。

### <a name="span-idwindows_symbolsspanspan-idwindows_symbolsspanwindows-symbols"></a><span id="windows_symbols"></span><span id="WINDOWS_SYMBOLS"></span>Windows シンボル

Windows では、拡張子が .pdb のファイルにシンボルを保持します。

コンパイラとリンカーは、シンボル形式を制御します。 Visual C++リンカーは、すべてのシンボルを .pdb ファイルに配置します。

Windows オペレーティングシステムは、2つのバージョンでビルドされました。 *無料のビルド*(または*リテールビルド*) のバイナリは比較的小さいため、チェックされた*ビルド*(または*デバッグビルド*) のバイナリは大きくなり、コード自体にデバッグシンボルが追加されます。 チェックされたビルドは、Windows 10 バージョン1803より前の以前のバージョンの Windows で使用できました。 これらの各ビルドには、独自のシンボルファイルがあります。 Windows でターゲットをデバッグする場合は、ターゲットの Windows のビルドに一致するシンボルファイルを使用する必要があります。

次の表は、標準の Windows シンボルツリーに存在するいくつかのディレクトリを示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Directory</th>
<th align="left">のシンボルファイルが含まれます。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ACM</p></td>
<td align="left"><p>Microsoft Audio Compression Manager ファイル</p></td>
</tr>
<tr class="even">
<td align="left"><p>COM</p></td>
<td align="left"><p>実行可能ファイル (.com)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CPL</p></td>
<td align="left"><p>コントロールパネルのプログラム</p></td>
</tr>
<tr class="even">
<td align="left"><p>DLL</p></td>
<td align="left"><p>ダイナミックリンクライブラリファイル (.dll)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DRV</p></td>
<td align="left"><p>ドライバーファイル (drv)</p></td>
</tr>
<tr class="even">
<td align="left"><p>EXCEL.EXE</p></td>
<td align="left"><p>実行可能ファイル (.exe)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SCR</p></td>
<td align="left"><p>スクリーンセーバーファイル</p></td>
</tr>
<tr class="even">
<td align="left"><p>SYS.DATABASES</p></td>
<td align="left"><p>ドライバーファイル (.sys)</p></td>
</tr>
</tbody>
</table>

 

 

 





