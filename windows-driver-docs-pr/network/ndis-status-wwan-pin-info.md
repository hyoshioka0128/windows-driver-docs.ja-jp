---
title: NDIS_STATUS_WWAN_PIN_INFO
description: ミニポートドライバーは、NDIS_STATUS_WWAN_PIN_INFO 通知を使用して OID クエリに応答し、OID_WWAN_PIN の要求を設定します。 ミニポートドライバーは、この通知を使用して一方的なイベントを送信することはできません。この通知では、NDIS_WWAN_PIN_INFO 構造体が使用されます。
ms.assetid: fa3c2467-2240-423b-b91b-f7e19d5be353
ms.date: 08/08/2017
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_PIN_INFO ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: dce91e3403f90a928cb65706bea5409108c6257b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844787"
---
# <a name="ndis_status_wwan_pin_info"></a>NDIS\_ステータス\_WWAN\_PIN\_情報


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_PIN\_情報通知を使用して OID クエリに応答し、 [oid\_WWAN\_PIN](oid-wwan-pin.md)の要求を設定します。

ミニポートドライバーは、この通知を使用して一方的なイベントを送信することはできません。

この通知では、 [**NDIS\_WWAN\_PIN\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)構造を使用します。

<a name="remarks"></a>注釈
-------

ミニポートドライバーは、クエリ要求への応答として、MB デバイスが現在想定している個人 Id 番号 (PIN) に関する情報を返す必要があります。 次のセクションで説明されているように、ミニポートドライバーは、set 要求に対する応答として、状態通知を返す必要があります。

**WwanPinOperationEnter 要求への応答**

ミニポートドライバーが NDIS\_ステータス\_WWAN\_PIN\_情報通知を使用し**て Wwanpinoperationenter**要求に応答する場合は、次の手順を実装する必要があります。

-   **Wwanpinoperationenter**クエリ要求が正常に実行されると、MB デバイスで PIN が不要になったときに、ミニポートドライバーは**uStatus**を WWAN\_STATUS\_SUCCESS に設定し、 **Pintype**を**wwanpintypenone**に設定する必要があります。

-   **Wwanpinoperationenter**要求が失敗した場合、ミニポートドライバーは、 **uStatus**を WWAN\_ステータス\_エラーに設定し、次の詳細に従って適用可能なデータを含める必要があります。

    -   PIN が無効または PIN が不要: **Wwanpinoperationenter**セット要求では、対応する pin が無効になっているか、MB デバイスで現在想定されていない場合、ミニポートドライバーは**Pintype**を**Wwanpintypenone**に設定する必要があります。 他のすべてのメンバーは無視されます。

    -   PIN はサポートされていません。指定した PIN が MB デバイスでサポートされていない場合、ミニポートドライバーでは、 **uStatus**を WWAN\_\_に設定する必要があります。\_デバイス\_サポートされていません。

    -   PIN の入力: このモードでは、この特定の種類の PIN で**AttemptsRemaining**値が0以外の場合に、pin を再入力する必要があります。 ミニポートドライバーでは、 **pintype**を NDIS\_WWAN の**pintype**と同じ値に設定し\_PIN\_設定する必要があります。

    -   PIN のブロック: **AttemptsRemaining**が0の場合、pin はブロックされます。 PIN のブロック解除操作が使用できない場合、ミニポートドライバーでは、 **uStatus**を WWAN\_STATUS\_FAILURE に設定し、 **Pintype**を**Wwanpintypenone**に設定する必要があります。 他のすべてのメンバーは無視されます。

        **注**  MB デバイスで pin ブロック解除操作がサポートされている場合、ミニポートドライバーは、Pin のブロック解除の手順に従って要求に応答する必要があります。

         

    -   PIN のブロック解除: **AttemptsRemaining**が0の場合、pin はブロックされます。 PIN のブロックを解除するために、該当する場合は、対応する PIN ロック解除キー (PUK) が MB デバイスによって要求されることがあります。 この場合、ミニポートドライバーでは、 **Pintype**を対応する WwanPinType*Xxx*PUK に設定し、関連する詳細を指定する必要があります。

    -   ブロックされた PUK: 失敗した試用の数が、WwanPinType*Xxx*PUK を入力するための事前設定された値を超えると、PUK はブロックされます。 ミニポートドライバーは、 **uStatus**を WWAN\_ステータス\_エラーに設定し、**ピンの種類**を**Wwanpintypenone**に設定して、これを通知する必要があります。 PUK1 がブロックされている場合、ミニポートドライバーは、 **ReadyState**を**WwanReadyStateBadSim**に設定して、NDIS\_STATUS\_WWAN\_READY\_情報を送信する必要があります。

