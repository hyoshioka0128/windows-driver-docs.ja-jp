---
title: NDIS_STATUS_WWAN_PIN_INFO
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_PIN_INFO 通知を使用して OID クエリに応答し、OID_WWAN_PIN の要求を設定します。 ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。この通知は、NDIS_WWAN_PIN_INFO 構造体を使用します。
ms.assetid: fa3c2467-2240-423b-b91b-f7e19d5be353
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_PIN_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 449a69ac21e3577b2d37b8211a7d4f4bff87b7ab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377619"
---
# <a name="ndisstatuswwanpininfo"></a>NDIS\_状態\_WWAN\_PIN\_情報


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_PIN\_OID クエリに応答し、要求の設定に情報通知[OID\_WWAN\_PIN](oid-wwan-pin.md)します。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知を使用して、 [ **NDIS\_WWAN\_PIN\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)構造体。

<a name="remarks"></a>注釈
-------

ミニポート ドライバーには、クエリ要求に応答の情報について、個人アイデンティティ暗証番号 (PIN) MB デバイスの現在の要求が返されます。 ミニポート ドライバーでは、一連の要求に対する応答で、以下のセクションで説明されているように入力状態の通知を返す必要があります。

**WwanPinOperationEnter 要求に応答するには**

ミニポート ドライバーが、NDIS を使用すると\_状態\_WWAN\_PIN\_情報通知に応答する**WwanPinOperationEnter**要求すると、これらの手順を実装する必要があります。

-   成功した**WwanPinOperationEnter** MB デバイスが不要になった、PIN を必要とする場合は、クエリ要求、ミニポート ドライバーを設定する必要があります**uStatus** WWAN に\_状態\_成功し、**PinType**に**WwanPinTypeNone**します。

-   失敗しました**WwanPinOperationEnter**要求、ミニポート ドライバーを設定する必要があります**uStatus** WWAN に\_状態\_失敗し、次の詳細に従って該当するデータを含めます。

    -   PIN を無効になっているまたは PIN が予期されていません。**WwanPinOperationEnter**セット要求、または現在、対応するピンが無効か、デバイスが必要、MB、ミニポート ドライバーを設定する必要があります**PinType**に**WwanPinTypeNone**します。 その他のすべてのメンバーは無視されます。

    -   PIN がサポートされていません。MB デバイスでは、特定の暗証番号 (pin) はサポートされていない場合のミニポート ドライバーを設定する必要があります**uStatus** WWAN に\_状態\_いいえ\_デバイス\_サポートします。

    -   PIN Retrial:このモードで MB デバイスは、PIN として再入力する必要があります、 **AttemptsRemaining**値がまだゼロ以外の暗証番号 (pin) のこの特定の型。 ミニポート ドライバーを設定する必要があります**PinType**のと同じ値に**PinType** ndis\_WWAN\_設定\_ピン留めします。

    -   ブロックをピン留めします。PIN がブロックされているときに**AttemptsRemaining**は 0 です。 操作は使用できません、暗証番号 (pin) のブロックを解除する場合は、ミニポート ドライバーを設定する必要があります**uStatus** WWAN に\_状態\_障害と**PinType**に**WwanPinTypeNone**. その他のすべてのメンバーは無視されます。

        **注**  MB デバイスの PIN をサポートしている場合は、操作をブロック解除、ミニポート ドライバーが要求に応答する PIN ブロック解除の手順を実行する必要があります。

         

    -   PIN のブロックを解除します。PIN がブロックされているときに**AttemptsRemaining**は 0 です。 暗証番号のブロックを解除するには、該当する場合、MB デバイスは、対応するピンのロックを解除キー (PUK) を要求する可能性があります。 この場合、ミニポート ドライバーを設定する必要があります**PinType**に対応する WwanPinType*Xxx*PUK に関連する詳細。

    -   PUK を禁止します。失敗した試行の回数が、WwanPinType を入力するための事前定義された値を超えたかどうか*Xxx*PUK、PUK がブロックされています。 ミニポート ドライバーはこれを設定して通知する必要があります**uStatus** WWAN に\_状態\_障害と**PinType**に**WwanPinTypeNone**します。 ミニポート ドライバーが、NDIS を送信する必要があります PUK1 がブロックされている場合に\_状態\_WWAN\_準備\_情報とともに**ReadyState**に設定**WwanReadyStateBadSim**.

**WwanPinOperationEnable、WwanPinOperationDisable、WwanPinOperationChange 要求に応答します。**

