---
title: NDIS_STATUS_WDI_INDICATION_CAN_SUSTAIN_AP
description: ミニポート ドライバーでは、ポートが以前 NDIS_STATUS_WDI_INDICATION_STOP_AP を示す後 OID_WDI_TASK_START_AP 要求を受信するのに準備ができていることを示す NDIS_STATUS_WDI_INDICATION_CAN_SUSTAIN_AP を使用します。
ms.assetid: 638822A9-4CED-4564-86B3-8BC9DBA05DD3
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_CAN_SUSTAIN_AP ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6f63ca5d4382ee112fdb1af5197dca1d45a78dd1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574363"
---
# <a name="ndisstatuswdiindicationcansustainap"></a>NDIS\_状態\_WDI\_INDICATION\_できます\_サステイン\_アジア太平洋


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_を示す値\_できます\_サステイン\_AP がポートを受信できる状態であることを示す、 [OID\_WDI\_タスク\_開始\_AP](oid-wdi-task-start-ap.md)後を示す以前の要求[NDIS\_状態\_WDI\_INDICATION\_停止\_アジア太平洋](ndis-status-wdi-indication-stop-ap.md)します。

| オブジェクト |
|--------|
| ポート   |

 

## <a name="payload-data"></a>ペイロード データ


| 型                                                                                     | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                     |
|------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------|
| [**WDI\_TLV\_INDICATION\_できます\_サステイン\_アジア太平洋**](https://msdn.microsoft.com/library/windows/hardware/dn926317) |                                |          | 理由、アダプターでは、802.11 AP 機能を維持できるようになりました。 |

 

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

 

 