**WwanPinOperationEnable、Wwanpinoperationenable、または Wwanpinoperationenable 要求への応答**

ミニポートドライバーが NDIS\_ステータス\_\_WWAN を使用する場合、\_情報通知をピン留めして、 **Wwanpinoperationenable**、 **wwanpinoperationenable**、および**wwanpinoperationenable**に応答するには、操作は次のとおりです。

-   要求が成功した場合、ミニポートドライバーは**uStatus**を WWAN\_ステータス\_SUCCESS に設定する必要があります。 WWAN_PIN_INFO のその他のメンバーについては、次の状況を参照してください。

-   ミニポートドライバーは、PIN が既に要求された状態にあるときに、pin の有効化と PIN の無効化の操作に対して、 **uStatus**を WWAN\_状態\_設定する必要があります。 ミニポートドライバーでは、 **Pintype**を**Wwanpintypenone**に設定する必要があります。 他のメンバーは無視されます。

-   PIN モードが [無効] から [有効] に変更された場合、PIN の状態は "WwanPinStateNone" になります。

-   PIN1 が有効になっている場合、電源が MB デバイスに設定されていると、PIN の状態が WwanPinStateEnter になります。

-   その他のすべての pin では、デバイス固有の状態に応じて、WwanPinStateNone から WwanPinStateEnter にピンの状態が変化することがあります。

-   PIN はサポートされていません。 PIN 操作が MB デバイスでサポートされていない場合、ミニポートドライバーでは、 **uStatus**を WWAN\_\_に設定する必要があります。\_デバイス\_サポートされていません。 たとえば、PIN2 を有効または無効にすることは、通常、MB デバイスではサポートされていないため、上記のエラーコードを返す必要があります。 他のすべてのメンバーは無視されます。

-   PIN を入力する必要があります。 PIN 操作で PIN を入力する必要がある場合、ミニポートドライバーでは、 **uStatus**を WWAN\_\_状態に設定し、PIN\_REQUIRED と**Pintype**を Wwanpintype*Xxx*に設定する必要があります。 他のメンバーは無視されます。

-   PIN の変更操作: MB デバイスが有効な状態にあるときにのみ PIN の値の変更を制限する場合は、無効の状態の変更要求を、WWAN\_状態\_PIN\_無効にして返す必要があります。

-   PIN の入力: エラーが発生した場合は、ミニポートドライバーで**uStatus**を WWAN\_ステータス\_エラーに設定し、 **PINTYPE**を NDIS\_wwan で指定された\_PIN\_設定したものと同じ値に設定する必要があります。 **AttemptsRemaining**を除き、他のメンバーは無視されます。 PIN が正しく入力されていない場合に発生する可能性があります。

-   PIN のブロック: **AttemptsRemaining**の数がゼロの場合、pin はブロックされます。 PIN のブロック解除操作が使用できない場合、ミニポートドライバーでは、 **uStatus**を WWAN\_STATUS\_FAILURE に設定し、 **Pintype**を**Wwanpintypenone**に設定する必要があります。 **AttemptsRemaining**は0に設定する必要があり、その他のすべてのメンバーは無視されます。

    **注**  MB デバイスで pin ブロック解除操作がサポートされている場合、ミニポートドライバーは、Pin のブロック解除の手順に従って要求に応答する必要があります。

     

-   PIN のブロック解除: **AttemptsRemaining**が0の場合、pin はブロックされます。 PIN のブロックを解除するために、該当する場合は、対応する PUK が MB デバイスによって要求されることがあります。 この場合、ミニポートドライバーは、 **uStatus**を WWAN\_ステータス\_エラー、 **pintype**を対応する Wwanpintype*Xxx*PUK、 **PinState** To **wwanpinstateenter**、 **AttemptsRemaining**に設定する必要があります。には、有効な PUK を入力するために許可されている試行回数が含まれている必要があります。

    MB のデバイスまたは SIM がブロックされた場合は、ミニポートドライバーが、 **ReadyState**を**WwanReadyStateDeviceLocked**に設定してイベント通知を送信する必要があります。

-   PIN1 のブロック時にアクティブな PDP コンテキストがある場合、ミニポートドライバーは PDP コンテキストを非アクティブ化し、PDP の非アクティブ化とリンク状態の変更についてオペレーティングシステムに通知を送信する必要があります。

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
<td><p>Windows 7 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis. h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_PIN](oid-wwan-pin.md)

[**NDIS\_ステータス\_WWAN\_PIN\_情報**](ndis-status-wwan-pin-info.md)

 

 




