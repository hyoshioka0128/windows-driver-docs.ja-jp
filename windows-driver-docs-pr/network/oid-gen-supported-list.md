---
title: OID_GEN_SUPPORTED_LIST
description: クエリとして、OID_GEN_SUPPORTED_LIST OID は、ミニポートドライバーまたは NIC がサポートするオブジェクトの Oid の配列を指定します。
ms.assetid: 4e663204-eee0-4732-83c9-ec1dacd41034
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_GEN_SUPPORTED_LIST
ms.localizationpriority: medium
ms.openlocfilehash: 8b5b5632c9a55720b6530163ca59c5d9806478c6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844598"
---
# <a name="oid_gen_supported_list"></a>OID\_GEN\_サポートされている\_リスト


クエリとして、OID\_GEN\_サポートされる\_リスト OID は、ミニポートドライバーまたは NIC がサポートするオブジェクトの Oid の配列を指定します。 オブジェクトには、汎用、メディア固有、および実装固有のオブジェクトが含まれます。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
要求されていません。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 ミニポートドライバー  
必ず. 「 [OID\_GEN\_サポートされる\_リスト (NDIS 5.1)](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff560258(v=vs.85))」を参照してください。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 ミニポートドライバー  
必ず. 「 [OID\_GEN\_サポートされる\_リスト (NDIS 5.1)](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff560258(v=vs.85))」を参照してください。

<a name="remarks"></a>注釈
-------

NDIS 6.0 以降のミニポートドライバーは、この OID 要求を受信しません。 NDIS は、この OID を、ミニポートドライバーが初期化時に提供するキャッシュされた値で処理します。

初期化中にサポートされる Oid の一覧を指定するために、ミニポートドライバーは[**NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造体の**SupportedOidList**メンバーを設定し、その構造体を[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数に渡します。

NDIS は、指定されたリストのサブセットを、このクエリを実行するプロトコルドライバーに転送します。 つまり、プロトコルドライバーは統計クエリを作成しないため、NDIS はサポートされているすべての統計 Oid を一覧から除外します。

サポートされている Oid の一覧に、ミニポートドライバーが OID を一覧表示する場合は、OID を完全にサポートする必要があります。 つまり、ミニポートドライバーは、クエリに応答するときに有効なデータを返すか、一覧に含まれる Oid の要求を設定する必要があります。 たとえば、 [oid\_GEN\_STATISTICS](oid-gen-statistics.md) oid は、NDIS 6.0 以降のミニポートドライバーに必要な oid です。 ミニポートドライバーでハードウェアまたはソフトウェアの統計情報がサポートされておらず、正しくない統計情報が返された場合、ドライバーは、サポートされている Oid の一覧で OID\_GEN\_の統計を指定できません。

[サポートされている Oid] の一覧に重複が表示される場合があります。 リスト内の OID ごとにエントリが1つだけであることを保証するために、ドライバーは必要ありません。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_GEN\_の統計情報](oid-gen-statistics.md)

 

 




