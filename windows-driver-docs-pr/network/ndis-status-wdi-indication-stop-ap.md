---
title: NDIS_STATUS_WDI_INDICATION_STOP_AP
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_STOP_AP を使用して、アダプターが、物理サイズのいずれかの 802.11 のアクセス ポイント (AP) 機能を維持できませんを示します。
ms.assetid: EF129BD3-6AA2-4F38-BECD-E9D526314A27
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_STOP_AP ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d634be86928ccb383763dbb4195cc98c492c01ee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375212"
---
# <a name="ndisstatuswdiindicationstopap"></a>NDIS\_状態\_WDI\_INDICATION\_停止\_アジア太平洋


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_INDICATION\_停止\_AP を示す、アダプターが、物理サイズのいずれかの 802.11 のアクセス ポイント (AP) 機能を維持できません。 アダプターは、NIC が使用可能な物理サイズで動作している任意の Ap を停止した後でのみこのを示す値を送信する必要があります。 ホストがすべてブロック[OID\_WDI\_タスク\_開始\_AP](oid-wdi-task-start-ap.md)アダプターが送信するまで要求[NDIS\_状態\_WDI\_INDICATION\_できます\_サステイン\_AP](ndis-status-wdi-indication-can-sustain-ap.md)します。

| オブジェクト |
|--------|
| ポート   |

 

## <a name="payload-data"></a>ペイロード データ


| 種類                                                                      | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                       |
|---------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------|
| [**WDI\_TLV\_INDICATION\_STOP\_AP**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-indication-stop-ap) |                                |          | アダプターの理由は、上の物理サイズのいずれかの 802.11 の AP 機能を維持ことはできません。 |

 

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


[OID\_WDI\_タスク\_開始\_アジア太平洋](oid-wdi-task-start-ap.md)

[NDIS\_STATUS\_WDI\_INDICATION\_CAN\_SUSTAIN\_AP](ndis-status-wdi-indication-can-sustain-ap.md)

 

 




