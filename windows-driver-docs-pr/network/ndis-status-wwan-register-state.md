---
title: NDIS_STATUS_WWAN_REGISTER_STATE
description: ミニポート ドライバーでは、MB サービスに MB デバイスの登録の状態に変更を通知 NDIS_STATUS_WWAN_REGISTER_STATE 通知を使用します。
ms.assetid: 3da8489a-6ca3-4897-9794-86665ce10e81
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_REGISTER_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 112703407a936bd52aa90f2e3c0921a0f5f4e368
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557939"
---
# <a name="ndisstatuswwanregisterstate"></a>NDIS\_状態\_WWAN\_登録\_状態


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_登録\_状態通知 MB サービスに MB デバイスの登録の状態に変更を通知します。

ミニポート ドライバーには、この通知が不要なイベントを送信できます。

この通知を使用して、 [ **NDIS\_WWAN\_登録\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567917)構造体。

<a name="remarks"></a>注釈
-------

デバイスの変更の登録状態として MB サービスがユーザーに適切な状態を反映ように、ミニポート ドライバーは適切なインジケーターを送信する必要があります。

さまざまな理由のための登録状態を変更します。 直接可能性*設定*OID の MB サービスからの要求\_WWAN\_登録\_状態から一時的な状態遷移など**WwanRegisterStateSearching**に**WwanRegisterStateHome**します。 自動のプロバイダーの選択の場合、ミニポート ドライバーによって自動の操作からその可能性があります。 最後に、ネットワークの可用性の変更によって発生した可能性がある、たとえば、ネットワークの対象範囲が失われる可能性がありますからの移行で**WwanRegisterStateHome**に**WwanRegisterStateDeregistered**します。

MB サービス OID による変更を除く\_WWAN\_登録\_状態を要求するミニポート ドライバーは、基になる原因に関係なく、登録状態が変更されるたびに MB サービスに通知されます。

CDMA デバイスをサポートしない MB のサービスが開始した登録解除します。 ただしが開始したデバイスの登録状態変更の MB サービスには、可用性や通信事業者ネットワークの可用性以外に基づく通知を送信する必要があります。 CDMA デバイスは、自動登録を行う必要があります。

ミニポート ドライバーは、電源アップ、モードに関係なく、現在の登録 - 自動または手動での自動登録を実行するデバイスの登録が成功登録状態通知を送信する必要があります。

手動登録は、MB サービスはのみを開始して登録後、ミニポート ドライバーでは、ことを示します**ReadyState**は**WwanReadyStateInitialized**します。

ミニポート ドライバーは、応答中に、次のガイドラインを使用する必要があります*設定*要求。

-   ドライバーはの一時的な状態で応答する必要があります、*設定*要求。 登録のための一時的な状態が**WwanRegisterStateSearching**します。

-   ときに**RegisterAction**に設定されている**WwanRegisterActionManual**ミニポート ドライバーは、ミニポート ドライバーを返す、要求を受信すると、プロバイダーが表示されない場合、エラー コード WWAN\_状態\_プロバイダー\_いない\_表示します。 手動モードを設定できなかったのため、デバイスは自動登録に切り替えられませんする必要があります。 デバイスが別のネットワークに手動で登録する以前のセットの場合は、この要求は、要求で指定されたネットワークに登録するデバイスを変更する必要があります。 値**RegisterState**に設定する必要があります、要求に応答**WwanRegisterStateDeregistered**します。

-   ときに**RegisterAction**に設定されている**WwanRegisterActionManual**ミニポート ドライバーが要求されている、WWAN で応答する必要がなければいけないのと同じネットワークに既に登録されている場合、\_状態\_成功します。

-   OID のセットで要求されたデータ クラスを登録するドライバーを試みる必要がある\_WWAN\_登録要求。 ミニポート ドライバーは、要求されたデータ クラスを登録できない場合、は、最適なデータ クラスを登録する必要があります。 これは、いくつかその他のデータのクラスを使用して、プロバイダー (自動と手動登録モード) に、デバイスが既に登録されている場合にも適用します。 データ クラスを変更する必要があります NDIS 可能性も\_状態\_WWAN\_パケット\_サービス通知します。

-   ときに**RegisterAction**に設定されている**WwanRegisterActionManual**オプションは OFF ですおよび、ミニポート ドライバーのプログラムの手動登録モードにデバイスとトランザクションに要求を完了する必要があります。通知します。 **RegisterState**に設定する必要があります**WwanRegisterStateDeregistered**します。 デバイスは、状態のオプションに変更し、イベント通知を送信する必要があります手動登録を試みる必要があります。

