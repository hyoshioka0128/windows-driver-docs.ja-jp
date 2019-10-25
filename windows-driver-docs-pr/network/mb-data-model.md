---
title: MB データ モデル
description: MB データ モデル
ms.assetid: 922b6b55-c332-4721-bbd1-571b0e154df3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cedf9e52e1a74cba00494d523ba83d06d7f4e149
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844295"
---
# <a name="mb-data-model"></a>MB データ モデル


MB ドライバーモデルでは、サイズが MB のデバイス機能の抽象化として定義された一連のオブジェクトで構成されるデータモデルを使用します。 各オブジェクトは、一意のオブジェクト識別子 (OID) によって識別され、対応する一連の属性によって定義されます。 一連の属性は、データ構造に編成されます。 デバイスを管理するために、MB サービスと MB のミニポートドライバーは、ネットワークドライバーインターフェイス仕様 (NDIS) によって提供される OID 要求と表示に基づいて、Oid とそれに関連付けられたデータ構造を交換します。

MB のドライバーモデルでは、OID 要求に対しては、*セット*操作と*クエリ*操作のみが使用されます。 MB ドライバーモデルでは、*メソッド*操作は使用されません。 このように、MB ドライバーモデルは、イベント通知とトランザクション通知の両方を使用して、MB デバイスのオブジェクトの状態の変化を示します。 トランザクション通知は、非同期トランザクションの完了も通知します。

次の表に、MB ミニポートドライバーに定義されている Oid と状態の表示と、関連付けられているデータ構造を示します。 MB ミニポートドライバーは、NDIS 6.20 仕様で必要なすべての必須の一般 Oid を実装する必要があります。 NDIS 6.x の一般的な Oid の一覧については、「[一般的な操作 oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/index)」を参照してください。

また、NDIS 仕様で実装するオプションとして記述されていても、MB のミニポートドライバーでは、OID\_GEN\_物理\_メディアを実装する必要があります。

次の表に示す MB Oid の構文とセマンティクスについては、「 [Mb 操作セマンティクス](mb-operational-semantics.md)」で説明されています。 Mb サービスと MB ミニポートドライバーの間のやり取りについては、「 [Mb 操作フローチャート](mb-operation-flowcharts.md)」で説明されています。

## <a name="wwan-specific-oids"></a>WWAN 固有の Oid

