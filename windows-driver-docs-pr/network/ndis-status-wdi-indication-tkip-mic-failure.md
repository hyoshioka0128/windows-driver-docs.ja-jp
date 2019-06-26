---
title: NDIS_STATUS_WDI_INDICATION_TKIP_MIC_FAILURE
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_TKIP_MIC_FAILURE を使用して、[tkip] 暗号アルゴリズムで暗号化を解除が正常に受信したパケットがメッセージ整合性コード (MIC) の検証に失敗したときを示します。
ms.assetid: ab9d3109-72af-457e-9e65-456613cea32f
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_TKIP_MIC_FAILURE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 135f8fcdefa4d66c1026a4df8abb8733d67f7cfe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375194"
---
# <a name="ndisstatuswdiindicationtkipmicfailure"></a>NDIS\_状態\_WDI\_INDICATION\_TKIP\_MIC\_エラー


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_INDICATION\_TKIP\_MIC\_TKIP 暗号アルゴリズムで暗号化を解除が正常に受信したパケットを示すエラーメッセージ整合性コード (MIC) の検証は失敗します。

| オブジェクト |
|--------|
| ポート   |

 

## <a name="payload-data"></a>ペイロード データ


| 種類                                                                             | 許可されている複数の TLV インスタンス | 省略可能 | 説明                       |
|----------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------|
| [**WDI\_TLV\_TKIP\_MIC\_エラー\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-tkip-mic-failure-info) |                                |          | [Tkip] MIC のエラーに関する情報。 |

 

<a name="requirements"></a>必要条件
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

 

 




