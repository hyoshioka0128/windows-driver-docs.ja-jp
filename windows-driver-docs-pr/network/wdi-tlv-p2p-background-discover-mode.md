---
title: WDI_TLV_P2P_BACKGROUND_DISCOVER_MODE
description: WDI_TLV_P2P_BACKGROUND_DISCOVER_MODE では、Wi-Fi Direct バック グラウンドの検出モード パラメーターを含む TLV です。
ms.assetid: 987DB282-A992-497F-98B5-0D3DD477B91C
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_BACKGROUND_DISCOVER_MODE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 65e0f53561d89462b4da11b69e4268b1a0f1552b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362912"
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
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926093" data-raw-source="[&lt;strong&gt;WDI_P2P_DISCOVER_TYPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926093)"><strong>WDI_P2P_DISCOVER_TYPE</strong></a></td>
<td>ポートで実行する探索の種類。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926101" data-raw-source="[&lt;strong&gt;WDI_P2P_SERVICE_DISCOVERY_TYPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926101)"><strong>WDI_P2P_SERVICE_DISCOVERY_TYPE</strong></a></td>
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

 

 