| OID と対応するデータ構造 | 操作の設定 |   | クエリ操作 |   | GSM/CDMA |
| ---                                  | ---       | ---       | ---       | ---       |--- |
|                                      | Windows 7 | Windows 8 | Windows 7 | Windows 8 |    |
| [OID\_wwan\_ドライバー\_cap](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-driver-caps)は[ **NDIS\_WWAN\_ドライバー\_cap**を使用します](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_driver_caps) | サポートされない | サポートされない |S | S | GSM、CDMA |
| [OID\_WWAN\_デバイス\_cap](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps)に対応する構造がありません | サポートされない | サポートされない | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | GSM、CDMA |
| [OID\_WWAN\_準備完了\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ready-info)に対応する構造がありません | サポートされていないサポート対象 | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | GSM、CDMA |
| [OID\_wwan\_サービス\_アクティブ化](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-service-activation)†は[ **NDIS\_WWAN\_サービス\_アクティブ化**を使用します](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_service_activation) | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | サポートされない | サポートされない | GSM、CDMA |
| [OID\_wwan\_無線\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-radio-state)は、 [ **NDIS\_WWAN\_設定\_ラジオ\_状態**を使用します](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_radio_state) | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | GSM、CDMA |
| [OID\_wwan\_pin](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin)は、\_PIN を設定して、 [ **NDIS\_\_wwan**を使用します](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin) | 確認が完了していないエイリアスの横には、 | サポートされない | 確認が完了していないエイリアスの横には、 | サポートされない | GSM、CDMA |
| [OID\_WWAN\_PIN\_リスト](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin-list)に対応する構造がありません | サポートされない | サポートされない | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | GSM、CDMA |
| [OID\_wwan\_pin\_ex](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin-ex)は、 [ **NDIS\_WWAN\_設定**\_\_を使用 ex](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin_ex) | サポートされない | 確認が完了していないエイリアスの横には、 | サポートされない | 確認が完了していないエイリアスの横には、 | GSM、CDMA |
| [OID\_WWAN\_HOME\_プロバイダー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-home-provider)に対応する構造がありません | サポートされない | サポートされない | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | GSM、CDMA |
| [OID\_WWAN\_優先\_プロバイダー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-preferred-providers)†は[ **NDIS\_WWAN**を使用し\_優先\_プロバイダーを設定\_](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preferred_providers) | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | GSM のみ |
| [OID\_WWAN\_可視\_プロバイダー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-visible-providers)に対応する構造がありません | サポートされない | サポートされない | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | GSM |
| [OID\_wwan\_登録\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-register-state)は、 [ **NDIS\_WWAN\_設定\_登録\_状態**を使用します](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_register_state) | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | CDMA |
| [OID\_wwan\_シグナル\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-signal-state)では、 [ **NDIS\_WWAN\_設定\_シグナル\_通知**を使用します](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_signal_indication) | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | GSM、CDMA |
| [OID\_wwan\_パケット\_サービス](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-packet-service)は、 [ **NDIS\_WWAN\_を使用して\_パケット\_サービスを設定**します](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_packet_service) | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | GSM、CDMA |
| [OID\_WWAN\_プロビジョニング](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-provisioned-contexts)された\_コンテキスト††は[ **NDIS\_WWAN\_設定\_プロビジョニング**された\_コンテキスト](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_provisioned_context) | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | GSM、CDMA |
| [OID\_wwan\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-connect)は[ **NDIS\_\_wwan を使用して\_コンテキスト\_状態を設定**します](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_context_state) | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | GSM、CDMA |
| [OID\_wwan\_sms\_構成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-configuration)では、 [ **Sms\_構成\_NDIS\_WWAN**を使用します。](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sms_configuration) | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | GSM、CDMA | 
| [OID\_wwan\_sms\_read](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-read)では、 [ **NDIS\_WWAN\_sms\_読み取り**を使用します](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_read) | サポートされない | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 |GSM、CDMA | 
| [OID\_wwan\_sms\_送信](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-send)を使用して、 [ **NDIS\_WWAN\_sms\_送信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send) | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | サポートされない | サポートされない | GSM、CDMA |
| [OID\_wwan\_sms\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-delete)では、 [ **NDIS\_WWAN\_sms\_削除**を使用します](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete) | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | サポートされない | サポートされない |  GSM、CDMA |
| [OID\_wwan\_sms\_ステータス](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-status)は、 [ **NDIS\_WWAN\_sms\_状態**を使用します](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_status) | サポートされない | サポートされない | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | GSM、CDMA |
| [OID\_WWAN\_ベンダ\_特定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-vendor-specific)の†はベンダー定義の構造を使用します | 確認が完了していないエイリアスの横には、 | 確認が完了していないエイリアスの横には、 | サポートされない | サポートされない | GSM、CDMA |
| [OID\_WWAN\_デバイス\_サービス](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-services)に対応する構造がありません | サポートされない | サポートされない | サポートされない | 確認が完了していないエイリアスの横には、 | GSM、CDMA |
| [OID\_wwan\_サブスクライブ\_デバイス\_サービス\_イベント](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-subscribe-device-service-events)は[ **NDIS\_WWAN\_使用して\_デバイス\_サービス\_イベントをサブスクライブ**します](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_subscribe_device_service_events) | サポートされない | 確認が完了していないエイリアスの横には、 | サポートされない | サポートされない | GSM、CDMA |
| [OID\_wwan\_auth\_チャレンジ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-auth-challenge)は、 [ **NDIS\_WWAN\_認証\_チャレンジ**を使用します](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_challenge) | サポートされない | サポートされない | サポートされない | 確認が完了していないエイリアスの横には、 | GSM、CDMA |
| [OID\_wwan\_USSD](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ussd)は、 [ **NDIS\_WWAN\_USSD\_要求**を使用します](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_request) | サポートされない | 確認が完了していないエイリアスの横には、 | サポートされない | サポートされない | GSM |
| [OID\_wwan\_デバイス\_サービス\_コマンド](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-service-command)は、 [ **NDIS\_WWAN\_デバイス\_サービス\_コマンド**を使用します](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_command) | サポートされない | 確認が完了していないエイリアスの横には、 | サポートされない | 確認が完了していないエイリアスの横には、| GSM、CDMA |

