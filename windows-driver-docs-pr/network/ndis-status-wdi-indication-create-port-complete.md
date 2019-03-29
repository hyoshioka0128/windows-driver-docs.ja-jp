---
title: NDIS_STATUS_WDI_INDICATION_CREATE_PORT_COMPLETE
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_CREATE_PORT_COMPLETE を使用して、OID_WDI_TASK_CREATE_PORT の完了を示します。
ms.assetid: 8d3cdac1-06d3-4a21-ac13-e6d789c6922e
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_CREATE_PORT_COMPLETE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 32f09995ff9fff702ba366e672aaad6e64166377
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580555"
---
# <a name="ndisstatuswdiindicationcreateportcomplete"></a>NDIS\_状態\_WDI\_INDICATION\_作成\_ポート\_完了


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_INDICATION\_作成\_ポート\_の完了を示す完了[OID\_WDI\_タスク\_作成\_ポート](oid-wdi-task-create-port.md)します。

| オブジェクト |
|--------|
| ポート   |

 

## <a name="payload-data"></a>ペイロード データ


| 型                                                               | 許可されている複数の TLV インスタンス | 省略可能 | 説明                         |
|--------------------------------------------------------------------|--------------------------------|----------|-------------------------------------|
| [**WDI\_TLV\_ポート\_属性**](https://msdn.microsoft.com/library/windows/hardware/dn898038) |                                |          | 作成したポートの属性。 |

 

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

 

 




