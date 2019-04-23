---
title: OID_WDI_SET_NEIGHBOR_REPORT_ENTRIES
description: OID_WDI_SET_NEIGHBOR_REPORT_ENTRIES、LE、AP から受信した近隣ノードのレポートの一覧を送信します。 これは、UE は現在接続している AP から近隣ノードのレポートを受信するとすぐに送信されます。
ms.assetid: F77FDA4A-3029-4F6E-A82E-B318543484FF
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_NEIGHBOR_REPORT_ENTRIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 583432f989fe79c2eacafc8bf486f4912ea5134a
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903292"
---
# <a name="oidwdisetneighborreportentries"></a>OID\_WDI\_設定\_近隣\_レポート\_エントリ


OID\_WDI\_設定\_近隣\_レポート\_エントリ、LE、AP から受信した近隣ノードのレポートの一覧を送信します。 これは、UE は現在接続している AP から近隣ノードのレポートを受信するとすぐに送信されます。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | X                       | 1                               |

 

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                             | 許可されている複数の TLV インスタンス | 省略可能 | 説明                   |
|---------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------|
| [**WDI\_TLV\_近隣\_レポート\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/mt269133) | x                              |          | 近隣ノードのレポートの一覧。 |

 

## <a name="set-property-results"></a>セットのプロパティの結果


追加データがありません。 ヘッダー内のデータで十分です。

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

 

 




