---
title: OID_WDI_SET_CLEAR_RECEIVE_COALESCING
description: OID_WDI_SET_CLEAR_RECEIVE_COALESCING は、パケットの結合のパケット フィルターを削除する、ホストによって使用されます。
ms.assetid: 1c2848c4-c412-4f33-9fc6-bf900a89c65d
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_CLEAR_RECEIVE_COALESCING ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 8112b2bd06cb569387d0d34a9a09cdae600ab8ce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355217"
---
# <a name="oidwdisetclearreceivecoalescing"></a>OID\_WDI\_設定\_クリア\_受信\_COALESCING


OID\_WDI\_設定\_クリア\_受信\_COALESCING がパケットの結合のパケット フィルターを削除する、ホストによって使用されます。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                                            | 許可されている複数の TLV インスタンス | 省略可能 | 説明                         |
|------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------|
| [**WDI\_TLV\_設定\_クリア\_受信\_COALESCING**](https://msdn.microsoft.com/library/windows/hardware/dn898057) |                                |          | 削除するパケット フィルター ID。 |

 

## <a name="set-property-results"></a>セットのプロパティの結果


追加データがありません。 ヘッダー内のデータで十分です。

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


[OID\_WDI\_設定\_受信\_COALESCING](oid-wdi-set-receive-coalescing.md)

 

 




