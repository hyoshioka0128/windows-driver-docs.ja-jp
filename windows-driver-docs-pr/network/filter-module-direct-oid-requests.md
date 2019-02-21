---
title: モジュールの直接の OID 要求をフィルター処理します。
description: モジュールの直接の OID 要求をフィルター処理します。
ms.assetid: 0ab7079b-6578-4932-a276-40a961b55efe
keywords:
- 直接の OID 要求インターフェイス WDK ネットワーク
- 直接の OID 要求パスの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 049fc5adfe6b237310ebdcdc4262c8708bcdc0ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530813"
---
# <a name="filter-module-direct-oid-requests"></a>モジュールの直接の OID 要求をフィルター処理します。





OID の直接の要求パスをサポートするフィルター ドライバーが提供*FilterXxx*関数のエントリ ポイント、 [ **NDIS\_フィルター\_ドライバー\_特性** ](https://msdn.microsoft.com/library/windows/hardware/ff565515)構造と NDIS 提供**NdisF * Xxx*** フィルター ドライバーの関数。

*OID 要求インターフェイスを直接*は標準の OID 要求インターフェイスに似ています。 たとえば、 [ **NdisFDirectOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561809)と[ *FilterDirectOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff549931)関数に似ています、 [**NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)と[ *FilterOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff549954)関数。

**注**  NDIS 6.1 以降が直接 OID 要求インターフェイスで使用するため特定の Oid をサポートします。 NDIS 6.1 といくつかの NDIS 6.1 Oid がサポートされていません前に存在する Oid。 OID を直接の Oid インターフェイスで使用できるかどうかを確認するのには、OID のリファレンス ページを参照してください。 たとえばの注を参照、 [OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569812) OID。

 

フィルター ドライバーは、シリアル化されないを直接の OID 要求を処理できる必要があります。 標準の OID 要求インターフェイスとは異なり NDIS は他の OID の直接のインターフェイスと標準の OID 要求インターフェイスに送信される要求との直接の OID 要求をシリアル化できません。 また、フィルター ドライバーが IRQL で直接 OID 要求を処理することにある必要があります&lt;= ディスパッチ\_レベル。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549931" data-raw-source="[&lt;em&gt;FilterDirectOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549931)"><em>FilterDirectOidRequest</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549954" data-raw-source="[&lt;em&gt;FilterOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549954)"><em>FilterOidRequest</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549908" data-raw-source="[&lt;em&gt;FilterCancelDirectOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549908)"><em>FilterCancelDirectOidRequest</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549911" data-raw-source="[&lt;em&gt;FilterCancelOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549911)"><em>FilterCancelOidRequest</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549933" data-raw-source="[&lt;em&gt;FilterDirectOidRequestComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549933)"><em>FilterDirectOidRequestComplete</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549956" data-raw-source="[&lt;em&gt;FilterOidRequestComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549956)"><em>FilterOidRequestComplete</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561809" data-raw-source="[&lt;strong&gt;NdisFDirectOidRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561809)"><strong>NdisFDirectOidRequest</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561830" data-raw-source="[&lt;strong&gt;NdisFOidRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561830)"><strong>NdisFOidRequest</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561815" data-raw-source="[&lt;strong&gt;NdisFDirectOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561815)"><strong>NdisFDirectOidRequestComplete</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561815" data-raw-source="[&lt;strong&gt;NdisFDirectOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561815)"><strong>NdisFDirectOidRequestComplete</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561788" data-raw-source="[&lt;strong&gt;NdisFCancelDirectOidRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561788)"><strong>NdisFCancelDirectOidRequest</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561792" data-raw-source="[&lt;strong&gt;NdisFCancelOidRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561792)"><strong>NdisFCancelOidRequest</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 





