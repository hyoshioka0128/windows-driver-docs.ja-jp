---
title: ドライバーの OID を直接要求するプロトコル
description: ドライバーの OID を直接要求するプロトコル
ms.assetid: 387d27de-3214-4f93-8f45-9a2f28e5036f
keywords:
- 直接の OID 要求インターフェイス WDK ネットワーク
- 直接の OID 要求パスの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1faea9159af9c0ec03a8efe654eebd29f2a7b65f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537217"
---
# <a name="protocol-driver-direct-oid-requests"></a>ドライバーの OID を直接要求するプロトコル





OID の直接の要求パスをサポートするプロトコルのドライバーが提供*ProtocolXxx*関数のエントリ ポイント、 [ **NDIS\_プロトコル\_ドライバー\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff566825)構造と NDIS 提供**Ndis * Xxx*** プロトコル ドライバーの関数。

*OID 要求インターフェイスを直接*は標準の OID 要求インターフェイスに似ています。 たとえば、 [ **NdisDirectOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561746)と[ **ProtocolDirectOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570259)関数は、に似ています[ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)と[ **ProtocolOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570264)関数。

**注**  NDIS 6.1 以降が直接 OID 要求インターフェイスで使用するため特定の Oid をサポートします。 NDIS 6.1 といくつかの NDIS 6.1 Oid がサポートされていません前に存在する Oid。 OID を直接の Oid インターフェイスで使用できるかどうかを確認するのには、OID のリファレンス ページを参照してください。 たとえばの注を参照、 [OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569812) OID。

 

Oid の直接の要求インターフェイスをサポートするには、標準の OID 要求インターフェイスのドキュメントを使用します。 次の表では、直接の OID 要求インターフェイス内の関数と標準の OID 要求インターフェイス間のリレーションシップを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">直接の OID 関数</th>
<th align="left">標準の OID 関数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570259" data-raw-source="[&lt;strong&gt;ProtocolDirectOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570259)"><strong>ProtocolDirectOidRequestComplete</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570264" data-raw-source="[&lt;strong&gt;ProtocolOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570264)"><strong>ProtocolOidRequestComplete</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561746" data-raw-source="[&lt;strong&gt;NdisDirectOidRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561746)"><strong>NdisDirectOidRequest</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563710" data-raw-source="[&lt;strong&gt;NdisOidRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563710)"><strong>NdisOidRequest</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561621" data-raw-source="[&lt;strong&gt;NdisCancelDirectOidRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561621)"><strong>NdisCancelDirectOidRequest</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561622" data-raw-source="[&lt;strong&gt;NdisCancelOidRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561622)"><strong>NdisCancelOidRequest</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 





