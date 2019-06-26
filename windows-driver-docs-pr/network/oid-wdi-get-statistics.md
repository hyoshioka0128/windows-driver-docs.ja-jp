---
title: OID_WDI_GET_STATISTICS
description: OID_WDI_GET_STATISTICS は、IHV コンポーネントが MAC と PHY 層の統計情報を返すことを要求します。
ms.assetid: 55c36869-ce85-42fe-877b-07aefb669b56
ms.date: 07/18/2017
keywords:
- OID_WDI_GET_STATISTICS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c141b531a070cac0f892077061caaaa1f742ca62
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387265"
---
# <a name="oidwdigetstatistics"></a>OID\_WDI\_取得\_統計情報


OID\_WDI\_取得\_統計情報要求 IHV コンポーネントは、MAC および PHY 層の統計情報を返します。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | Set はサポートされません。        | 1                               |

 

ポートごと、MAC の統計をすべてに保持する必要があります。 除外しない限り、ポートごと PHY の統計を保持もする必要があります。 「チャネル」あたり統計情報を維持できる場合はポート (除外許可) に従いあたり PHY 統計情報を維持することはできません (同じチャネルで動作している 2 つのポートの PHY 統計情報を組み合わせることができます)。

## <a name="get-property-parameters"></a>プロパティのパラメーターを取得します。


追加のパラメーターはありません。 ヘッダー内のデータで十分です。
## <a name="get-property-results"></a>プロパティの結果を得る


| TLV                                                              | 許可されている複数の TLV インスタンス | 省略可能 | 説明              |
|------------------------------------------------------------------|--------------------------------|----------|--------------------------|
| [**WDI\_TLV\_MAC\_STATISTICS**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-mac-statistics) | x                              |          | ツー ピアの MAC の統計情報です。 |
| [**WDI\_TLV\_PHY\_統計情報**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-phy-statistics) | x                              |          | -ポート PHY 統計。 |

 

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

 

 