> [!NOTE]
> 上の表には、次の注意事項が適用されます。†は、ミニポートドライバーがサポートするオプションの Oid を表します。 オプションの Oid をサポートしていないミニポートドライバーでは、OID\_GEN\_サポートされている\_リストでそれらを返すことはできません。
>
> †は、GSM ベースのデバイスをサポートするミニポートドライバーを表します。これは、必要に応じて、\_コンテキストの設定とクエリ操作によってプロビジョニングされた\_\_WWAN をサポートすることができます。 CDMA ベースのデバイスをサポートするミニポートドライバーでは、必要に応じて、Simple IP を報告する CDMA ベースのデバイスに対して\_コンテキストクエリ操作 (WWAN\_CTRL\_CAPS\_CDMA を使用して、OID\_WWAN\_プロビジョニングすることができ\_SIMPLE\_IP)。
>
> ミニポートドライバーは、オプション以外のすべての Oid をサポートする必要があります。 MB サービスでは、すべての必須の Oid を報告しないミニポートドライバーが無視される場合があります。
> 
> 前の表の「a」と「S」は、OID 要求を完了するためのトランザクションの性質を反映しています。 "A" は、非同期トランザクションの場合は "S"、同期トランザクションの場合は "S" を表します。
>
> 前の表のデータ構造は、操作 Oid の設定と、同期クエリ操作 Oid のデータを返す場合に対応します。
> 
> 次の Oid は、対応するデータ構造内の、 [**WWAN\_list\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_list_header)と呼ばれる、共通の可変長リストデータ構造を共有します。
> -   OID\_WWAN\_準備完了\_情報
> -   OID\_WWAN\_優先\_プロバイダー
> -   OID\_WWAN\_表示される\_プロバイダー
> -   OID\_WWAN\_プロビジョニングされた\_コンテキスト
> -   OID\_WWAN\_SMS\_読み取り 

