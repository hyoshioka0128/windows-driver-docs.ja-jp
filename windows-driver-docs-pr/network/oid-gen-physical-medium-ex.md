---
title: OID_GEN_PHYSICAL_MEDIUM_EX
description: クエリとして、OID_GEN_PHYSICAL_MEDIUM_EX OID は、ミニポートアダプターがサポートする物理メディアの種類を指定します。
ms.assetid: cbac8c9b-d7fe-4588-8a64-599d04a77a72
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_GEN_PHYSICAL_MEDIUM_EX
ms.localizationpriority: medium
ms.openlocfilehash: 6b808aeda7ac7383314f94a1e77b8535ea502843
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824386"
---
# <a name="oid_gen_physical_medium_ex"></a>OID\_GEN\_物理\_MEDIUM\_EX


クエリとして、OID\_GEN\_物理\_MEDIUM\_EX OID は、ミニポートアダプターがサポートする物理メディアの種類を指定します。

<a name="remarks"></a>注釈
-------

Ndis は、この OID を NDIS 6.0 以降のミニポートドライバー用に処理します。 ミニポートドライバーは、初期化中に物理メディアの値を提供します。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、NDIS\_物理\_中列挙値が含まれています。

  OID\_GEN\_物理的\_MEDIUM\_EX と Oid\_GEN\_[物理\_medium](oid-gen-physical-medium.md)の違いに**注意**してください。これは、oid\_gen\_物理\_中\_ex バージョンでは、 **NdisPhysicalMedium802\_3**型が**NdisPhysicalMediumUnspecified**として上書きされないのに対し、oid\_gen\_物理\_中はそのままです。 すべての6.x ドライバーで EX バージョンを使用することをお勧めします。 OID\_GEN\_物理\_MEDIUM\_EX は、WMI GUID を通じて公開されます。

 

ミニポートドライバーは、物理メディアの種類を報告して、 [oid\_GEN\_メディア\_サポート](oid-gen-media-supported.md)対象として宣言したメディアと、サポートされている oid クエリを区別します。

NDIS でサポートされている OID\_GEN\_物理\_MEDIUM\_EX は、新しいネットワークをサポートするミニポートアダプターの oid EX をサポートしています。ただし、これらのネットワークでは、オペレーティングシステムに表示されるパケットと NDIS には、標準の既知のメディアの種類として送信されます。

新しいネットワークでは、標準メディアと同様に表示される可能性のあるパケットが転送されますが、標準とは異なる新しい機能やわずかな違いが生じる可能性があります。 この OID が存在するので、上層のドライバーやアプリケーションが NIC の接続先となる実際のネットワークを判別できるようになります。 基になるネットワークに関する情報を取得した後、上位層のドライバーとアプリケーションはこの情報を使用して、このようなドライバーやアプリケーションの動作を変更できます。

802.3 NIC と、物理的なメディアの種類が定義されていないエミュレートされた 802.3 NIC を明確に区別するために、NDIS 6.0 以降のバージョンでは、 **NdisPhysicalMedium802\_3**メディアタイプを報告するために802.3 ミニポートドライバーが必要です。

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
<td><p>NDIS 6.20 以降でサポートされています。 ミニポートドライバーが要求されていません。 (「解説」を参照してください。)</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[OID\_GEN\_メディア\_サポートされています](oid-gen-media-supported.md)

[OID\_GEN\_物理\_メディア](oid-gen-physical-medium.md)

 

 




