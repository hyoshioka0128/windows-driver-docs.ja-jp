---
title: NDIS_STATUS_WWAN_REGISTER_STATE
description: ミニポートドライバーは、NDIS_STATUS_WWAN_REGISTER_STATE 通知を使用して、MB デバイスの登録状態の変更を MB サービスに伝達します。
ms.assetid: 3da8489a-6ca3-4897-9794-86665ce10e81
ms.date: 08/08/2017
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_REGISTER_STATE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: c1474227e459d3045ecf2c04cd354a0cc770fb5c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844649"
---
# <a name="ndis_status_wwan_register_state"></a>NDIS\_ステータス\_WWAN\_登録\_状態


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_登録\_状態通知を使用して、MB デバイスの登録状態の変更を MB サービスに伝達します。

ミニポートドライバーは、この通知を使用して、要請されていないイベントも送信できます。

この通知では、 [**NDIS\_WWAN\_登録\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_registration_state)構造を使用します。

<a name="remarks"></a>注釈
-------

デバイスの登録状態が変化すると、ミニポートドライバーは適切な情報を送信して、MB サービスがユーザーに正しい状態を反映できるようにする必要があります。

さまざまな理由により、登録状態が変更されます。 OID\_\_WWAN に対する MB サービスからの*設定*要求によって、 **wwanregisterstatesearching** **wwanregisterstatesearching**への一時的な状態遷移などの\_状態が登録されることがあります。 また、自動的にプロバイダーを選択した場合は、ミニポートドライバーによる自動操作によっても発生する可能性があります。 最後に、ネットワークの可用性の変更によって発生する可能性があります。たとえば、ネットワークカバレッジが失われると、 **Wwanregisterstatehome**から**Wwanregisterstateregisterに**移行される可能性があります。

\_状態要求の登録\_、MB サービス\_OID によって発生する変更を除き、原因にかかわらず、登録状態が変化するたびに、ミニポートドライバーは MB サービスに通知します。

CDMA デバイスは、MB サービスで開始された登録と登録解除をサポートしていません。 ただし、通信事業者ネットワークの可用性または非可用性に基づいて、デバイスによって開始される登録状態変更通知は、MB サービスに送信される必要があります。 CDMA デバイスは自動登録を行う必要があります。

現在の登録モード (自動または手動) に関係なく、電源投入時に自動登録を行うデバイスの場合、正常に登録されると、ミニポートドライバーが登録状態通知を送信する必要があります。

手動登録の場合、MB サービスは、ミニポートドライバーが**ReadyState**が**WwanReadyStateInitialized**であることを示す場合にのみ、登録を開始します。

ミニポートドライバーは、次のガイドラインを使用して、*設定*要求に応答する必要があります。

-   ドライバーは、*設定*された要求に対して一時的な状態では応答しません。 登録の一時的な状態は、 **Wwanregisterstatesearching**です。

-   **Registeraction**が**Wwanregisteractionmanual**に設定されている場合、ミニポートドライバーが要求を受信したときにプロバイダーが表示されない場合、ミニポートドライバーはエラーコード WWAN\_ステータス\_プロバイダー\_返しません\_表示されます。 手動モードの設定でエラーが発生したため、デバイスを自動登録に切り替えることはできません。 デバイスが以前に別のネットワークに手動で登録するように設定されている場合、この要求では、要求で指定されたネットワークに登録するようにデバイスを変更する必要があります。 要求に応答する**Registerstate**の値は、 **Wwanregisterstateregisterに**設定する必要があります。

-   **Registeraction**が**Wwanregisteractionmanual**に設定されている場合、ミニポートドライバーが、要求された同じネットワークに既に登録されていると、WWAN\_STATUS\_SUCCESS に応答します。

-   ドライバーは、set OID\_WWAN\_REGISTER 要求で、要求されたデータクラスへの登録を試みます。 ミニポートドライバーが、要求されたデータクラスに登録できない場合は、最適なデータクラスに登録する必要があります。 これは、デバイスが他のデータクラスを使用して既にプロバイダー (自動および手動登録モード) に登録されている場合にも適用されます。 また、データクラスを変更すると、NDIS\_ステータス\_WWAN\_パケット\_サービス通知も発生します。

-   **Registeraction**が**Wwanregisteractionmanual**に設定されていて、ラジオがオフの場合、ミニポートドライバーはデバイスを手動で登録モードにプログラムし、トランザクション通知を使用して要求を完了する必要があります。 **Registerstate**は、 **Wwanregisterstateregisterに**設定する必要があります。 デバイスは、ラジオがオンの状態に変更されたときに手動登録を試行し、イベント通知を送信する必要があります。