## <a name="wwan-specific-indications-corresponding-data-structures-and-os-revisions"></a>WWAN 固有のインジケーター、対応するデータ構造、および OS リビジョン

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>指示</strong>および<strong>対応するデータ構造</strong></p></td>
<td align="left"><p><strong>Windows 7 リビジョン</strong></p>
<p><strong>Windows 8 のリビジョン</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps)"><strong>NDIS_STATUS_WWAN_DEVICE_CAPS</strong></a></p>
<p>NDIS_WWAN_DEVICE_CAPS を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)"></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_CAPS_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_CAPS_REVISION_2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_READY_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info)"><strong>NDIS_STATUS_WWAN_READY_INFO</strong></a></p>
<p>NDIS_WWAN_READY_INFO を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ready_info" data-raw-source="[&lt;strong&gt;NDIS_WWAN_READY_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ready_info)"></a></p></td>
<td align="left"><p>NDIS_WWAN_READY_INFO_REVISION_1</p>
<p>NDIS_WWAN_READY_INFO_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-radio-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_RADIO_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-radio-state)"><strong>NDIS_STATUS_WWAN_RADIO_STATE</strong></a></p>
<p>NDIS_WWAN_RADIO_STATE を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_RADIO_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state)"></a></p></td>
<td align="left"><p>NDIS_WWAN_RADIO_STATE_REVISION_1</p>
<p>NDIS_WWAN_RADIO_STATE_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-info" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-info)"><strong>NDIS_STATUS_WWAN_PIN_INFO</strong></a></p>
<p>NDIS_WWAN_PIN_INFO を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PIN_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)"></a></p></td>
<td align="left"><p>NDIS_WWAN_PIN_INFO_REVISION_1</p>
<p>NDIS_WWAN_PIN_INFO_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-list" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_LIST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-list)"><strong>NDIS_STATUS_WWAN_PIN_LIST</strong></a></p>
<p>NDIS_WWAN_PIN_LIST を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PIN_LIST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list)"></a></p></td>
<td align="left"><p>NDIS_WWAN_PIN_LIST_REVISION_1</p>
<p>NDIS_WWAN_PIN_LIST_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-service-activation" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SERVICE_ACTIVATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-service-activation)"><strong>NDIS_STATUS_WWAN_SERVICE_ACTIVATION</strong></a>†</p>
<p>NDIS_WWAN_SERVICE_ACTIVATION_STATUS を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_service_activation_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SERVICE_ACTIVATION_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_service_activation_status)"></a></p></td>
<td align="left"><p>NDIS_WWAN_SERVICE_ACTIVATION_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SERVICE_ACTIVATION_STATUS_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p>
<p>NDIS_WWAN_HOME_PROVIDER を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider" data-raw-source="[&lt;strong&gt;NDIS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider)"></a></p></td>
<td align="left"><p>NDIS_WWAN_HOME_PROVIDER_REVISION_1</p>
<p>NDIS_WWAN_HOME_PROVIDER_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-providers)"><strong>NDIS_STATUS_WWAN_PREFERRED_PROVIDERS</strong></a>†</p>
<p>NDIS_WWAN_PREFERRED_PROVIDERS を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PREFERRED_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers)"></a></p></td>
<td align="left"><p>NDIS_WWAN_PREFERRED_PROVIDERS_REVISION_1</p>
<p>NDIS_WWAN_PREFERRED_PROVIDERS_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p>
<p>NDIS_WWAN_VISIBLE_PROVIDERS を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)"></a></p></td>
<td align="left"><p>NDIS_WWAN_VISIBLE_PROVIDERS_REVISION_1</p>
<p>NDIS_WWAN_VISIBLE_PROVIDERS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_REGISTER_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state)"><strong>NDIS_STATUS_WWAN_REGISTER_STATE</strong></a></p>
<p>NDIS_WWAN_REGISTRATION_STATE を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_registration_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_REGISTRATION_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_registration_state)"></a></p></td>
<td align="left"><p>NDIS_WWAN_REGISTRATION_STATE_REVISION_1</p>
<p>NDIS_WWAN_REGISTRATION_STATE_REVISION_2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-signal-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SIGNAL_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-signal-state)"><strong>NDIS_STATUS_WWAN_SIGNAL_STATE</strong></a></p>
<p>NDIS_WWAN_SIGNAL_STATE を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SIGNAL_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)"></a></p></td>
<td align="left"><p>NDIS_WWAN_SIGNAL_STATE_REVISION_1</p>
<p>NDIS_WWAN_SIGNAL_STATE_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PACKET_SERVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service)"><strong>NDIS_STATUS_WWAN_PACKET_SERVICE</strong></a></p>
<p>NDIS_WWAN_PACKET_SERVICE_STATE を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PACKET_SERVICE_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state)"></a></p></td>
<td align="left"><p>NDIS_WWAN_PACKET_SERVICE_STATE_REVISION_1</p>
<p>NDIS_WWAN_PACKET_SERVICE_STATE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts)"><strong>NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS</strong></a></p>
<p>NDIS_WWAN_PROVISIONED_CONTEXTS を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_provisioned_contexts" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PROVISIONED_CONTEXTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_provisioned_contexts)"></a></p></td>
<td align="left"><p>NDIS_WWAN_PROVISIONED_CONTEXTS_REVISION_1</p>
<p>NDIS_WWAN_PROVISIONED_CONTEXTS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-context-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_CONTEXT_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-context-state)"><strong>NDIS_STATUS_WWAN_CONTEXT_STATE</strong></a></p>
<p>NDIS_WWAN_CONTEXT_STATE を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_CONTEXT_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state)"></a></p></td>
<td align="left"><p>NDIS_WWAN_CONTEXT_STATE_REVISION_1</p>
<p>NDIS_WWAN_CONTEXT_STATE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-configuration" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_CONFIGURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-configuration)"><strong>NDIS_STATUS_WWAN_SMS_CONFIGURATION</strong></a></p>
<p>NDIS_WWAN_SMS_CONFIGURATION を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_configuration" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_CONFIGURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_configuration)"></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_CONFIGURATION_REVISION_1</p>
<p>NDIS_WWAN_SMS_CONFIGURATION_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-receive" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_RECEIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-receive)"><strong>NDIS_STATUS_WWAN_SMS_RECEIVE</strong></a></p>
<p>NDIS_WWAN_SMS_RECEIVE を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_receive" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_RECEIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_receive)"></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_RECEIVE_REVISION_1</p>
<p>NDIS_WWAN_SMS_RECEIVE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-send" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_SEND&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-send)"><strong>NDIS_STATUS_WWAN_SMS_SEND</strong></a></p>
<p>NDIS_WWAN_SMS_SEND_STATUS を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_SEND_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status)"></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_SEND_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SMS_SEND_STATUS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-delete" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_DELETE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-delete)"><strong>NDIS_STATUS_WWAN_SMS_DELETE</strong></a></p>
<p>NDIS_WWAN_SMS_DELETE_STATUS を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_DELETE_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete_status)"></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_DELETE_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SMS_DELETE_STATUS_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-status" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-status)"><strong>NDIS_STATUS_WWAN_SMS_STATUS</strong></a></p>
<p>NDIS_WWAN_SMS_STATUS を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_status)"></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SMS_STATUS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-vendor-specific" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VENDOR_SPECIFIC&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-vendor-specific)"><strong>NDIS_STATUS_WWAN_VENDOR_SPECIFIC</strong></a>†</p>
<p>ベンダー定義の構造を使用する</p></td>
<td align="left"><p>該当なし</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_USSD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd)"><strong>NDIS_STATUS_WWAN_USSD</strong></a></p>
<p>NDIS_WWAN_USSD_EVENT を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_event" data-raw-source="[&lt;strong&gt;NDIS_WWAN_USSD_EVENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_event)"></a></p></td>
<td align="left"><p>NDIS_WWAN_USSD_EVENT_REVISION_1</p>
<p>NDIS_WWAN_USSD_EVENT_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS</strong></a></p>
<p>NDIS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_supported_commands" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_supported_commands)"></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICES_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICES_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-response" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-response)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE</strong></a></p>
<p>NDIS_WWAN_DEVICE_SERVICE_RESPONSE を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_response" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_RESPONSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_response)"></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICE_RESPONSE_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICE_RESPONSE_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-event" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-event)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT</strong></a></p>
<p>NDIS_WWAN_DEVICE_SERVICE_EVENT を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_event" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_EVENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_event)"></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICE_EVENT_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICE_EVENT_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION</strong></a></p>
<p>NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_subscription" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_subscription)"></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-auth-response" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_AUTH_RESPONSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-auth-response)"><strong>NDIS_STATUS_WWAN_AUTH_RESPONSE</strong></a></p>
<p>NDIS_WWAN_AUTH_RESPONSE を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_response" data-raw-source="[&lt;strong&gt;NDIS_WWAN_AUTH_RESPONSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_response)"></a></p></td>
<td align="left"><p>NDIS_WWAN_AUTH_RESPONSE_REVISION_1</p>
<p>NDIS_WWAN_AUTH_RESPONSE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-set-home-provider-complete" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-set-home-provider-complete)"><strong>NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE</strong></a></p>
<p>NDIS_WWAN_SET_HOME_PROVIDER を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_home_provider" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SET_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_home_provider)"></a></p></td>
<td align="left"><p>該当なし</p>
<p>NDIS_WWAN_HOME_PROVIDER_REVISION_2</p></td>
</tr>
</tbody>
</table>

