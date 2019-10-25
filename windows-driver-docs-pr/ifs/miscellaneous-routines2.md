---
title: その他のルーチン
description: その他のルーチン
ms.assetid: e065c86c-a784-49e1-a1d9-e2bcff3fcae4
keywords:
- RDBSS WDK ファイルシステム、その他のルーチン
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、その他のルーチン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81bb6d2a731a1787065fd754117985fd12bcd515
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841124"
---
# <a name="miscellaneous-routines"></a>その他のルーチン


## <span id="ddk_miscellaneous_functions_if"></span><span id="DDK_MISCELLANEOUS_FUNCTIONS_IF"></span>


RDBSS には、特定のカテゴリに分類されない多くのユーティリティルーチンが含まれています。

RDBSS その他のルーチンには、次のようなものがあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルーチン</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxfsddispatch" data-raw-source="[&lt;strong&gt;RxFsdDispatch&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxfsddispatch)"><strong>RxFsdDispatch</strong></a></p></td>
<td align="left"><p>このルーチンは、i/o 要求パケット (IRP) を処理するための RDBSS のファイルシステムドライバー (FSD) ディスパッチを実装しています。 このルーチンは、要求の RDBSS 処理を開始するために、ドライバーディスパッチルーチンのネットワークミニリダイレクターによって呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfsdpostrequest" data-raw-source="[&lt;strong&gt;RxFsdPostRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfsdpostrequest)"><strong>RxFsdPostRequest</strong></a></p></td>
<td align="left"><p>このルーチンは、RX_CONTEXT 構造体によって指定された IRP を、ファイルシステムプロセス (FSP) による処理のためにワーカーキューにキューします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxstruc/nf-rxstruc-rxgetrdbssprocess" data-raw-source="[&lt;strong&gt;RxGetRDBSSProcess&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxstruc/nf-rxstruc-rxgetrdbssprocess)"><strong>RxGetRDBSSProcess</strong></a></p></td>
<td align="left"><p>このルーチンは、RDBSS カーネルプロセスによって使用されるメインスレッドのプロセスへのポインターを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxisthisacscagentopen" data-raw-source="[&lt;strong&gt;RxIsThisACscAgentOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxisthisacscagentopen)"><strong>RxIsThisACscAgentOpen</strong></a></p></td>
<td align="left"><p>このルーチンは、ファイルオープン要求がユーザーモードのクライアント側キャッシュエージェントによって行われたかどうかを判断します。</p>
<p>このルーチンは、Windows Server 2003 でのみ使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxmakelatedeviceavailable" data-raw-source="[&lt;strong&gt;RxMakeLateDeviceAvailable&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxmakelatedeviceavailable)"><strong>RxMakeLateDeviceAvailable</strong></a></p></td>
<td align="left"><p>このルーチンは、デバイスオブジェクトを変更して "遅延デバイス" を使用できるようにします。 遅延デバイスとは、ドライバーの読み込みルーチンで作成されたものではありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxpreparetoreparsesymboliclink" data-raw-source="[&lt;strong&gt;RxPrepareToReparseSymbolicLink&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxpreparetoreparsesymboliclink)"><strong>RxPrepareToReparseSymbolicLink</strong></a></p></td>
<td align="left"><p>このルーチンは、再解析を容易にするためにファイルオブジェクト名を設定します。 このルーチンは、シンボリックリンクをスキャンするためにネットワークミニリダイレクターによって使用されます。 このルーチンは、ネットワークミニリダイレクターでは使用しないでください。</p></td>
</tr>
</tbody>
</table>

 

 

 




