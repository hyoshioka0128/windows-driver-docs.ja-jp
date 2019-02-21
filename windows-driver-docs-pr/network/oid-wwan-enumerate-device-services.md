---
title: OID_WWAN_ENUMERATE_DEVICE_SERVICES
description: OID_WWAN_ENUMERATE_DEVICE_SERVICES は、ミニポート ドライバーでサポートされるデバイスのサービスの一覧を返します。NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS 状態通知がサポートされているデバイスの一覧にサービスの Guid を提供する NDIS_WWAN_SUPPORTED_DEVICE_SERVICES 構造体を格納しています。
ms.assetid: 12AB2235-DDF8-44CB-BD3D-61D0FFCB4080
ms.date: 08/08/2017
keywords: -OID_WWAN_ENUMERATE_DEVICE_SERVICES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 8ebec1b11f3bc654868108acd9e30f0872ccb2f1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549992"
---
# <a name="oidwwanenumeratedeviceservices"></a>OID\_WWAN\_ENUMERATE\_デバイス\_サービス


OID\_WWAN\_ENUMERATE\_デバイス\_サービスは、ミニポート ドライバーでサポートされるデバイスのサービスの一覧を返します。

要求のセットがサポートされていません。

ミニポート ドライバーは、最初に、非同期的には、NDIS を返すクエリ要求を処理する必要があります\_状態\_INDICATION\_元の要求とそれ以降の送信に必要な[ **NDIS\_状態\_WWAN\_デバイス\_サービス\_サポートされている\_コマンド**](https://msdn.microsoft.com/library/windows/hardware/hh846210)状態通知を含む、 [ **NDIS\_WWAN\_サポートされている\_デバイス\_サービス**](https://msdn.microsoft.com/library/windows/hardware/hh831867)サービスの Guid サポートされているデバイスの一覧を提供する構造体。

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
<td><p>バージョン:Windows 8 および Windows の以降のバージョンでサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_WWAN\_デバイス\_サービス\_サポートされている\_コマンド**](https://msdn.microsoft.com/library/windows/hardware/hh846210)

[**NDIS\_WWAN\_サポートされている\_デバイス\_サービス**](https://msdn.microsoft.com/library/windows/hardware/hh831867)

 

 




