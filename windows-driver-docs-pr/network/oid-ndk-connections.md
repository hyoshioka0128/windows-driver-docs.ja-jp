---
title: OID_NDK_CONNECTIONS
description: クエリとして、NDIS およびそれ以降のドライバーまたはユーザーモードのアプリケーションは、OID_NDK_CONNECTIONS OID を使用して、ミニポートアダプターからのアクティブなネットワーク直接接続の一覧を照会します。
ms.assetid: 31A0BB2B-B571-4548-A9D1-BE44687DEA37
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_NDK_CONNECTIONS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 9d3562c8e48966c00603093b85011dd48e366d92
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844587"
---
# <a name="oid_ndk_connections"></a>NDK\_接続\_OID


クエリとして、NDIS およびそれ以降のドライバーまたはユーザーモードアプリケーションは、OID\_NDK\_CONNECTIONS OID を使用して、ミニポートアダプターからのアクティブなネットワーク直接接続の一覧を照会します。

NDK サービスを提供する NDIS 6.30 以降のミニポートドライバーでは、この OID がサポートされている必要があります。 それ以外の場合、この OID は省略可能です。

<a name="remarks"></a>注釈
-------

NDIS は、アダプターからのアクティブなネットワーク直接接続の一覧を取得するために、この OID を発行します。 このアダプターは、ndis [ **\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーで、 [**ndis\_NDK\_connections**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_connections)構造を持つ接続の一覧を返す必要があります。

この構造体は、返される接続の数に基づいて可変サイズになっています。 要素数としての接続配列のサイズは、 **count**メンバーで指定されます。

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
<td><p>サポートなし</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.30 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_NDK\_接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_connections)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

 

 




