---
title: NDIS_STATUS_WWAN_SMS_STATUS
description: ミニポート ドライバーの使用、MB サービスを次のイベント、MB デバイスのメッセージ ストアに通知するために NDIS_STATUS_WWAN_SMS_STATUS 通知がいっぱいです。新しい SMS テキスト メッセージが到着した、MessageIndex.Miniport に対応する新しいメッセージをドライバーもこの通知が不要なイベントを送信します。この通知は、NDIS_WWAN_SMS_STATUS 構造体を使用します。
ms.assetid: 65553a3f-57af-49ef-a3b7-ed35df0a319d
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_SMS_STATUS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c60af8cff49121851565aa71b41cd1eb8dcb20e0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530460"
---
# <a name="ndisstatuswwansmsstatus"></a>NDIS\_状態\_WWAN\_SMS\_状態


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_SMS\_MB サービスに、次のイベントを通知するために状態の通知。

-   MB デバイスのメッセージ ストアがいっぱいです。

-   新しいメッセージに一致する、新しい SMS テキスト メッセージが到着した*MessageIndex*します。

ミニポート ドライバーには、この通知が不要なイベントを送信できます。

この通知を使用して、 [ **NDIS\_WWAN\_SMS\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567945)構造体。

<a name="remarks"></a>注釈
-------

ミニポート ドライバーは、NDIS を使用する必要があります\_状態\_WWAN\_SMS\_クラス-0 以外 (flash/アラート) のすべてのメッセージの到着 MB サービスに通知する状態。 クラス 0 (flash/アラート) メッセージの到着、MB、サービスに通知するミニポート ドライバーを使用する必要があります[ **NDIS\_状態\_WWAN\_SMS\_受信**](ndis-status-wwan-sms-receive.md).

この表示でのトランザクション通知可能性があります、*クエリ*OID の要求\_WWAN\_SMS\_状態または要請されていないイベント。

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
<td><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_SMS\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567945)

[**NDIS\_状態\_WWAN\_SMS\_受信**](ndis-status-wwan-sms-receive.md)

 

 




