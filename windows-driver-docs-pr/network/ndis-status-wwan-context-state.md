---
title: NDIS_STATUS_WWAN_CONTEXT_STATE
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_CONTEXT_STATE 通知を使用して、特定のコンテキストのアクティブ化の状態が変更されたときにイベント通知を送信します。
ms.assetid: 6713f6a3-d1b7-49d0-83e1-50a33e9fff32
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_CONTEXT_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d488069c2c19d2e385ccc6a0f192a8c411698129
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382651"
---
# <a name="ndisstatuswwancontextstate"></a>NDIS\_状態\_WWAN\_コンテキスト\_状態


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_コンテキスト\_状態通知の特定のコンテキストのアクティブ化の状態が変更されたときにイベント通知を送信します。

ミニポート ドライバーには、この通知が不要なイベントを送信できます。

この通知を使用して、 [ **NDIS\_WWAN\_コンテキスト\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state)構造体。

<a name="remarks"></a>注釈
-------

結果として、コンテキストの状態の変更の原因がないときに、ミニポート ドライバーは MB サービスを通知もする必要があります、*設定*MB サービスから要求します。 たとえば、ネットワークには、コンテキストが非アクティブ化する場合、ミニポート ドライバーは MB サービスに通知する必要があります。 ミニポート ドライバーでは、ネットワークが開始されたコンテキストのアクティブ化は実装しないでください。

ミニポート ドライバーは、すべての該当するコンテキストの状態変更については、直接 Windows をよう通知する必要があります NDIS を処理するときに\_状態\_WWAN\_パケット\_サービスまたは NDIS\_状態\_WWAN\_登録\_状態通知の状態。

別の音声およびデータ接続をサポートする MB デバイスのミニポート ドライバーは、次のガイドラインに従う必要があります。

-   初期化時に、WwanVoiceCallStateNone に、VoiceCallState を設定する必要があります。

-   音声通話の開始には、VoiceCallState WwanVoiceCallStateInProgress に設定したイベント通知を送信します。 その他のすべてのメンバーは、その現在の状態を反映する必要があります。 音声通話中にアクティブな接続がないが発生した場合、ConnectionId を「0」に設定してください。

-   音声通話が完了した後は、VoiceCallState WwanVoiceCallStateHangUp に設定したイベント通知を送信します。 その他のすべてのメンバーは、その現在の状態を反映する必要があります。 音声通話切断中にアクティブな接続がないが発生した場合、ConnectionId を「0」に設定してください。 このイベントは後、に、VoiceCallState を設定する必要があります**WwanVoiceCallStateNone**ミニポート ドライバーでします。

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


[**NDIS\_WWAN\_コンテキスト\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state)

[OID\_WWAN\_プロビジョニング済み\_コンテキスト](oid-wwan-provisioned-contexts.md)

 

 




