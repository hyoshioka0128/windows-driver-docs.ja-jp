---
title: バグ チェック 0x36 DEVICE_REFERENCE_COUNT_NOT_ZERO
description: DEVICE_REFERENCE_COUNT_NOT_ZERO のバグ チェックでは、0x00000036 の値を持ちます。 これは、正の値の参照カウントが含まれていたデバイス オブジェクトを削除するドライバーが試行されたことを示します。
ms.assetid: 8379d034-44fd-412a-8a2d-d234d41227ac
keywords:
- バグ チェック 0x36 DEVICE_REFERENCE_COUNT_NOT_ZERO
- DEVICE_REFERENCE_COUNT_NOT_ZERO
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DEVICE_REFERENCE_COUNT_NOT_ZERO
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 37e0520e1310ee83946e22b2db8e8005e9a87ab8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559811"
---
# <a name="bug-check-0x36-devicereferencecountnotzero"></a>バグ チェック 0x36 の。デバイス\_参照\_カウント\_いない\_0


デバイス\_参照\_カウント\_いない\_0 個のバグ チェックが 0x00000036 の値を持ちます。 これは、正の値の参照カウントが含まれていたデバイス オブジェクトを削除するドライバーが試行されたことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="devicereferencecountnotzero-parameters"></a>デバイス\_参照\_カウント\_いない\_0 個のパラメーター


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
<td align="left"><p>デバイス オブジェクトのアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

デバイス ドライバーが、システムからそのデバイス オブジェクトの 1 つを削除しようとしていますが、そのオブジェクトの参照カウントが 0 以外。

つまり、デバイスにまだ保留中の参照があります。 (参照カウントは、いくつかの理由がこのデバイス オブジェクトを削除できない理由を示します)。

これは、呼び出し元のデバイス ドライバーのバグです。

 

 




