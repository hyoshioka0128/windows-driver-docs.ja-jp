---
title: ミニポート アダプター Direct OID 要求
description: ミニポート アダプター Direct OID 要求
ms.assetid: 63ced5a3-0c83-4952-aa0e-c3c654b3f241
keywords:
- 直接の OID 要求インターフェイス WDK ネットワーク
- 直接の OID 要求パスの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb6e42d4d5d722722174264794c7303b095a5706
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372442"
---
# <a name="miniport-adapter-direct-oid-requests"></a>ミニポート アダプター Direct OID 要求





OID の直接の要求パスをサポートするミニポート ドライバーが提供*MiniportXxx*関数のエントリ ポイント、 [ **NDIS\_ミニポート\_ドライバー\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565958)構造と NDIS 提供**NdisM * Xxx*** ミニポート ドライバーの関数。

*OID 要求インターフェイスを直接*は標準の OID 要求インターフェイスに似ています。 たとえば、 [ **NdisMDirectOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563582)と[ *MiniportDirectOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559371)関数は、に似ています[**NdisMOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563622)と[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)関数。

**注**  NDIS 6.1 では、直接 OID 要求インターフェイスで使用する特定の Oid がサポートされています。 NDIS 6.1 といくつかの NDIS 6.1 Oid がサポートされていません前に存在する Oid。 OID を直接の Oid インターフェイスで使用できるかどうかを確認するのには、OID のリファレンス ページを参照してください。 

ミニポート ドライバーでは、シリアル化されないを直接の OID 要求を処理できる必要があります。 標準の OID 要求インターフェイスとは異なり NDIS は他の OID の直接のインターフェイスと標準の OID 要求インターフェイスに送信される要求との直接の OID 要求をシリアル化できません。 また、ミニポート ドライバーが IRQL で直接 OID 要求を処理することにある必要があります&lt;= ディスパッチ\_レベル。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559371" data-raw-source="[&lt;em&gt;MiniportDirectOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559371)"><em>MiniportDirectOidRequest</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559416" data-raw-source="[&lt;em&gt;MiniportOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559416)"><em>MiniportOidRequest</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559335" data-raw-source="[&lt;em&gt;MiniportCancelDirectOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559335)"><em>MiniportCancelDirectOidRequest</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559339" data-raw-source="[&lt;em&gt;MiniportCancelOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559339)"><em>MiniportCancelOidRequest</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563582" data-raw-source="[&lt;strong&gt;NdisMDirectOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563582)"><strong>NdisMDirectOidRequestComplete</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563622" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563622)"><strong>NdisMOidRequestComplete</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 





