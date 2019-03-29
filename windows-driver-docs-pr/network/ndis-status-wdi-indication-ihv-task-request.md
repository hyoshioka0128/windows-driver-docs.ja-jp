---
title: NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST を使用して、Microsoft コンポーネントが、IHV タスクをキューに要求します。ObjectPort します。
ms.assetid: E123F957-574F-4C78-B366-76E886018503
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 40b321c1a34360d07cb14e660c2dc31c32e4cbc0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570598"
---
# <a name="ndisstatuswdiindicationihvtaskrequest"></a>NDIS\_状態\_WDI\_INDICATION\_IHV\_タスク\_要求


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_INDICATION\_IHV\_タスク\_Microsoft コンポーネントが、IHV タスクをキューに要求を要求します。

| オブジェクト |
|--------|
| ポート   |

 

## <a name="payload-data"></a>ペイロード データ


| 型                                                                                         | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                                  |
|----------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_IHV\_タスク\_要求\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/dn926314) |                                |          | このタスクの IHV から要求された優先順位。 参照してください、 [ **WDI\_IHV\_タスク\_優先度**](https://msdn.microsoft.com/library/windows/hardware/dn926064)有効な値の列挙型。 |
| [**WDI\_TLV\_IHV\_タスク\_デバイス\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/dn926313)         |                                | x        | IHV から提供されるコンテキスト情報に転送される[OID\_WDI\_タスク\_IHV](oid-wdi-task-ihv.md)します。                                       |

 

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


[OID\_WDI\_タスク\_IHV](oid-wdi-task-ihv.md)

 

 




