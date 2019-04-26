---
title: フィルター条件 L2 フラグ
description: このセクションでは、フィルター処理条件 L2 フラグについて説明します。
ms.assetid: D24A261D-6324-43CC-BD2A-CDB9B024432C
keywords:
- ネットワーク ドライバーをフィルター処理条件 L2 フラグ
ms.date: 11/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7571f114a4a0fecc6371215441aaf9b4153c8e84
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347526"
---
# <a name="filtering-condition-l2-flags"></a>フィルター条件 L2 フラグ

フィルター処理条件 L2 フラグは、各ビット フィールドで表されます。 これらのフラグの定義は次のとおりです。

<table>
<tr>
<th>条件のフラグをフィルター処理</th>
<th>説明</th>
</tr>
<tr>
<td>
<p>FWP_CONDITION_L2_IS_NATIVE_ETHERNET</p>
<p>0x00000001</p>
</td>
<td>
<p>テスト データがコールアウト ドライバーに渡された場合に、ネイティブ イーサネットのパケットがについて説明します。</p>
<p>このフラグは、Windows 8、Windows Server 2012、および以降のバージョンの Windows で次のフィルター処理の層に適用。</p>
<dl>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_NATIVE
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_NATIVE
</dd>
</dl>
<p>テスト データがコールアウト ドライバーに渡された場合に、WIFI パケットがについて説明します。</p>
<p>このフラグは、Windows 8、Windows Server 2012、および以降のバージョンの Windows で次のフィルター処理の層に適用。</p>
<dl>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_NATIVE
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_NATIVE
</dd>
</dl>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_L2_IS_WIFI</p>
<p>0x00000002</p>
</td>
<td>
<p>テスト データがコールアウト ドライバーに渡された場合に、ネイティブ Wi-fi パケットがについて説明します。</p>
<p>このフラグは、Windows 8、Windows Server 2012、および以降のバージョンの Windows で次のフィルター処理の層に適用。</p>
<dl>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_NATIVE
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_NATIVE
</dd>
</dl>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_L2_IS_MOBILE_BROADBAND</p>
<p>0x00000004</p>
</td>
<td>
<p>テスト データがコールアウト ドライバーに渡された場合に、モバイル ブロード バンド パケットがについて説明します。</p>
<p>このフラグは、Windows 8、Windows Server 2012、および以降のバージョンの Windows で次のフィルター処理の層に適用。</p>
<dl>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_NATIVE
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_NATIVE
</dd>
</dl>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_L2_IS_WIFI_DIRECT_DATA</p>
<p>0x00000008</p>
</td>
<td>
<p>テスト コールアウト ドライバーに渡されるデータは、WIFI を説明されている場合は、データ パケットを指示します。</p>
<p>このフラグは、Windows 8、Windows Server 2012、および以降のバージョンの Windows で次のフィルター処理の層に適用。</p>
<dl>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_NATIVE
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_NATIVE
</dd>
</dl>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_L2_IS_VM2VM</p>
<p>0x00000010</p>
</td>
<td>
<p>テスト データがコールアウト ドライバーに渡された場合に、ネイティブの仮想マシンの仮想マシンにパケットがについて説明します。</p>
<p>このフラグは、Windows 8、Windows Server 2012、および以降のバージョンの Windows で次のフィルター処理の層に適用。</p>
<dl>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_NATIVE
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_NATIVE
</dd>
</dl>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_L2_IS_MALFORMED_PACKET</p>
<p>0x00000020</p>
</td>
<td>
<p>テスト データがコールアウト ドライバーに渡された場合に、形式が正しくないイーサネットのパケットがについて説明します。</p>
<p>このフラグは、Windows 8、Windows Server 2012、および以降のバージョンの Windows で次のフィルター処理の層に適用。</p>
<dl>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_NATIVE
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_NATIVE
</dd>
</dl>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_L2_IS_IP_FRAGMENT_GROUP</p>
<p>0x00000040</p>
</td>
<td>
<p>テスト データがコールアウト ドライバーに渡された場合に、IP フラグメント グループの一部について説明します。</p>
<p>このフラグは、Windows 8、Windows Server 2012、および以降のバージョンの Windows で次のフィルター処理の層に適用。</p>
<dl>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_NATIVE
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_NATIVE
</dd>
</dl>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_L2_IF_CONNECTOR_PRESENT</p>
<p>0x00000080</p>
</td>
<td>
<p>ネットワーク インターフェイスのコネクタは、基になるネットワーク アダプター上に存在するかどうかをテストします。</p>
<p>このフラグは、物理アダプターに設定する必要があります。</p>
<p>このフラグは、Windows 8、Windows Server 2012、および以降のバージョンの Windows で次のフィルター処理の層に適用。</p>
<dl>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_NATIVE
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_NATIVE
</dd>
</dl>
</td>
</tr>
</table>

