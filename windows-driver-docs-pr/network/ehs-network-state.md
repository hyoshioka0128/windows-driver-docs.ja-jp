---
title: eHS_NETWORK_STATE 列挙型
description: EHS_NETWORK_STATE 列挙体は、ネットワークがホット スポット ネットワークかどうかを示します。
ms.assetid: a833d226-e2cf-41f9-a926-5b1f6daa03af
keywords:
- Windows Vista 以降のドライバーをネットワーク eHS_NETWORK_STATE 列挙型
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0e258c385af2e7dcce00d736219fca8895140dc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536498"
---
# <a name="ehsnetworkstate-enumeration"></a>eHS\_ネットワーク\_の状態の列挙

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**EHS\_ネットワーク\_状態**列挙体は、ネットワークは、ホット スポット ネットワークかどうかを示します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef enum _eHS_NETWORK_STATE { 
  HS_NETWORK_STATE_NOT_A_HOTSPOT,
  HS_NETWORK_STATE_HOTSPOT_MANUAL_CONNECT,
  HS_NETWORK_STATE_HOTSPOT_AUTO_CONNECT,
  HS_NETWORK_STATE_MAX
} eHS_NETWORK_STATE;
```

<a name="constants"></a>定数
---------

<a href="" id="hs-network-state-not-a-hotspot"></a>**HS\_ネットワーク\_状態\_いない\_A\_ホット スポット**  
ネットワークのホット スポット ネットワークでないことを示します。

<a href="" id="hs-network-state-hotspot-manual-connect"></a>**HS\_ネットワーク\_状態\_ホット スポット\_手動\_接続**  
ユーザーはホット スポット ネットワークに手動で接続できることを示します。

<a href="" id="hs-network-state-hotspot-auto-connect"></a>**HS\_ネットワーク\_状態\_ホット スポット\_自動\_接続**  
ホット スポット ネットワークに、デバイスが自動的に接続できることを示します。

<a href="" id="hs-network-state-max"></a>**HS\_ネットワーク\_状態\_MAX**  
範囲外の値を示します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows 10 Mobile</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin.h (Hotspotoffloadplugin.h を含む)</td>
</tr>
</tbody>
</table>

 

 




