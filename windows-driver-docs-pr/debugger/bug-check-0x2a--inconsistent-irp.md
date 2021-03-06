---
title: バグ チェック 0x2A INCONSISTENT_IRP
description: INCONSISTENT_IRP のバグ チェックでは、0x0000002A の値を持ちます。 これは、一貫性のない情報が含まれる IRP が見つかったことを示します。
ms.assetid: e8dcfba1-94ed-499c-ae00-e0dfaf7f5094
keywords:
- バグ チェック 0x2A INCONSISTENT_IRP
- INCONSISTENT_IRP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INCONSISTENT_IRP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0096fe2faf30d8d20e663243b7c14b134f82fe98
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519568"
---
# <a name="bug-check-0x2a-inconsistentirp"></a>バグ チェック 0x2A:一貫性のない\_IRP


"不整合"\_IRP のバグ チェックが 0x0000002A の値を持ちます。 これは、一貫性のない情報が含まれる IRP が見つかったことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="inconsistentirp-parameters"></a>一貫性のない\_IRP パラメーター


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
<td align="left"><p>見つかった IRP のアドレス</p></td>
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

不整合な状態である IRP が検出されました。 つまり通常、IRP のいくつかのフィールドが IRP の残りの状態と一致していません。 例は、される完了しましたが、ドライバーのデバイスのキューにキューに登録されるとしてまだマークされている IRP になります。

<a name="remarks"></a>注釈
-------

このバグ チェック コードは、システムでは、現在使用されていないが、デバッグ目的で存在します。

 

 




