---
title: OID_WWAN_DEVICE_SERVICE_COMMAND
description: OID_WWAN_DEVICE_SERVICE_COMMAND では、ベンダー固有のコマンドを実装するミニポート ドライバーを許可します。NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE 状態通知ベンダ定義の構造 (NDIS_WWAN_DEVICE_SERVICE_COMMAND) を含むトランザクションが完了しているときに、応答を提供します。
ms.assetid: 296E2D23-6EDA-4480-91A3-B6CB39243DAD
ms.date: 08/08/2017
keywords: -OID_WWAN_DEVICE_SERVICE_COMMAND ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 593b6589e023d77367618f960d38a2a3eecd2151
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579874"
---
# <a name="oidwwandeviceservicecommand"></a>OID\_WWAN\_デバイス\_サービス\_コマンド


OID\_WWAN\_デバイス\_サービス\_コマンドは、ベンダー固有のコマンドを実装するために、ミニポート ドライバーを使用します。

両方のクエリし、要求のセットがサポートされています。

ミニポート ドライバーは、クエリを処理する必要があり、セットが非同期的に、最初には、NDIS を返すことを要求\_状態\_INDICATION\_元の要求とそれ以降の送信に必要な[ **NDIS\_ステータス\_WWAN\_デバイス\_サービス\_応答**](https://msdn.microsoft.com/library/windows/hardware/hh846205)ベンダー定義の構造体を格納している状態の通知 ([**NDIS\_WWAN\_デバイス\_サービス\_コマンド**](https://msdn.microsoft.com/library/windows/hardware/hh439836))、トランザクションが完了しているときに、応答を提供します。

ミニポート ドライバーは、NDIS を返す必要があります\_状態\_いない\_指定したデバイスのサービスまたは操作をサポートしていない場合にサポートされます。

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

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_WWAN\_デバイス\_サービス\_応答**](https://msdn.microsoft.com/library/windows/hardware/hh846205)

[**NDIS\_WWAN\_デバイス\_サービス\_コマンド**](https://msdn.microsoft.com/library/windows/hardware/hh439836)

 

 




