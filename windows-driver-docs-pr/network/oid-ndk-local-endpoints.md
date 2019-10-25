---
title: OID_NDK_LOCAL_ENDPOINTS
description: クエリとして、NDIS およびそれ以降のドライバーまたはユーザーモードアプリケーションは、OID_NDK_LOCAL_ENDPOINTS OID を使用して、アクティブなネットワークダイレクトリスナーとミニポートアダプターの共有エンドポイントの一覧を表示します。
ms.assetid: 93F077AF-7FEA-4F92-9784-B65ADCC16564
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_NDK_LOCAL_ENDPOINTS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: ea564c3887461fa8b61ba4b2ec72c8e0c5b181e3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844107"
---
# <a name="oid_ndk_local_endpoints"></a>OID\_NDK\_ローカル\_エンドポイント


クエリとして、NDIS およびそれ以降のドライバーまたはユーザーモードアプリケーションでは、OID\_NDK\_ローカル\_エンドポイント OID が、ミニポートアダプターのアクティブなネットワークダイレクトリスナーと共有エンドポイントの一覧に OID を使用します。

NDK サービスを提供する NDIS 6.30 以降のミニポートドライバーでは、この OID がサポートされている必要があります。 それ以外の場合、この OID は省略可能です。

<a name="remarks"></a>注釈
-------

NDIS は、この OID を発行して、アクティブなネットワークダイレクトリスナーと、アダプターからの共有エンドポイントの一覧を取得します。 Ndis [ **\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーで、 [**ndis\_NDK\_ローカル\_エンドポイント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_local_endpoints)構造のリスナーと共有エンドポイントの一覧を返すには、アダプターが必要です。

この構造体は、返されるローカルエンドポイントの数に基づいて可変サイズになっています。 ローカルエンドポイント配列のサイズは、要素数として**カウント**メンバーに指定されます。

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


[**NDIS\_NDK\_ローカル\_エンドポイント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_local_endpoints)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

 

 