> [!NOTE]
> 次の注意事項が前の表に適用されます。†は、ミニポートドライバーがサポートする可能性があるオプションの表示を表します。 ミニポートドライバーでオプションの OID がサポートされている場合、ミニポートドライバーも対応する表示をサポートする必要があることに注意してください。 

## <a name="wwan-specific-indication-support-for-gsm-cdma-and-unsolicited-indications"></a>GSM、CDMA、および要請されていない表示をサポートする WWAN 固有の指示

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>示す値</strong></p></td>
<td align="left"><p><strong>GSM</strong></p></td>
<td align="left"><p><strong>CDMA</strong></p></td>
<td align="left"><p><strong>自主</strong></p>
<p><strong>示す値</strong></p>
<p><strong>許可?</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps)"><strong>NDIS_STATUS_WWAN_DEVICE_CAPS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_READY_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info)"><strong>NDIS_STATUS_WWAN_READY_INFO</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-radio-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_RADIO_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-radio-state)"><strong>NDIS_STATUS_WWAN_RADIO_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-info" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-info)"><strong>NDIS_STATUS_WWAN_PIN_INFO</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-list" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_LIST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-list)"><strong>NDIS_STATUS_WWAN_PIN_LIST</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-service-activation" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SERVICE_ACTIVATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-service-activation)"><strong>NDIS_STATUS_WWAN_SERVICE_ACTIVATION</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-providers)"><strong>NDIS_STATUS_WWAN_PREFERRED_PROVIDERS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_REGISTER_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state)"><strong>NDIS_STATUS_WWAN_REGISTER_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-signal-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SIGNAL_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-signal-state)"><strong>NDIS_STATUS_WWAN_SIGNAL_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PACKET_SERVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service)"><strong>NDIS_STATUS_WWAN_PACKET_SERVICE</strong></a></p>
<p>NDIS_WWAN_PACKET_SERVICE_STATE を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PACKET_SERVICE_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state)"></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts)"><strong>NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-context-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_CONTEXT_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-context-state)"><strong>NDIS_STATUS_WWAN_CONTEXT_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-configuration" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_CONFIGURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-configuration)"><strong>NDIS_STATUS_WWAN_SMS_CONFIGURATION</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-receive" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_RECEIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-receive)"><strong>NDIS_STATUS_WWAN_SMS_RECEIVE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-send" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_SEND&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-send)"><strong>NDIS_STATUS_WWAN_SMS_SEND</strong></a></p>
<p>NDIS_WWAN_SMS_SEND_STATUS を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_SEND_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status)"></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-delete" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_DELETE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-delete)"><strong>NDIS_STATUS_WWAN_SMS_DELETE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-status" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-status)"><strong>NDIS_STATUS_WWAN_SMS_STATUS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-vendor-specific" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VENDOR_SPECIFIC&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-vendor-specific)"><strong>NDIS_STATUS_WWAN_VENDOR_SPECIFIC</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_USSD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd)"><strong>NDIS_STATUS_WWAN_USSD</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-response" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-response)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-event" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-event)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-auth-response" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_AUTH_RESPONSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-auth-response)"><strong>NDIS_STATUS_WWAN_AUTH_RESPONSE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-set-home-provider-complete" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-set-home-provider-complete)"><strong>NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
</tbody>
</table> 

