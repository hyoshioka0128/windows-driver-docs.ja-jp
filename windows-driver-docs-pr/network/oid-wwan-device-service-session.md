---
title: OID_WWAN_DEVICE_SERVICE_SESSION
description: OID_WWAN_DEVICE_SERVICE_SESSION では、ミニポート ドライバーを開くか、デバイス サービス セッションを閉じるよう指示します。NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION 状態の通知操作の結果を記述する NDIS_WWAN_SET_DEVICE_SERVICE_SESSION 構造体を格納しています。
ms.assetid: 32D4EDE3-4782-4C54-95B8-83DE7E63C4F8
ms.date: 08/08/2017
keywords: -OID_WWAN_DEVICE_SERVICE_SESSION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 19624fffce6e9af02e24e648d8b2b60c7ed9954d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341374"
---
# <a name="oidwwandeviceservicesession"></a>OID\_WWAN\_デバイス\_サービス\_セッション


OID\_WWAN\_デバイス\_サービス\_セッションを開くか、デバイス サービス セッションを閉じるミニポート ドライバーに指示します。

クエリ要求はサポートされていません。

ミニポート ドライバーが非同期的に、最初に返す NDIS セット要求を処理する必要があります\_状態\_INDICATION\_元の要求とそれ以降の送信に必要な[ **NDIS\_状態\_WWAN\_デバイス\_サービス\_セッション**](https://msdn.microsoft.com/library/windows/hardware/hh846206)状態通知を含む、 [ **NDIS\_WWAN\_設定\_デバイス\_サービス\_セッション**](https://msdn.microsoft.com/library/windows/hardware/hh831865)操作の結果を記述する構造体。

ミニポート ドライバーは、NDIS を返す必要があります\_状態\_いない\_指定したデバイスのサービスまたは操作をサポートしていない場合にサポートされます。

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


[**NDIS\_WWAN\_設定\_デバイス\_サービス\_セッション**](https://msdn.microsoft.com/library/windows/hardware/hh831865)

[**NDIS\_状態\_WWAN\_デバイス\_サービス\_セッション**](https://msdn.microsoft.com/library/windows/hardware/hh846206)

 

 




