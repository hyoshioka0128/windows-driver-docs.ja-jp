---
title: バグ チェック 0xD3 DRIVER_PORTION_MUST_BE_NONPAGED
description: DRIVER_PORTION_MUST_BE_NONPAGED のバグ チェックでは、0x000000D3 の値を持ちます。 これは、システムがプロセスが高すぎる IRQL でページング可能なメモリへのアクセスを試行したことを示します。
ms.assetid: 8b33dd20-9faa-4c02-96b7-89f55e69aeec
keywords:
- バグ チェック 0xD3 DRIVER_PORTION_MUST_BE_NONPAGED
- DRIVER_PORTION_MUST_BE_NONPAGED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_PORTION_MUST_BE_NONPAGED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b1062a3418c4e1790a06c7255684df6b294af4fb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371757"
---
# <a name="bug-check-0xd3-driverportionmustbenonpaged"></a>バグ チェック 0xD3:ドライバー\_部分\_する必要があります\_BE\_非ページ


ドライバー\_部分\_する必要があります\_BE\_NONPAGED バグ チェックが 0x000000D3 の値を持ちます。 これは、システムがプロセスが高すぎる IRQL でページング可能なメモリへのアクセスを試行したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="driverportionmustbenonpaged-parameters"></a>ドライバー\_部分\_する必要があります\_BE\_NONPAGED パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>参照されるメモリ</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>IRQL の参照時に</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0:</strong>Read</p>
<p><strong>1:</strong>書き込み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>メモリ アドレス</p></td>
</tr>
</tbody>
</table>

 

その名前がブルー スクリーンに印刷され、場所のメモリに格納されているドライバーのエラーの原因が識別できる場合 (PUNICODE\_文字列) **KiBugCheckDriver**します。

<a name="cause"></a>原因
-----

このバグ チェックは通常が誤ってマークされていない独自のコードやデータをページング可能としてドライバーで発生します。

<a name="resolution"></a>解決方法
----------

デバッグを開始するには、カーネル デバッガーを使用して、スタック トレースを取得します。

 

 




