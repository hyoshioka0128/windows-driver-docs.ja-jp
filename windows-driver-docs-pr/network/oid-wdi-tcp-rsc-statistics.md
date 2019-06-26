---
title: OID_WDI_TCP_RSC_STATISTICS
description: OID_WDI_TCP_RSC_STATISTICS は、ハードウェアの RSC の統計情報のクエリを実行する get コマンドです。
ms.assetid: 9079DD03-597D-4B6D-8515-ECF5DAC2A41A
ms.date: 07/18/2017
keywords:
- OID_WDI_TCP_RSC_STATISTICS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 846685e243184bacd5875080ece94f4062d3bb3f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362882"
---
# <a name="oidwditcprscstatistics"></a>OID\_WDI\_TCP\_RSC\_統計情報


OID\_WDI\_TCP\_RSC\_統計情報が、ハードウェアの RSC の統計情報のクエリを実行する get コマンド。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | X                       | 1                               |

 

## <a name="get-property-parameters"></a>プロパティのパラメーターを取得します。


追加のパラメーターはありません。 ヘッダー内のデータで十分です。
## <a name="get-property-results"></a>プロパティの結果を得る


| TLV                                                                                              | 許可されている複数の TLV インスタンス | 省略可能 | 説明                         |
|--------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------|
| [**WDI\_TLV\_TCP\_RSC\_STATISTICS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-tcp-rsc-statistics-parameters) |                                |          | ハードウェアの TCP RSC の統計情報です。 |

 

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

 

 




