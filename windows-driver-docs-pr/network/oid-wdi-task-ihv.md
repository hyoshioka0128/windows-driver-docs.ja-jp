---
title: OID_WDI_TASK_IHV
description: OID_WDI_TASK_IHV は IHV によって開始されたタスクを開始するために使用します。
ms.assetid: 2F18A92D-D658-4454-874F-7DC3B6F8F453
ms.date: 07/18/2017
keywords:
- OID_WDI_TASK_IHV ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: c41f1f68bdaa39bc0c2d57d499cbc007767cac73
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387237"
---
# <a name="oidwditaskihv"></a>OID\_WDI\_タスク\_IHV


OID\_WDI\_タスク\_IHV は IHV によって開始されたタスクを開始するために使用します。

| オブジェクト | 中止できます。                                           | 既定の優先順位 (ホスト ドライバー ポリシー)       | 通常の実行時間 (秒) |
|--------|---------------------------------------------------------|---------------------------------------------|---------------------------------|
| ポート   | [はい]。 ポートは、中止した後、クリーンな状態でなければなりません。 | 優先順位は、IHV から要求された設定によって異なります。 | 10                              |

 

送信することによって、タスクが開始[NDIS\_状態\_WDI\_INDICATION\_IHV\_タスク\_要求](ndis-status-wdi-indication-ihv-task-request.md)、値に基づいて優先順位はIHV によって要求されました。

## <a name="task-parameters"></a>タスク パラメーター


| TLV                                                                                  | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                                                                   |
|--------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_IHV\_タスク\_デバイス\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ihv-task-device-context) |                                | x        | IHV コンポーネントによって提供されるコンテキスト データ。 これから転送される[NDIS\_状態\_WDI\_INDICATION\_IHV\_タスク\_要求](ndis-status-wdi-indication-ihv-task-request.md)。 |

 

## <a name="task-completion-indication"></a>タスクの完了を示す値


[NDIS\_状態\_WDI\_INDICATION\_IHV\_タスク\_完了](ndis-status-wdi-indication-ihv-task-complete.md)

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

 

 




