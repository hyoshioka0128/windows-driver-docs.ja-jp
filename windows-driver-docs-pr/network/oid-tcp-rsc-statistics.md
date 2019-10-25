---
title: OID_TCP_RSC_STATISTICS
description: クエリとして、NDIS およびそれ以降のドライバーまたはユーザーモードのアプリケーションは、OID_TCP_RSC_STATISTICS OID を使用して、ミニポートアダプターの受信セグメント合体 (RSC) 統計を取得します。
ms.assetid: CD289868-1925-4222-8A4D-359118124325
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_TCP_RSC_STATISTICS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: d23634c0cb6ff59b4a01583bc7d33d0fce5c2561
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843900"
---
# <a name="oid_tcp_rsc_statistics"></a>OID\_TCP\_RSC\_の統計情報


クエリとして、NDIS およびそれ以降のドライバーまたはユーザーモードアプリケーションでは、\_TCP\_RSC\_STATISTICS OID の OID を使用して、ミニポートアダプターの受信セグメント合体 (RSC) 統計を取得します。

RSC サービスを提供する NDIS 6.30 以降のミニポートドライバーでは、この OID がサポートされている必要があります。 それ以外の場合、この OID は省略可能です。

<a name="remarks"></a>注釈
-------

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_RSC\_STATISTICS\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rsc_statistics_info)構造体が含まれています。

ミニポートドライバーは、次のように、 [**NDIS\_RSC\_statistics\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rsc_statistics_info)構造体のメンバーの統計情報を保持する必要があります。

-   ドライバーは、1つの結合された単位 (SCU) にパケットが追加されるたびに、 **CoalescedPkts**メンバー内の結合されたパケット数を1つ増やす必要があります。
-   ドライバーは、パケットが SCU に追加されるたびに、パケットの TCP ペイロードのサイズによって、 **CoalescedOctets**メンバー内の結合されたオクテットカウントをインクリメントする必要があります。
-   ドライバーは、SCU が完了するたびに、結合された events count **CoalesceEvents**メンバーを1つ増やす必要があります。 このような SCUs には、0以外の**CoalescedSegCount**値を設定する必要があります。
-   ドライバーは、終了した IP データグラムの長さ以外の例外が発生するたび**に、中止メンバーの**中止回数を1つ増やす必要があります。 この数には、パケットがハードウェアリソースによって結合されていない場合が含まれます。

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
<td><p>Windows 8 の NDIS 6.30 以降のドライバーでサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_RSC\_統計\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rsc_statistics_info)

 

 




