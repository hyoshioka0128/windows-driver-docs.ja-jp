---
title: プリンター Dirids
description: プリンター Dirids
ms.assetid: 104af180-c739-4733-b21b-448cfe15ab71
keywords:
- WDK の INF ファイルを印刷する dirids
- dirids WDK
- ディレクトリの識別子の WDK プリンター
- プリンター dirids WDK
- 識別子の WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9f577dbc0ee727a9a379b129f8252d6d2c64d55
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340899"
---
# <a name="printer-dirids"></a>プリンター Dirids





INF ファイル、ディレクトリ識別子内のターゲット ディレクトリを指定するときに (`dirids`) 使用する必要があります。 詳細については、次を参照してください。[を使用して Dirids](https://msdn.microsoft.com/library/windows/hardware/ff553598)します。

次の表に、プリンター固有`dirids`とそれぞれの目的です。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Dirid</th>
<th>目的</th>
<th>ディレクトリの内容</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>66000</p></td>
<td><p>によって返されるディレクトリ パスを表す、 <a href="https://go.microsoft.com/fwlink/p/?linkid=124454" data-raw-source="[GetPrinterDriverDirectory](https://go.microsoft.com/fwlink/p/?linkid=124454)">GetPrinterDriverDirectory</a>関数。</p></td>
<td><p>ドライバー ファイルと<a href="printer-inf-file-entries.md#ddk-dependent-files-gg" data-raw-source="[dependent files](printer-inf-file-entries.md#ddk-dependent-files-gg)">依存ファイル</a>します。</p></td>
</tr>
<tr class="even">
<td><p>66001</p></td>
<td><p>によって返されるディレクトリ パスを表す、 <a href="https://go.microsoft.com/fwlink/p/?linkid=124455" data-raw-source="[GetPrintProcessorDirectory](https://go.microsoft.com/fwlink/p/?linkid=124455)">GetPrintProcessorDirectory</a>関数。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556325#wdkgloss-print-processor" data-raw-source="&lt;em&gt;Print processor&lt;/em&gt;"><em>プリント プロセッサ</em></a>ファイル。</p></td>
</tr>
<tr class="odd">
<td><p>66002</p></td>
<td><p>ローカル システムの \System32 にコピーする追加ファイルをディレクトリのパスを表します。 このテーブルを次の段落を参照してください。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556325#wdkgloss-print-monitor" data-raw-source="&lt;em&gt;Print monitor&lt;/em&gt;"><em>印刷モニター</em> </a>ファイル。</p></td>
</tr>
<tr class="even">
<td><p>66003</p></td>
<td><p>によって返されるディレクトリ パスを表す、 <a href="https://go.microsoft.com/fwlink/p/?linkid=124456" data-raw-source="[GetColorDirectory](https://go.microsoft.com/fwlink/p/?linkid=124456)">GetColorDirectory</a>関数。</p></td>
<td><p>ICM のカラー プロファイル ファイル。</p></td>
</tr>
<tr class="odd">
<td><p>66004</p></td>
<td><p>プリンターの種類に固有の ASP ファイルのコピー先となるディレクトリ パスを表します。</p></td>
<td><p>ASP ファイルと関連ファイルです。</p></td>
</tr>
</tbody>
</table>

 

割り当てられているディレクトリ内のファイル`dirid`66002 場合など、ローカル システムにネイティブのアーキテクチャ用のプリンター ドライバーをインストールしています、System32 サブディレクトリにコピーされますドライバーは、x86 上でローカルにインストールされて x86 システム。 このディレクトリ内のファイルには、ドライバーは、リモート システムにインストールされている場合は無視されます。

クラスのインストーラーをプリンターがスプーラーを呼び出すときに、プリンター ドライバーがインストールされている[AddPrinterDriverEx](https://go.microsoft.com/fwlink/p/?linkid=124457)関数。 この関数によって返されるディレクトリにあるすべてのドライバー ファイルが必要です、 **GetPrinterDriverDirectory**関数。

 

 




