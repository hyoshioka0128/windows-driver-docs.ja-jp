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
ms.openlocfilehash: 8c24c6fddd20265f13efc4b9b051c80ea846352c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553818"
---
# <a name="bug-check-0xd3-driverportionmustbenonpaged"></a>バグ チェック 0xD3 の。ドライバー\_部分\_する必要があります\_BE\_非ページ


ドライバー\_部分\_する必要があります\_BE\_NONPAGED バグ チェックが 0x000000D3 の値を持ちます。 これは、システムがプロセスが高すぎる IRQL でページング可能なメモリへのアクセスを試行したことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

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

 

 