ミニポート ドライバーが、NDIS を使用すると\_状態\_WWAN\_PIN\_情報通知に応答する**WwanPinOperationEnable**、 **WwanPinOperationDisable**、および**WwanPinOperationChange**、次の操作を実装する必要があります。

-   成功した要求は、ミニポート ドライバーを設定する必要があります**uStatus** WWAN に\_状態\_成功します。 WWAN_PIN_INFO で他のメンバーは、次の状況を参照してください。

-   ミニポート ドライバーを設定する必要があります**uStatus** WWAN に\_状態\_PIN が要求された状態で既にときに、暗証番号 (pin) を有効にし、ピン留めすると無効化の操作の成功します。 ミニポート ドライバーを設定する必要があります**PinType**に**WwanPinTypeNone**します。 他のメンバーは無視されます。

-   PIN モードが無効から有効に変更されると、暗証番号 (pin) の状態が WwanPinStateNone にあります。

-   MB デバイスに電源を入れ直したとき PIN1 が有効になっている場合に、暗証番号 (pin) の状態で WwanPinStateEnter ものとなります。

-   その他のすべてのピンの状態の固定からに変更できます WwanPinStateNone WwanPinStateEnter MB デバイスの特定の条件に基づいて。

-   PIN がサポートされていません。MB デバイスでは、暗証番号 (pin) の操作はサポートされていない場合のミニポート ドライバーを設定する必要があります**uStatus** WWAN に\_状態\_いいえ\_デバイス\_サポートします。 たとえばを有効にして、暗証番号 2 を無効化は通常サポートされません MB デバイスで上記のエラー コードを返す必要があるため。 その他のすべてのメンバーは無視されます。

-   PIN を入力する必要があります。ミニポート ドライバーを設定する必要があります暗証番号 (pin) の操作では、PIN を入力する必要がある場合**uStatus** WWAN に\_状態\_PIN\_REQUIRED と**PinType** WwanPinTypeに*Xxx*します。 他のメンバーは無視されます。

-   PIN の変更操作:WWAN で無効な状態を変更する要求を返す必要がある場合 MB デバイスは、有効な状態にあるときにのみ、暗証番号 (pin) の値の変更を制限、\_状態\_PIN\_無効になっています。

-   PIN Retrial:失敗した場合、ミニポート ドライバーを設定する必要があります**uStatus** WWAN に\_状態\_エラー、および**PinType**で指定された NDIS と同じ値に\_WWAN\_設定\_ピン留めします。 以外の他のメンバーは無視されます**AttemptsRemaining**します。 これは、正しくない PIN を入力するときに発生します。

-   ブロックをピン留めします。PIN がブロックされているときに、数**AttemptsRemaining**は 0 です。 操作は使用できません、暗証番号 (pin) のブロックを解除する場合は、ミニポート ドライバーを設定する必要があります**uStatus** WWAN に\_状態\_障害と**PinType**に**WwanPinTypeNone**. **AttemptsRemaining**を 0 に設定する必要があり、その他のすべてのメンバーは無視されます。

    **注**  MB デバイスの PIN をサポートしている場合は、操作をブロック解除、ミニポート ドライバーが要求に応答する PIN ブロック解除の手順を実行する必要があります。

     

-   暗証番号のブロック解除:PIN がブロックされているときに**AttemptsRemaining**は 0 です。 PIN のブロックを解除するには、MB デバイスは該当する場合、対応する PUK を要求できます。 この場合、ミニポート ドライバーを設定する必要があります**uStatus** WWAN に\_状態\_障害、 **PinType**に対応する WwanPinType*Xxx*PUK、**PinState**に**WwanPinStateEnter**、および**AttemptsRemaining**有効 PUK を入力できる回数があります。

    ミニポート ドライバー MB デバイスまたは SIM で結果をブロックに暗証番号 (pin) がブロックされた場合にイベント通知の送信する必要があります**ReadyState**設定**WwanReadyStateDeviceLocked**します。

-   PIN1 ブロック時にアクティブな PDP コンテキストがある場合のミニポート ドライバーする必要があります PDP コンテキストを非アクティブ化し、PDP 非アクティブ化に関するオペレーティング システムに通知を送信されて、状態の変更をリンクします。

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


[OID\_WWAN\_暗証番号 (PIN)](oid-wwan-pin.md)

[**NDIS\_状態\_WWAN\_PIN\_情報**](ndis-status-wwan-pin-info.md)

 

 




