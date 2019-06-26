---
title: NDIS_STATUS_WDI_INDICATION_RADIO_STATUS
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_RADIO_STATUS を使用して、アダプターのオプションの状態の変化を示します。
ms.assetid: c2f90a52-ce55-4819-a66a-cfcc591cb3e9
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_RADIO_STATUS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0bc2c7969bcc9dd1f7977503ca8ca236506233d0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353318"
---
# <a name="ndisstatuswdiindicationradiostatus"></a>NDIS\_状態\_WDI\_INDICATION\_ラジオ\_状態


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_INDICATION\_ラジオ\_アダプターのオプションの状態の変化を示す状態。 ソフトウェア無線の変更は、ホストによってトリガーされたときに、アダプターによってハードウェア無線状態の変更が検出されたときに、要請されていないこの通知が送信されます。

| オブジェクト |
|--------|
| ポート   |

 

## <a name="payload-data"></a>ペイロード データ


| 種類                                                                  | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                              |
|-----------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------|
| [**WDI\_TLV\_RADIO\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-radio-state-parameters) |                                |          | ハードウェアとソフトウェア無線の現在の状態。 |

 

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

## <a name="see-also"></a>関連項目


[WDI\_タスク\_設定\_ラジオ\_状態](oid-wdi-task-set-radio-state.md)

 

 




