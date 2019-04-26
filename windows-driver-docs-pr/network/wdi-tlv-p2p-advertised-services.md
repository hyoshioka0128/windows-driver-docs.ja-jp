---
title: WDI_TLV_P2P_ADVERTISED_SERVICES
description: WDI_TLV_P2P_ADVERTISED_SERVICES では、提供するサービスの一覧を含む TLV です。
ms.assetid: C210DDF3-0349-4108-82EC-1823F562E5D7
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_ADVERTISED_SERVICES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c684ff1415f0391ad6f359638839011a74973128
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356810"
---
# <a name="wditlvp2padvertisedservices"></a>WDI\_TLV\_P2P\_アドバタイズ\_サービス


WDI\_TLV\_P2P\_アドバタイズ\_サービスが提供するサービスの一覧を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xEF

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>種類</th>
<th>許可されている複数の TLV インスタンス</th>
<th>省略可能</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="wdi-tlv-p2p-advertised-service-entry.md" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ADVERTISED_SERVICE_ENTRY&lt;/strong&gt;](wdi-tlv-p2p-advertised-service-entry.md)"><strong>WDI_TLV_P2P_ADVERTISED_SERVICE_ENTRY</strong></a></p></td>
<td><p>x</p></td>
<td><p>x</p></td>
<td>提供するサービスの一覧。</td>
</tr>
<tr class="even">
<td><p><a href="wdi-tlv-p2p-advertised-prefix-entry.md" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ADVERTISED_PREFIX_ENTRY&lt;/strong&gt;](wdi-tlv-p2p-advertised-prefix-entry.md)"><strong>WDI_TLV_P2P_ADVERTISED_PREFIX_ENTRY</strong></a></p></td>
<td><p>x</p></td>
<td><p>x</p></td>
<td><p>提供するサービスの一覧から派生したアドバタイズされたプレフィックスの一覧。</p></td>
</tr>
<tr class="odd">
<td><p><a href="wdi-tlv-p2p-asp2-advertised-service-entry.md" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY&lt;/strong&gt;](wdi-tlv-p2p-asp2-advertised-service-entry.md)"><strong>WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY</strong></a></p></td>
<td><p>x</p></td>
<td><p>x</p></td>
<td><p>Windows 10 version 1607 では、バージョン 1.0.21 WDI に追加されます。</p>
<p>提供する ASP2 サービスの一覧。</p></td>
</tr>
<tr class="even">
<td><p><a href="wdi-tlv-p2p-service-update-indicator.md" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SERVICE_UPDATE_INDICATOR&lt;/strong&gt;](wdi-tlv-p2p-service-update-indicator.md)"><strong>WDI_TLV_P2P_SERVICE_UPDATE_INDICATOR</strong></a></p></td>
<td></td>
<td></td>
<td><p>サービス情報の検出 ANQP 要求に応答して、ドライバーがサポートしている場合、ANQP 応答に含めるサービス更新プログラムのインジケーター。</p></td>
</tr>
</tbody>
</table>

 

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

 

 




