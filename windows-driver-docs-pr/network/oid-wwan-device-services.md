---
title: OID_WWAN_DEVICE_SERVICES
description: OID_WWAN_DEVICE_SERVICES は、ミニポートドライバーでサポートされているデバイスサービスの一覧を返します。サポートされているデバイスサービスの Guid を示す NDIS_WWAN_DEVICE_SERVICES 構造体。
ms.assetid: 79DB0FC0-9AAA-465D-9479-9AD41BE9F4B4
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_DEVICE_SERVICES ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 37f4ed3b522775ba7333fb713bfcd944d64869fa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843849"
---
# <a name="oid_wwan_device_services"></a>OID\_WWAN\_デバイス\_サービス


OID\_WWAN\_デバイス\_サービスは、ミニポートドライバーでサポートされているデバイスサービスの一覧を返します。

ミニポートドライバーは、クエリ要求を非同期的に処理し、最初に NDIS\_の状態\_返して、元の要求に必要な\_を示し、後で NDIS\_ステータス\_WWAN\_デバイスに送信する必要があり\_サポートされているデバイスサービス Guid を示す[**NDIS\_WWAN\_デバイス\_サービス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)構造を含むサービスステータス通知。

Set 要求はサポートされていません。

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
<td><p>バージョン: Windows 8 以降のバージョンの Windows でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

 

 




