---
title: その他のルーチン
description: その他のルーチン
ms.assetid: e065c86c-a784-49e1-a1d9-e2bcff3fcae4
keywords:
- RDBSS WDK ファイル システム、その他のルーチン
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、その他のルーチン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fd2eb0d92e75bcd6259ae0a9b979204b3518a2b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384278"
---
# <a name="miscellaneous-routines"></a>その他のルーチン


## <span id="ddk_miscellaneous_functions_if"></span><span id="DDK_MISCELLANEOUS_FUNCTIONS_IF"></span>


RDBSS には、さまざまな特定のカテゴリに分類されないユーティリティ ルーチンが含まれています。

RDBSS の他のルーチンを以下に示します。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554468" data-raw-source="[&lt;strong&gt;RxFsdDispatch&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554468)"><strong>RxFsdDispatch</strong></a></p></td>
<td align="left"><p>このルーチンは、I/O 要求パケット (IRP) を処理する RDBSS のファイル システム ドライバー (FSD) ディスパッチを実装します。 このルーチンは、要求の RDBSS 処理を開始するためにドライバー ディスパッチ ルーチンで、ネットワーク ミニ リダイレクターによって呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554472" data-raw-source="[&lt;strong&gt;RxFsdPostRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554472)"><strong>RxFsdPostRequest</strong></a></p></td>
<td align="left"><p>このルーチンは、ファイル システムのプロセス (FSP) して処理するためのワーカー キューに RX_CONTEXT 構造体で指定された IRP をキューします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554481" data-raw-source="[&lt;strong&gt;RxGetRDBSSProcess&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554481)"><strong>RxGetRDBSSProcess</strong></a></p></td>
<td align="left"><p>このルーチンは、RDBSS カーネルのプロセスによって使用されるメイン スレッドのプロセスにポインターを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554508" data-raw-source="[&lt;strong&gt;RxIsThisACscAgentOpen&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554508)"><strong>RxIsThisACscAgentOpen</strong></a></p></td>
<td align="left"><p>このルーチンは、要求がユーザー モードのクライアント側キャッシュ エージェントによって行われた場合は、ファイルを開くかを判断します。</p>
<p>このルーチンは、Windows Server 2003 にできるだけです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554532" data-raw-source="[&lt;strong&gt;RxMakeLateDeviceAvailable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554532)"><strong>RxMakeLateDeviceAvailable</strong></a></p></td>
<td align="left"><p>このルーチンは、"遅延"デバイスのデバイス オブジェクトを変更します。 使用可能な。 遅延のデバイスは、いずれかのドライバーの読み込みルーチンでは作成されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554649" data-raw-source="[&lt;strong&gt;RxPrepareToReparseSymbolicLink&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554649)"><strong>RxPrepareToReparseSymbolicLink</strong></a></p></td>
<td align="left"><p>このルーチンは、再解析を容易にするために、ファイル オブジェクトの名前を設定します。 このルーチンは、シンボリック リンクを通過するネットワークのミニ リダイレクターによって使用されます。 このルーチンは、ネットワークのミニ リダイレクターによって使用する必要がありますされません。</p></td>
</tr>
</tbody>
</table>

 

 

 




