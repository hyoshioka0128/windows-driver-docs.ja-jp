---
title: バグ チェック 0xC8 IRQL_UNEXPECTED_VALUE
description: IRQL_UNEXPECTED_VALUE のバグ チェックでは、0x000000C8 の値を持ちます。 これは、プロセッサの IRQL では、いないどのようなことが現時点ではことを示します。
ms.assetid: eff166ab-e245-48ea-ab9e-9bb722814acf
keywords:
- バグ チェック 0xC8 IRQL_UNEXPECTED_VALUE
- IRQL_UNEXPECTED_VALUE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- IRQL_UNEXPECTED_VALUE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4ceadebe5f019861c04a44c0f49ec5afaa2bb248
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537311"
---
# <a name="bug-check-0xc8-irqlunexpectedvalue"></a>バグ チェック 0xC8 の。IRQL\_予期しない\_値


IRQL\_予期しない\_値バグ チェックが 0x000000C8 の値を持ちます。 これは、プロセッサの IRQL では、いないどのようなことが現時点ではことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="irqlunexpectedvalue-parameters"></a>IRQL\_予期しない\_値パラメーター


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
<td align="left"><p>次のビット計算の値です。</p>
<p>(現在の IRQL &lt; &lt; 16) |(IRQL を予想&lt; &lt; 8) |UniqueValue</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0、または<strong>APC-&gt;KernelRoutine</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0、または<strong>APC</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0、または<strong>APC-&gt;NormalRoutine</strong></p></td>
</tr>
</tbody>
</table>

 

(パラメーター 1 と 0 xff) を計算することによって、"UniqueValue"を指定できます。 "UniqueValue"は、0 個または 1 つは、パラメーター 2、3 のパラメーター、およびパラメーター 4 が指定された APC ポインターなります。 それ以外の場合、これらのパラメーターは 0 になります。

<a name="cause"></a>原因
-----

このエラーは通常、デバイス ドライバーまたは一定の IRQL を変更して、その期間の最後に元の IRQL を復元せず別の下位のプログラムによって発生します。 たとえば、ルーチンをスピン ロックを取得してとを解放できませんでしたが可能性があります。

 

 




