---
title: OID_WDI_SET_NEIGHBOR_REPORT_ENTRIES
description: OID_WDI_SET_NEIGHBOR_REPORT_ENTRIES、LE、AP から受信した近隣ノードのレポートの一覧を送信します。 これは、UE は現在接続している AP から近隣ノードのレポートを受信するとすぐに送信されます。
ms.assetid: F77FDA4A-3029-4F6E-A82E-B318543484FF
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_NEIGHBOR_REPORT_ENTRIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 295b479b16b84213ee12192b39eaee1119879da6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359213"
---
# <a name="oidwdisetneighborreportentries"></a>OID\_WDI\_設定\_近隣\_レポート\_エントリ


OID\_WDI\_設定\_近隣\_レポート\_エントリ、LE、AP から受信した近隣ノードのレポートの一覧を送信します。 これは、UE は現在接続している AP から近隣ノードのレポートを受信するとすぐに送信されます。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | X                       | 1                               |

 

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                             | 許可されている複数の TLV インスタンス | 省略可能 | 説明                   |
|---------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------|
| [**WDI\_TLV\_近隣\_レポート\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-neighbor-report-entry) | x                              |          | 近隣ノードのレポートの一覧。 |

 

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

 

 