-   ときに**RegisterAction**に設定されている**WwanRegisterActionAutomatic**オプションは OFF ですと、ミニポート ドライバーの自動登録モードにデバイスをプログラムする必要がありますおよびを使用して要求を完了する必要があります、。トランザクション通知します。 **RegisterState**に設定する必要があります**WwanRegisterStateDeregistered**します。 デバイスは、無線の状態にし、イベント通知を送信する必要がある、自動登録を行う必要があります。

-   登録の緊急の状態が発生した場合 ( **WwanRegisterStateDenied**)、 **uStatus** WWAN に設定する必要があります\_状態\_成功と NDIS\_の状態\_WWAN\_準備\_に情報通知を送信する必要があります**EmergencyMode**に設定**WwanEmergencyModeOn**します。

-   状態を使用するため**WwanRegisterStateDeregistered**ミニポート ドライバーは、次のガイドラインを使用する必要があります。

    -   **WwanRegisterStateDeregistered**ラジオにある要求が OFF MB サービスに通知するために、ミニポート ドライバーによって使用されます**RegisterAction**が完了します。

    -   **WwanRegisterStateDeregistered**ミニポート ドライバーが開始したネットワークの MB サービスに通知するための登録解除によって使用されます。

    -   **WwanRegisterStateDeregistered**ミニポート ドライバーではネットワークの範囲外のためのネットワークに接続が切断の MB サービスに通知するために使用します。

-   GSM と CDMA デバイスでは、可用性または PS 接続の配送業者の使用不能に通知する登録の状態通知を送信する必要があります。 適切な登録の状態: のいずれかのイベント通知を送信する必要があります MB デバイスは、通信事業者ネットワークの可用性を検出すると**WwanRegisterStateHome**、 **WwanRegisterStateRoaming**、または**WwanRegisterStatePartner**します。 通信事業者ネットワーク信号、イベント通知を失うことに**WwanRegisterStateDeregistered** MB サービスを示す必要があります。

ミニポート ドライバーには、次の規則に従って、クエリの結果が返されます。

-   ミニポート ドライバーを設定するものと、デバイスが登録時に、プロバイダーにロックしようとして、 **RegisterState**として**WwanRegisterStateSearching**します。 両方の**ProviderName**と**RoamingText**にメンバーを設定する必要があります**NULL**します。 手動登録のモードが発生した場合**ProviderId** ProviderId が最後の手動登録のセットの要求から入力する必要があります。 **ProviderId**に設定することができます**NULL**自動登録モードが発生した場合。

-   ミニポート ドライバーはなど、登録の最後に安定した状態に移動最終的にこれは、一時的な状態**WwanRegisterStateHome**、 **WwanRegisterStatePartner**、または**WwanRegisterStateRoaming** ; 登録が完了または**WwanRegisterStateDenied**の登録の緊急状態です。

-   ミニポート ドライバーを返すものとかどうか、すべてのプロバイダーでは、デバイスが登録されていない、 **WwanRegisterStateDeregistered**します。 両方の**ProviderName**と**RoamingText**にメンバーを設定する必要があります**NULL**します。 手動登録のモードが発生した場合**ProviderId** ProviderId が最後の手動登録のセットの要求から入力する必要があります。 **ProviderId**に設定することができます**NULL**自動登録モードが発生した場合。

-   ミニポート ドライバーを設定するものと、デバイスがホーム プロバイダーに登録された場合**RegisterState**として**WwanRegisterStateHome**します。 **ProviderId**メンバーは、ホーム プロバイダー ID を設定する必要があります **ProviderName**ホーム プロバイダー ネットワークの名前に設定する必要があります。 **RoamingText**にメンバーを設定する必要があります**NULL**します。

-   ミニポート ドライバーを設定するものと、デバイスがローミング プロバイダーに登録された場合**RegisterState**として**WwanRegisterStatePartner**場合は、プロバイダーは、優先ローミング パートナーまたはだけ**WwanRegisterStateRoaming**ローミング パートナーでは、それぞれします。 値を設定は、ミニポート ドライバーは、2 つを区別しない場合、 **WwanRegisterStateRoaming**します。 **ProviderId**メンバーは、デバイスが登録されて現在のプロバイダーのプロバイダー ID に設定するものとし、 **ProviderName**現在の登録済みのプロバイダー名を使用して入力する必要があります。 **RoamingText**場合、プロバイダー固有の文字列値をメンバーを設定する必要がありますが存在するまたは**NULL**それ以外の場合。

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


[**NDIS\_WWAN\_登録\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567917)

[OID\_WWAN\_登録\_状態](oid-wwan-register-state.md)

 

 




