---
title: NDIS_STATUS_WDI_INDICATION_ACTION_FRAME_RECEIVED
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_ACTION_FRAME_RECEIVED を使用して、操作、フレームが受信されたことを示します。
ms.assetid: C1F6EB50-C11F-428F-BF51-5C89A59CBF76
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_ACTION_FRAME_RECEIVED ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f096bdf33487c34bbe8156b72421502c9093ea9a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366422"
---
# <a name="ndisstatuswdiindicationactionframereceived"></a>NDIS\_状態\_WDI\_INDICATION\_アクション\_フレーム\_受信日時


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_を示す値\_アクション\_フレーム\_を操作するフレームが受信されたことを示すために受信します。

| オブジェクト |
|--------|
| ポート   |

 

## <a name="payload-data"></a>ペイロード データ


| 種類                                                                               | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                               |
|------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------|
| [**WDI\_TLV\_BSSID**](https://msdn.microsoft.com/library/windows/hardware/dn926153)                                      |                                |          | ソースの BSSID します。                                  |
| [**WDI\_TLV\_BSS\_エントリ\_チャネル\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn926155) |                                |          | BSS エントリに論理チャネル数と帯域 ID。 |
| [**WDI\_TLV\_アクション\_フレーム\_本文**](https://msdn.microsoft.com/library/windows/hardware/dn926118)            |                                |          | 受信操作フレーム本体。                           |

 

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WDI\_設定\_広告\_情報](oid-wdi-set-advertisement-information.md)

 

 




