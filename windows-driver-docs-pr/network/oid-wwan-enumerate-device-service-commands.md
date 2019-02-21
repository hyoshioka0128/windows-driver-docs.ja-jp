---
title: OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS
description: OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS では、デバイスのサービスのサポートされているコマンドの一覧を返します。NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS 状態の通知操作の結果を記述する NDIS_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS 構造体を格納しています。
ms.assetid: 9888E4EC-D4BB-4BAC-B20B-DFA51005EEDA
ms.date: 08/08/2017
keywords: -OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: aa2574afdffd0d5d1b91ab38743747f748ba4eb9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539175"
---
# <a name="oidwwanenumeratedeviceservicecommands"></a>OID\_WWAN\_ENUMERATE\_デバイス\_サービス\_コマンド


OID\_WWAN\_ENUMERATE\_デバイス\_サービス\_コマンドは、デバイスのサービスのサポートされているコマンドの一覧を返します。

要求のセットがサポートされていません。

ミニポート ドライバーは、最初に、非同期的には、NDIS を返すクエリ要求を処理する必要があります\_状態\_INDICATION\_元の要求とそれ以降の送信に必要な[ **NDIS\_状態\_WWAN\_デバイス\_サービス\_サポートされている\_コマンド**](https://msdn.microsoft.com/library/windows/hardware/hh846210)状態通知を含む、 [ **NDIS\_WWAN\_ENUMERATE\_デバイス\_サービス\_コマンド**](https://msdn.microsoft.com/library/windows/hardware/hh831862)操作の結果を記述する構造体。

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


[**NDIS\_状態\_WWAN\_デバイス\_サービス\_サポートされている\_コマンド**](https://msdn.microsoft.com/library/windows/hardware/hh846210)

[**NDIS\_WWAN\_ENUMERATE\_デバイス\_サービス\_コマンド**](https://msdn.microsoft.com/library/windows/hardware/hh831862)

 

 




