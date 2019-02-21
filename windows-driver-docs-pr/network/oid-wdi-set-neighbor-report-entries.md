---
title: OID_WDI_SET_NEIGHBOR_REPORT_ENTRIES
description: OID_WDI_SET_NEIGHBOR_REPORT_ENTRIES、LE、AP から受信した近隣ノードのレポートの一覧を送信します。 これは、UE は現在接続している AP から近隣ノードのレポートを受信するとすぐに送信されます。
ms.assetid: F77FDA4A-3029-4F6E-A82E-B318543484FF
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_NEIGHBOR_REPORT_ENTRIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bc58f763a53e8455cdfc66f13d2b77ad145c197f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550582"
---
# <a name="oidwdisetneighborreportentries"></a>OID\_WDI\_設定\_近隣\_レポート\_エントリ


OID\_WDI\_設定\_近隣\_レポート\_エントリ、LE、AP から受信した近隣ノードのレポートの一覧を送信します。 これは、UE は現在接続している AP から近隣ノードのレポートを受信するとすぐに送信されます。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | X                       | 1                               |

 

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                             | 許可されている複数の TLV インスタンス | 省略可能 | 説明                   |
|---------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------|
| [**WDI\_TLV\_近隣\_レポート\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/mt269133) | X                              |          | 近隣ノードのレポートの一覧。 |

 

## <a name="set-property-results"></a>セットのプロパティの結果


追加データがありません。 ヘッダー内のデータで十分です。
要件
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

 

 




