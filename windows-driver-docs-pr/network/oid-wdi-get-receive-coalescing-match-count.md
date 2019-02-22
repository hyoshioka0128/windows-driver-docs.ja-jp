---
title: OID_WDI_GET_RECEIVE_COALESCING_MATCH_COUNT
description: OID_WDI_GET_RECEIVE_COALESCING_MATCH_COUNT を要求に一致したパケットの数は、ネットワーク ポートのフィルターを受信します。
ms.assetid: 45b68057-d62a-4b77-9634-dfbed2817f23
ms.date: 07/18/2017
keywords:
- OID_WDI_GET_RECEIVE_COALESCING_MATCH_COUNT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b9580ed42fa1117eff1ca8d5928f1f869d7eea59
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537396"
---
# <a name="oidwdigetreceivecoalescingmatchcount"></a>OID\_WDI\_取得\_受信\_COALESCING\_一致\_数


OID\_WDI\_取得\_受信\_COALESCING\_一致\_に一致したパケットの数、ネットワーク ポートのフィルターの受信要求数。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

## <a name="get-property-parameters"></a>プロパティのパラメーターを取得します。


追加のパラメーターはありません。 ヘッダー内のデータで十分です。
## <a name="get-property-results"></a>プロパティの結果を得る


| TLV                                                                                              | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                  |
|--------------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------|
| [**WDI\_TLV\_COALESCING\_フィルター\_一致\_数**](https://msdn.microsoft.com/library/windows/hardware/dn926252) |                                |          | 一致したパケットの数には、ネットワーク ポートのフィルターが表示されます。 |

 

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

 

 




