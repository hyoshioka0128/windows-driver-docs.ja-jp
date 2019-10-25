---
title: WDI_TLV_P2P_BACKGROUND_DISCOVER_MODE
description: WDI_TLV_P2P_BACKGROUND_DISCOVER_MODE は、Wi-fi Direct バックグラウンド検出モードパラメーターを含む TLV です。
ms.assetid: 987DB282-A992-497F-98B5-0D3DD477B91C
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_BACKGROUND_DISCOVER_MODE ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 0f7df9e0f598857c71ece77ddd6019cf1ac7c940
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842360"
---
# <a name="wdi_tlv_p2p_background_discover_mode"></a>WDI\_TLV\_P2P\_バックグラウンド\_\_モードの検出


WDI\_TLV\_P2P\_バックグラウンド\_検出\_モードは、Wi-fi Direct バックグラウンド検出モードパラメーターを含む TLV です。

## <a name="tlv-type"></a>TLV 型


0xCE

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>タスクバーの検索ボックスに</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_discover_type" data-raw-source="[&lt;strong&gt;WDI_P2P_DISCOVER_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_discover_type)"><strong>WDI_P2P_DISCOVER_TYPE</strong></a></td>
<td>ポートによって実行される探索の種類。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_service_discovery_type" data-raw-source="[&lt;strong&gt;WDI_P2P_SERVICE_DISCOVERY_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_service_discovery_type)"><strong>WDI_P2P_SERVICE_DISCOVERY_TYPE</strong></a></td>
<td>ポートによって実行されるサービス検出の種類。
<p>有効な値は、WDI_P2P_SERVICE_DISCOVERY_TYPE_NO_SERVICE_DISCOVERY と WDI_P2P_SERVICE_DISCOVERY_TYPE_SERVICE_NAME_ONLY のみです。</p></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>デバイスの表示タイムアウト。 デバイスエントリを報告するための最大タイムアウト (ミリ秒単位) を指定します。 これは、バックグラウンドスキャンにのみ必要です。</td>
</tr>
</tbody>
</table>

 

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
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 




