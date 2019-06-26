---
title: WDI_TLV_P2P_BACKGROUND_DISCOVER_MODE
description: WDI_TLV_P2P_BACKGROUND_DISCOVER_MODE では、Wi-Fi Direct バック グラウンドの検出モード パラメーターを含む TLV です。
ms.assetid: 987DB282-A992-497F-98B5-0D3DD477B91C
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_BACKGROUND_DISCOVER_MODE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0c0323cf72f029ab425147667b64d63c3492fd66
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386823"
---
# <a name="wditlvp2pbackgrounddiscovermode"></a>WDI\_TLV\_P2P\_バック グラウンド\_DISCOVER\_モード


WDI\_TLV\_P2P\_バック グラウンド\_DISCOVER\_モードは、Wi-Fi Direct バック グラウンドの検出モード パラメーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xCE

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_p2p_discover_type" data-raw-source="[&lt;strong&gt;WDI_P2P_DISCOVER_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_p2p_discover_type)"><strong>WDI_P2P_DISCOVER_TYPE</strong></a></td>
<td>ポートで実行する探索の種類。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_p2p_service_discovery_type" data-raw-source="[&lt;strong&gt;WDI_P2P_SERVICE_DISCOVERY_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_p2p_service_discovery_type)"><strong>WDI_P2P_SERVICE_DISCOVERY_TYPE</strong></a></td>
<td>ポートで実行されるサービスの検出の種類。
<p>唯一の有効な値は WDI_P2P_SERVICE_DISCOVERY_TYPE_NO_SERVICE_DISCOVERY および WDI_P2P_SERVICE_DISCOVERY_TYPE_SERVICE_NAME_ONLY です。</p></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>デバイスの表示タイムアウトします。 レポートのデバイスのエントリの最大タイムアウト (ミリ秒単位) を指定します。 これは、機能は、バック グラウンドのスキャンのみに必要です。</td>
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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




