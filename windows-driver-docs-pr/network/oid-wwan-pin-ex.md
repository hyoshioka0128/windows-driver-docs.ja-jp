---
title: OID_WWAN_PIN_EX
description: OID_WWAN_PIN_EX は、暗証番号 (Pin) に関連する拡張情報を設定または返します。
ms.assetid: 4D3D91B2-7B3C-4C8F-B98F-0F9999D04C03
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_PIN_EX ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 7dbdb72698f8f5899714aea4972560810dabb287
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843819"
---
# <a name="oid_wwan_pin_ex"></a>OID\_WWAN\_PIN\_EX


OID\_WWAN\_PIN\_EX は、個人識別番号 (Pin) に関連する拡張情報を設定または返します。

ミニポートドライバーは、セットおよびクエリ要求を非同期的に処理し、最初に NDIS\_\_STATUS を返し、元の要求に対して必要な\_を示し、後で[**ndis\_ステータス\_WWAN\_PIN を送信する必要があり @no__t**](ndis-status-wwan-pin-info.md)設定要求またはクエリ要求を完了したときの情報状態通知 (_s)

ミニポートドライバーは、 [**ndis\_ステータス\_wwan\_pin\_情報**](ndis-status-wwan-pin-info.md)の状態通知を送信する必要があります。これには、pin の種類と pin を返すための[ **\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)構造が含まれます。情報は、主に、クエリ要求の完了時に、MB デバイスまたはサブスクライバー Id モジュール (SIM カード) のロックを解除するために PIN が必要かどうかを示すために指定します。

Pin に関連する情報を設定するように要求している呼び出し元は、 [**NDIS\_WWAN\_\_\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin_ex)します。これにより、ポートが MB のデバイスに pin を送信したり、pin の設定を有効または無効にしたり、SIM の pin を変更したりできます。

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

 

 




