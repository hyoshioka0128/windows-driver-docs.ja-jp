---
title: WDI_TLV_BSS_ENTRY
description: WDI_TLV_BSS_ENTRY は、BSS エントリ情報を含む TLV です。
ms.assetid: 1D3AAB94-9FCE-4243-994A-7195440DDFCA
ms.date: 07/18/2017
keywords:
- WDI_TLV_BSS_ENTRY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 17452b6d04ea66c8381c8c993d66d3c5fe8288d5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580872"
---
# <a name="wditlvbssentry"></a>WDI\_TLV\_BSS\_エントリ


WDI\_TLV\_BSS\_エントリが BSS エントリ情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x8

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 型                                                                                      | 許可されている複数の TLV インスタンス | 省略可能                                                                            | 説明                                                                                                                                                                                                                                                       |
|-------------------------------------------------------------------------------------------|--------------------------------|-------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_BSSID**](wdi-tlv-bssid.md)                                                  |                                |                                                                                     | BSS の BSSID します。                                                                                                                                                                                                                                             |
| [**WDI\_TLV\_プローブ\_応答\_フレーム**](wdi-tlv-probe-response-frame.md)                  |                                | x                                                                                   | プローブ応答フレーム。 プローブ応答フレームを受信していない場合は空です。                                                                                                                                                                            |
| [**WDI\_TLV\_ビーコン\_フレーム**](wdi-tlv-beacon-frame.md)                                   |                                | x                                                                                   | ビーコン フレーム。 ビーコンを受信していない場合は空です。                                                                                                                                                                                                  |
| [**WDI\_TLV\_BSS\_エントリ\_信号\_情報**](wdi-tlv-bss-entry-signal-info.md)               |                                |                                                                                     | BSS の信号情報 (受信信号強度とリンク品質) です。                                                                                                                                                                                    |
| [**WDI\_TLV\_BSS\_エントリ\_チャネル\_情報**](wdi-tlv-bss-entry-channel-info.md)             |                                |                                                                                     | BSS エントリに論理チャネル数と帯域 ID。                                                                                                                                                                                                         |
| [**WDI\_TLV\_BSS\_エントリ\_デバイス\_コンテキスト**](wdi-tlv-bss-entry-device-context.md)         |                                | x                                                                                   | ピアのデバイス コンテキスト。 このコンテキストでは、IHV コンポーネントからは提供され、IHV コンポーネントが維持する必要がある BSS ごとのエントリの状態を格納するために使用できます。 有効期間管理を回避するためには、問題と、IHV コンポーネントは、このフィールドにポインターを使用しない必要があります。 |
| [**WDI\_TLV\_BSS\_エントリ\_年齢\_情報**](wdi-tlv-bss-entry-age-info.md)                     |                                | X (注。この TLV は IHV コンポーネントによって BSS リストを保持している場合に必須) です。 | このエントリが最後に検出されたときのタイムスタンプを含む、この BSS エントリの有効期間情報。                                                                                                                                                  |
| [**WDI\_TLV\_P2P\_検出\_サービス\_エントリ**](wdi-tlv-p2p-discovered-service-entry.md) | x                              | x                                                                                   | サービスの一覧が、リモート デバイスで検出された検出要求に WDI が指定されている場合、ガス クエリで取得サービスの情報を含む\_P2P\_サービス\_検出\_型\_サービス\_検出の種類の情報。                                  |

 

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




