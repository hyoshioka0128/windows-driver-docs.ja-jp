---
title: WDI_TLV_LOW_LATENCY_CONNECTION_QUALITY_PARAMETERS
description: WDI_TLV_LOW_LATENCY_CONNECTION_QUALITY_PARAMETERS では、低待機時間の接続の品質パラメーターを含む TLV です。
ms.assetid: F6C26267-AC6F-4810-913B-46DA99498BE2
ms.date: 07/18/2017
keywords:
- WDI_TLV_LOW_LATENCY_CONNECTION_QUALITY_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bb1f1d1a0be94d3ddb4f521effd9b938186aa524
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553385"
---
# <a name="wditlvlowlatencyconnectionqualityparameters"></a>WDI\_TLV\_低\_待機時間\_接続\_品質\_パラメーター


WDI\_TLV\_低\_待機時間\_接続\_品質\_パラメーターは、低待機時間の接続の品質パラメーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xF6

## <a name="length"></a>長さ


含まれるすべての要素の配列のサイズをバイト単位で。

## <a name="values"></a>値


| 種類  | 説明                                                                                                                                                                                                                                                                            |
|-------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | アクティブなスキャンまたはその他のマルチ チャネルの操作中にポートに別のチャネルでは、時間をミリ秒単位の最大数を指定します。 この無効チャネルが高いする唯一のインスタンスは、アダプターがパッシブのスキャンを実行する必要があるかどうかです。                                 |
| UINT8 | リンクの品質のしきい値を指定します[NDIS\_状態\_WDI\_INDICATION\_ローミング\_必要](https://msdn.microsoft.com/library/windows/hardware/dn925648)します。 NDIS を送信するアダプターの許容はリンクの品質がこのしきい値を下回ると、\_状態\_WDI\_INDICATION\_ローミング\_が必要です。 |

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WDI\_設定\_接続\_品質](https://msdn.microsoft.com/library/windows/hardware/dn925927)

[NDIS\_状態\_WDI\_INDICATION\_ローミング\_が必要](https://msdn.microsoft.com/library/windows/hardware/dn925648)

 

 