-   **Registeraction**が**Wwanregisteractionautomatic**に設定されていて、ラジオがオフの場合、ミニポートドライバーはデバイスを自動登録モードにプログラミングする必要があり、トランザクション通知を使用して要求を完了する必要があります。 **Registerstate**は、 **Wwanregisterstateregisterに**設定する必要があります。 デバイスは、ラジオがオンの状態になったときに自動登録を行う必要があり、イベント通知を送信する必要があります。

-   緊急時の登録 ( **Wwanregisterstatedenied**発生した場合) の場合、 **uStatus**は、WWAN\_STATUS\_SUCCESS および NDIS\_STATUS\_WWAN\_READY\_INFO 通知をと共に送信する必要があります。**EmergencyMode**を**WwanEmergencyModeOn**に設定します。

-   状態**Wwanregisterstateregisterを**使用するには、ミニポートドライバーで次のガイドラインを使用する必要があります。

    -   **Wwanregisterstateregisterは**、オプションがオフであるにもかかわらず**registeraction**の要求が完了したことを MB サービスに通知するために、ミニポートドライバーによって使用されます。

    -   **Wwanregisterstateregisterは**、ネットワークによって開始された登録解除の MB サービスに通知するために、ミニポートドライバーによって使用されます。

    -   **Wwanregisterstateregisterは**、ネットワークに接続されていないためにネットワークへの接続が失われたことを MB サービスに通知するために、ミニポートドライバーによって使用されます。

-   GSM および CDMA デバイスは、PS 接続の通信事業者の可用性または非可用性を通知するために、登録状態通知を送信する必要があります。 MB デバイスが通信事業者ネットワークの可用性を検出すると、適切な登録状態 ( **Wwanregisterstatehome**、 **WwanRegisterStateRoaming**、または**wwanregisterstatehome** ) のいずれかを使用してイベント通知を送信する必要があります. 通信事業者のネットワーク信号が失われた場合は、 **Wwanregisterstateregisterを**含むイベント通知を MB サービスに示す必要があります。

ミニポートドライバーは、次の規則に従ってクエリの結果を返します。

-   デバイスが登録中にプロバイダーをロックしようとすると、ミニポートドライバーは**Registerstate**を**Wwanregisterstatesearching**として設定します。 **ProviderName**と**RoamingText**の両方のメンバーを**NULL**に設定する必要があります。 手動登録モードの場合は、前回の手動登録セット要求からの ProviderId を使用して**providerid**を入力する必要があります。 自動登録モードの場合は、 **ProviderId**を**NULL**に設定できます。

-   これは一時的な状態です。ミニポートドライバーは、登録の最後 (たとえば、 **Wwanregisterstatehome**、 **wwanregisterstatehome**、 **WwanRegisterStateRoaming**など) の最後に安定した状態に移行します。製品または、ステートレスな状態登録を行う場合は、 **Wwanregisterstatedenied**を使用します。

-   デバイスがプロバイダーに登録されていない場合、ミニポートドライバーは、 **Wwanregisterstateregisterを**返します。 **ProviderName**と**RoamingText**の両方のメンバーを**NULL**に設定する必要があります。 手動登録モードの場合は、前回の手動登録セット要求からの ProviderId を使用して**providerid**を入力する必要があります。 自動登録モードの場合は、 **ProviderId**を**NULL**に設定できます。

-   デバイスがホームプロバイダーに登録されている場合、ミニポートドライバーは**Registerstate**を**Wwanregisterstatehome**として設定します。 **ProviderId**メンバーは、HOME プロバイダー ID に設定されている必要があります。 **ProviderName**は、ホームプロバイダーネットワークの名前に設定する必要があります。 **RoamingText**メンバーは**NULL**に設定する必要があります。

-   デバイスがローミングプロバイダーに登録されている場合、そのプロバイダーが優先ローミングパートナーであるか、ローミングパートナーの**WwanRegisterStateRoaming**のみである場合、ミニポートドライバーは**Registerstate**を**wwanregisterstatepartner**として設定する必要があります。4.3. ミニポートドライバーがこの2つを区別しない場合は、値を**WwanRegisterStateRoaming**に設定します。 **ProviderId**メンバーは、デバイスが登録されている現在のプロバイダーのプロバイダー ID に設定されている必要があります。 **ProviderName**には、現在登録されているプロバイダー名を入力する必要があります。 **RoamingText**メンバーは、存在する場合はプロバイダー固有の文字列値に設定し、それ以外の場合は**NULL**に設定する必要があります。

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


[**NDIS\_WWAN\_登録\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_registration_state)

[OID\_WWAN\_\_状態の登録](oid-wwan-register-state.md)

 

 