## <a name="multi-carrier-specific-oids"></a>複数のキャリアに固有の Oid

次の変更は、マルチキャリアモードをサポートする NDIS 6.30 ミニポートドライバーに適用されます。 ミニポートドライバーがマルチキャリアモードをサポートしていない場合は、前の表を参照してください。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>OID</strong>と<strong>Windows 8 対応データ構造</strong></p></td>
<td align="left"><p><strong>クエリ操作</strong></p></td>
<td align="left"><p><strong>操作の設定</strong></p></td>
<td align="left"><p><strong>GSM/CDMA</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-home-provider" data-raw-source="[OID_WWAN_HOME_PROVIDER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-home-provider)">OID_WWAN_HOME_PROVIDER</a></p>
<p>NDIS_WWAN_SET_HOME_PROVIDER を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_home_provider" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SET_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_home_provider)"></a></p></td>
<td align="left"><p>確認が完了していないエイリアスの横には、</p></td>
<td align="left"><p>確認が完了していないエイリアスの横には、</p></td>
<td align="left"><p>GSM、CDMA</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-preferred-providers" data-raw-source="[OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-preferred-providers)">OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preferred_multicarrier_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SET_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preferred_multicarrier_providers)"><strong>NDIS_WWAN_SET_PREFERRED_MULTICARRIER_PROVIDERS</strong></a>を使用します。 <strong>PreferredListHeader</strong>を<strong>WwanStructProvider2</strong>に設定し、構造体を WWAN_PROVIDER2 に設定する必要があります。</p></td>
<td align="left"><p>確認が完了していないエイリアスの横には、</p></td>
<td align="left"><p>確認が完了していないエイリアスの横には、</p></td>
<td align="left"><p>GSM、CDMA</p></td>
</tr>
</tbody>
</table> 

