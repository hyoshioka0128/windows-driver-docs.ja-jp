---
title: OID_NDK_LOCAL_ENDPOINTS
description: クエリとして NDIS と関連付けたドライバーまたはユーザー モード アプリケーションはミニポート アダプターで Network Direct のアクティブなリスナーと共有のエンドポイントの一覧に OID_NDK_LOCAL_ENDPOINTS OID を使用します。
ms.assetid: 93F077AF-7FEA-4F92-9784-B65ADCC16564
ms.date: 08/08/2017
keywords: -OID_NDK_LOCAL_ENDPOINTS ネットワークのドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 443d46ee9f2e4a9e7d676513320d77f55d300bf1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356137"
---
# <a name="oidndklocalendpoints"></a>OID\_NDK\_ローカル\_エンドポイント


クエリとして NDIS と関連付けたドライバーまたはユーザー モード アプリケーション使用 OID\_NDK\_ローカル\_Network Direct のアクティブなリスナーとミニポート アダプター上の共有のエンドポイントの一覧にエンドポイントの OID。

NDIS 6.30 と以降のミニポート ドライバー NDK サービスを提供するには、この OID をサポートする必要があります。 それ以外の場合、この OID は省略可能です。

<a name="remarks"></a>注釈
-------

NDIS は、アダプターから Network Direct のアクティブなリスナーと共有のエンドポイントの一覧を取得するには、この OID を発行します。 リスナーと共有のエンドポイントのリストを返すため、アダプターが必要な[ **NDIS\_NDK\_ローカル\_エンドポイント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_ndk_local_endpoints)で構造体**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体。

この構造体には返されるローカル エンドポイントの数に基づく可変サイズです。 要素の数として、ローカル エンドポイントの配列のサイズがで指定された、**カウント**メンバー。

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
<td><p>NDIS 6.30 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_NDK\_ローカル\_エンドポイント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_ndk_local_endpoints)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

 

 




