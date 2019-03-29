---
title: OID_WWAN_DEVICE_SERVICES
description: OID_WWAN_DEVICE_SERVICES は、ミニポート ドライバーでサポートされるデバイスのサービスの一覧を返します。サポートされているデバイスのサービスの Guid を示す NDIS_WWAN_DEVICE_SERVICES 構造体。
ms.assetid: 79DB0FC0-9AAA-465D-9479-9AD41BE9F4B4
ms.date: 08/08/2017
keywords: -OID_WWAN_DEVICE_SERVICES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bac260ee93b094bb894b90efc76a5899021b0872
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582062"
---
# <a name="oidwwandeviceservices"></a>OID\_WWAN\_デバイス\_サービス


OID\_WWAN\_デバイス\_サービスは、ミニポート ドライバーでサポートされるデバイスのサービスの一覧を返します。

ミニポート ドライバーは、最初に、非同期的には、NDIS を返すクエリ要求を処理する必要があります\_状態\_INDICATION\_元の要求と後で、NDIS を送信するには、必要な作業\_状態\_WWAN\_デバイス\_サービス状態の通知を含む、 [ **NDIS\_WWAN\_デバイス\_サービス**](https://msdn.microsoft.com/library/windows/hardware/hh439835)サポートされているデバイス サービス Guid 構造体。

要求のセットがサポートされていません。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>バージョン:Windows 8 および Windows の以降のバージョンでサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

 

 




