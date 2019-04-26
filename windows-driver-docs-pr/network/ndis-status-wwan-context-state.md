---
title: NDIS_STATUS_WWAN_CONTEXT_STATE
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_CONTEXT_STATE 通知を使用して、特定のコンテキストのアクティブ化の状態が変更されたときにイベント通知を送信します。
ms.assetid: 6713f6a3-d1b7-49d0-83e1-50a33e9fff32
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_CONTEXT_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 88cba37b828fa8cb7c0cfcc15a077f54a9246708
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348541"
---
# <a name="ndisstatuswwancontextstate"></a>NDIS\_状態\_WWAN\_コンテキスト\_状態


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_コンテキスト\_状態通知の特定のコンテキストのアクティブ化の状態が変更されたときにイベント通知を送信します。

ミニポート ドライバーには、この通知が不要なイベントを送信できます。

この通知を使用して、 [ **NDIS\_WWAN\_コンテキスト\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567906)構造体。

<a name="remarks"></a>注釈
-------

結果として、コンテキストの状態の変更の原因がないときに、ミニポート ドライバーは MB サービスを通知もする必要があります、*設定*MB サービスから要求します。 たとえば、ネットワークには、コンテキストが非アクティブ化する場合、ミニポート ドライバーは MB サービスに通知する必要があります。 ミニポート ドライバーでは、ネットワークが開始されたコンテキストのアクティブ化は実装しないでください。

ミニポート ドライバーは、すべての該当するコンテキストの状態変更については、直接 Windows をよう通知する必要があります NDIS を処理するときに\_状態\_WWAN\_パケット\_サービスまたは NDIS\_状態\_WWAN\_登録\_状態通知の状態。

別の音声およびデータ接続をサポートする MB デバイスのミニポート ドライバーは、次のガイドラインに従う必要があります。

-   初期化時に、WwanVoiceCallStateNone に、VoiceCallState を設定する必要があります。

-   音声通話の開始には、VoiceCallState WwanVoiceCallStateInProgress に設定したイベント通知を送信します。 その他のすべてのメンバーは、その現在の状態を反映する必要があります。 音声通話中にアクティブな接続がないが発生した場合、ConnectionId を「0」に設定してください。

-   音声通話が完了した後は、VoiceCallState WwanVoiceCallStateHangUp に設定したイベント通知を送信します。 その他のすべてのメンバーは、その現在の状態を反映する必要があります。 音声通話切断中にアクティブな接続がないが発生した場合、ConnectionId を「0」に設定してください。 このイベントは後、に、VoiceCallState を設定する必要があります**WwanVoiceCallStateNone**ミニポート ドライバーでします。

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
<td><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_コンテキスト\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567906)

[OID\_WWAN\_プロビジョニング済み\_コンテキスト](oid-wwan-provisioned-contexts.md)

 

 