## <a name="multi-carrier-specific-indications-corresponding-data-structures-and-os-revisions"></a>マルチキャリア固有の指示、対応するデータ構造、OS リビジョン

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>指示</strong>および<strong>対応するデータ構造</strong></p></td>
<td align="left"><p><strong>Windows 8 のリビジョン</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p>
<p>NDIS_WWAN_HOME_PROVIDER2 を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider2" data-raw-source="[&lt;strong&gt;NDIS_WWAN_HOME_PROVIDER2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider2)"></a></p></td>
<td align="left"><p>NDIS_WWAN_HOME_PROVIDER_REVISION_2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers)"><strong>NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</strong></a></p>
<p>NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers)"></a></p></td>
<td align="left"><p>NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS_REVISION_1. <strong>PreferredListHeader</strong>を<strong>WwanStructProvider2</strong>に設定し、リストに WWAN_PROVIDER2 構造体を含める必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p>
<p>NDIS_WWAN_VISIBLE_PROVIDERS を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)"></a></p></td>
<td align="left"><p>NDIS_WWAN_VISIBLE_PROVIDERS_REVISION_1. <strong>VisibleListHeader</strong>を<strong>WwanStructProvider2</strong>に設定し、リストに WWAN_PROVIDER2 構造体を含める必要があります。</p></td>
</tr>
</tbody>
</table> 

## <a name="multi-carrier-specific-indication-support-for-gsm-cdma-and-unsolicited-indications"></a>GSM、CDMA、および要請されていない表示をサポートするマルチキャリア固有の表示

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>指示</strong>および<strong>対応するデータ構造</strong></p></td>
<td align="left"><p><strong>GSM</strong></p></td>
<td align="left"><p><strong>CDMA</strong></p></td>
<td align="left"><p><strong>自主</strong></p>
<p><strong>示す値</strong></p>
<p><strong>許可?</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers)"><strong>NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p>
<p>NDIS_WWAN_VISIBLE_PROVIDERS を使用する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)"></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
</tbody>
</table>
