---
title: NDIS_STATUS_WWAN_SMS_RECEIVE
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_SMS_RECEIVE 通知を使用して、MB サービスに通知するか、OID_WWAN_SMS_READ を前の読み取り要求の完了に関する \ 160; クエリ要求またはから新しいクラス 0 (flash/アラート) メッセージの到着、イベント通知としてネットワーク プロバイダー。 ミニポート ドライバーには、この通知が不要なイベントを送信できます。この通知は、NDIS_WWAN_SMS_RECEIVE 構造体を使用します。
ms.assetid: fc1c3587-8bba-4ffd-9561-4140c307c705
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_SMS_RECEIVE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a85ebb8003f12fe7f0d696d0a4a5437912fe8814
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561051"
---
# <a name="ndisstatuswwansmsreceive"></a>NDIS\_状態\_WWAN\_SMS\_受信


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_SMS\_MB サービスにいずれかを以前の読み取り要求の完了に関する通知の受信通知を[OID\_WWAN\_SMS\_読み取り](oid-wwan-sms-read.md) 要求、またはイベント通知としてネットワーク プロバイダーからの新しいクラス 0 (flash/アラート) メッセージの到着をクエリします。

ミニポート ドライバーには、この通知が不要なイベントを送信できます。

この通知を使用して、 [ **NDIS\_WWAN\_SMS\_受信**](https://msdn.microsoft.com/library/windows/hardware/ff567942)構造体。

<a name="remarks"></a>注釈
-------

要求 Id を新しいクラス 0 (flash/アラート) メッセージの到着を示すために、ミニポート ドライバーで「0」に設定されます。 クラス 0 (flash/警告)、新しいメッセージの到着が現在のネットワーク登録状態に依存します。

要求は、多数のミニポート ドライバーの事前に割り当てられたバッファーでは受け入れられない SMS レコードの取得の結果を読み取り場合、は、複数の兆候で MB サービスに SMS レコードを送信することができます。 UStatus、ここである必要がありますに設定する WWAN\_状態\_SMS\_詳細\_WWAN で中間トランザクションと最後のトランザクションのデータが終了する必要があります\_状態\_成功します。

次の図は、SMS レコードを取得できるように多数の複数の indication メソッドの使用量を表します。

![sms においてレコード取得の数が多いの複数の indication メソッドの使用状況を示す図](images/wwansmsrecordretrieval.png)

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


[OID\_WWAN\_SMS\_読み取り](oid-wwan-sms-read.md)

[**NDIS\_WWAN\_SMS\_受信**](https://msdn.microsoft.com/library/windows/hardware/ff567942)

 

 




