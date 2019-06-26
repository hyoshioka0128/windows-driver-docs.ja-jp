---
title: MB データ モデル
description: MB データ モデル
ms.assetid: 922b6b55-c332-4721-bbd1-571b0e154df3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03efe34af831856edbdf568c12d52e365aca5701
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379410"
---
# <a name="mb-data-model"></a>MB データ モデル


MB ドライバー モデルは、MB デバイスの機能の抽象化として定義されているオブジェクトのセットで構成されるデータ モデルを使用します。 各オブジェクトは、一意のオブジェクト識別子 (OID) で識別され、対応する属性のセットによって定義されます。 一連の属性は、データ構造に編成されます。 デバイスを管理するには、MB サービスと MB のミニポート ドライバー Oid と OID 要求と Network Driver Interface Specification (NDIS) によって提供されている指示に基づいてそれらに関連付けられているデータ構造体を交換します。

のみ MB ドライバー モデルで*設定*と*クエリ*OID 要求の操作が使用されます。 MB ドライバー モデルが使用しない*メソッド*操作。 MB ドライバー モデルは、MB デバイスのオブジェクトの状態の変化を示すイベントとトランザクションの通知の両方を使用します。 トランザクションの通知では、非同期のトランザクションの完了も通知します。

次の表には、Oid と関連付けられているデータ構造体として MB ミニポート ドライバーでは、定義されている状態のインジケーターが一覧表示します。 MB のミニポート ドライバーでは、NDIS 6.20 が動作の仕様を必要とするすべての必須全般の Oid を実装する必要があります。 NDIS の一般的な Oid の一覧については、6.x を参照してください[一般的な操作の Oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/index)します。

さらに、MB ミニポート ドライバーが OID を実装する必要があります\_GEN\_物理\_中の場合でも、NDIS 仕様が実装するためにオプションとして説明します。

構文とセマンティクス MB Oid が次の表に示すは記載[MB 演算のセマンティクス](mb-operational-semantics.md)します。 MB サービスと MB ミニポート ドライバー間の相互作用が記載されて[MB 操作フローチャート](mb-operation-flowcharts.md)します。

## <a name="wwan-specific-oids"></a>WWAN に固有の Oid

| OID と対応するデータ構造体 | 設定操作 |   | クエリ操作 |   | GSM/CDMA |
| ---                                  | ---       | ---       | ---       | ---       |--- |
|                                      | Windows 7 | Windows 8 | Windows 7 | Windows 8 |    |
| [OID\_WWAN\_ドライバー\_CAP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-driver-caps)使用[ **NDIS\_WWAN\_ドライバー\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_driver_caps) | サポートされていません | サポートされていません |S | S | GSM、CDMA |
| [OID\_WWAN\_デバイス\_CAP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps)対応する構造がありません | サポートされていません | サポートされていません | A | A | GSM、CDMA |
| [OID\_WWAN\_準備\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ready-info)対応する構造がありません | サポートされている Not がサポートされていません | A | A | GSM、CDMA |
| [OID\_WWAN\_サービス\_アクティベーション](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-service-activation)† 使用[ **NDIS\_WWAN\_サービス\_アクティブ化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_service_activation) | A | A | サポートされていません | サポートされていません | GSM、CDMA |
| [OID\_WWAN\_ラジオ\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-radio-state)使用[ **NDIS\_WWAN\_設定\_ラジオ\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_radio_state) | A | A | A | A | GSM、CDMA |
| [OID\_WWAN\_PIN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin)使用[ **NDIS\_WWAN\_設定\_暗証番号 (pin)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin) | A | サポートされていません | A | サポートされていません | GSM、CDMA |
| [OID\_WWAN\_PIN\_一覧](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin-list)対応する構造がありません | サポートされていません | サポートされていません | A | A | GSM、CDMA |
| [OID\_WWAN\_PIN\_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin-ex)使用[ **NDIS\_WWAN\_設定\_PIN\_例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin_ex) | サポートされていません | A | サポートされていません | A | GSM、CDMA |
| [OID\_WWAN\_ホーム\_プロバイダー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-home-provider)対応する構造がありません | サポートされていません | サポートされていません | A | A | GSM、CDMA |
| [OID\_WWAN\_優先\_プロバイダー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-preferred-providers)† 使用[ **NDIS\_WWAN\_設定\_優先\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preferred_providers) | A | A | A | A | GSM のみ |
| [OID\_WWAN\_VISIBLE\_プロバイダー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-visible-providers)対応する構造がありません | サポートされていません | サポートされていません | A | A | GSM |
| [OID\_WWAN\_登録\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-register-state)使用[ **NDIS\_WWAN\_設定\_登録\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_register_state) | A | A | A | A | CDMA |
| [OID\_WWAN\_信号\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-signal-state)使用[ **NDIS\_WWAN\_設定\_信号\_を示す値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_signal_indication) | A | A | A | A | GSM、CDMA |
| [OID\_WWAN\_パケット\_サービス](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-packet-service)使用[ **NDIS\_WWAN\_設定\_パケット\_サービス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_packet_service) | A | A | A | A | GSM、CDMA |
| [OID\_WWAN\_プロビジョニング済み\_コンテキスト](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-provisioned-contexts)† を使用して[ **NDIS\_WWAN\_設定\_プロビジョニング済み\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_provisioned_context) | A | A | A | A | GSM、CDMA |
| [OID\_WWAN\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-connect)使用[ **NDIS\_WWAN\_設定\_コンテキスト\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_context_state) | A | A | A | A | GSM、CDMA |
| [OID\_WWAN\_SMS\_構成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-configuration)使用[ **NDIS\_WWAN\_設定\_SMS\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sms_configuration) | A | A | A | A | GSM、CDMA | 
| [OID\_WWAN\_SMS\_読み取り](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-read)使用[ **NDIS\_WWAN\_SMS\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_read) | サポートされていません | A | A | A |GSM、CDMA | 
| [OID\_WWAN\_SMS\_送信](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-send)使用[ **NDIS\_WWAN\_SMS\_送信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send) | A | A | サポートされていません | サポートされていません | GSM、CDMA |
| [OID\_WWAN\_SMS\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-delete)使用[ **NDIS\_WWAN\_SMS\_削除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete) | A | A | サポートされていません | サポートされていません |  GSM、CDMA |
| [OID\_WWAN\_SMS\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-status)使用[ **NDIS\_WWAN\_SMS\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_status) | サポートされていません | サポートされていません | A | A | GSM、CDMA |
| [OID\_WWAN\_ベンダー\_特定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-vendor-specific)† はベンダ定義の構造を使用 | A | A | サポートされていません | サポートされていません | GSM、CDMA |
| [OID\_WWAN\_デバイス\_サービス](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-services)対応する構造がありません | サポートされていません | サポートされていません | サポートされていません | A | GSM、CDMA |
| [OID\_WWAN\_購読\_デバイス\_サービス\_イベント](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-subscribe-device-service-events)使用[ **NDIS\_WWAN\_購読\_デバイス\_サービス\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_subscribe_device_service_events) | サポートされていません | A | サポートされていません | サポートされていません | GSM、CDMA |
| [OID\_WWAN\_AUTH\_チャレンジ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-auth-challenge)使用[ **NDIS\_WWAN\_AUTH\_チャレンジ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_challenge) | サポートされていません | サポートされていません | サポートされていません | A | GSM、CDMA |
| [OID\_WWAN\_USSD](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ussd)使用[ **NDIS\_WWAN\_USSD\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_request) | サポートされていません | A | サポートされていません | サポートされていません | GSM |
| [OID\_WWAN\_デバイス\_サービス\_コマンド](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-service-command)使用[ **NDIS\_WWAN\_デバイス\_サービス\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_command) | サポートされていません | A | サポートされていません | A| GSM、CDMA |

> [!NOTE]
> 前の表を次の注意事項が適用されます: † ミニポート ドライバーがサポートできる省略可能な Oid を表します。 省略可能な Oid をサポートしていないミニポート ドライバー返す必要があるいないに OID\_GEN\_サポートされている\_一覧。
>
> † 表す OID をサポートできる必要に応じて、GSM ベースのデバイスをサポートするミニポート ドライバー\_WWAN\_プロビジョニング済み\_コンテキストの設定し、操作をクエリします。 CDMA ベースのデバイスをサポートするミニポート ドライバーは、OID をサポートできます必要に応じて\_WWAN\_プロビジョニング済み\_コンテキストは、CDMA ベースのデバイスで単純な IP を報告するための操作をクエリ (WWAN\_CTRL\_キャップ\_CDMA\_単純\_IP)。
>
> ミニポート ドライバーでは、すべて省略できない Oid をサポートする必要があります。 MB サービスは、すべての必須の Oid は報告されません任意のミニポート ドライバーを無視することができます。
> 
> "A"と"S"セットおよびクエリ操作列上の表では、OID 要求を完了するため、トランザクションの性質を反映します。"A"の略非同期トランザクションと"S"の同期トランザクションです。
>
> 上記の表に、データ構造には、操作の Oid を設定して、データ同期のクエリ操作の Oid を返しますが対応しています。
> 
> 一般的な可変長のリストのデータ構造と呼ばれる次の Oid 共有[ **WWAN\_一覧\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_list_header)対応するデータ構造で。
> -   OID\_WWAN\_準備\_情報
> -   OID\_WWAN\_優先\_プロバイダー
> -   OID\_WWAN\_VISIBLE\_プロバイダー
> -   OID\_WWAN\_プロビジョニング済み\_コンテキスト
> -   OID\_WWAN\_SMS\_読み取り 

## <a name="wwan-specific-indications-corresponding-data-structures-and-os-revisions"></a>WWAN に固有の問題、対応するデータ構造、および OS のバージョン

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Indication</strong>と<strong>対応するデータ構造体</strong></p></td>
<td align="left"><p><strong>Windows 7 のリビジョン</strong></p>
<p><strong>Windows 8 のリビジョン</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps)"><strong>NDIS_STATUS_WWAN_DEVICE_CAPS</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)"> <strong>NDIS_WWAN_DEVICE_CAPS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_CAPS_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_CAPS_REVISION_2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_READY_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info)"><strong>NDIS_STATUS_WWAN_READY_INFO</strong></a></p>
<p>uses <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_ready_info" data-raw-source="[&lt;strong&gt;NDIS_WWAN_READY_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_ready_info)"><strong>NDIS_WWAN_READY_INFO</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_READY_INFO_REVISION_1</p>
<p>NDIS_WWAN_READY_INFO_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-radio-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_RADIO_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-radio-state)"><strong>NDIS_STATUS_WWAN_RADIO_STATE</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_RADIO_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state)"> <strong>NDIS_WWAN_RADIO_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_RADIO_STATE_REVISION_1</p>
<p>NDIS_WWAN_RADIO_STATE_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-info" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-info)"><strong>NDIS_STATUS_WWAN_PIN_INFO</strong></a></p>
<p>uses <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PIN_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)"><strong>NDIS_WWAN_PIN_INFO</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PIN_INFO_REVISION_1</p>
<p>NDIS_WWAN_PIN_INFO_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-list" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_LIST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-list)"><strong>NDIS_STATUS_WWAN_PIN_LIST</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PIN_LIST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list)"> <strong>NDIS_WWAN_PIN_LIST</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PIN_LIST_REVISION_1</p>
<p>NDIS_WWAN_PIN_LIST_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-service-activation" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SERVICE_ACTIVATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-service-activation)"><strong>NDIS_STATUS_WWAN_SERVICE_ACTIVATION</strong></a>†</p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_service_activation_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SERVICE_ACTIVATION_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_service_activation_status)"> <strong>NDIS_WWAN_SERVICE_ACTIVATION_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SERVICE_ACTIVATION_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SERVICE_ACTIVATION_STATUS_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider" data-raw-source="[&lt;strong&gt;NDIS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider)"> <strong>NDIS_WWAN_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_HOME_PROVIDER_REVISION_1</p>
<p>NDIS_WWAN_HOME_PROVIDER_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-providers)"><strong>NDIS_STATUS_WWAN_PREFERRED_PROVIDERS</strong></a>†</p>
<p>uses <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PREFERRED_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers)"><strong>NDIS_WWAN_PREFERRED_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PREFERRED_PROVIDERS_REVISION_1</p>
<p>NDIS_WWAN_PREFERRED_PROVIDERS_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)"> <strong>NDIS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_VISIBLE_PROVIDERS_REVISION_1</p>
<p>NDIS_WWAN_VISIBLE_PROVIDERS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_REGISTER_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state)"><strong>NDIS_STATUS_WWAN_REGISTER_STATE</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_registration_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_REGISTRATION_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_registration_state)"> <strong>NDIS_WWAN_REGISTRATION_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_REGISTRATION_STATE_REVISION_1</p>
<p>NDIS_WWAN_REGISTRATION_STATE_REVISION_2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-signal-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SIGNAL_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-signal-state)"><strong>NDIS_STATUS_WWAN_SIGNAL_STATE</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SIGNAL_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)"> <strong>NDIS_WWAN_SIGNAL_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SIGNAL_STATE_REVISION_1</p>
<p>NDIS_WWAN_SIGNAL_STATE_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PACKET_SERVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service)"><strong>NDIS_STATUS_WWAN_PACKET_SERVICE</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PACKET_SERVICE_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state)"> <strong>NDIS_WWAN_PACKET_SERVICE_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PACKET_SERVICE_STATE_REVISION_1</p>
<p>NDIS_WWAN_PACKET_SERVICE_STATE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts)"><strong>NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_provisioned_contexts" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PROVISIONED_CONTEXTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_provisioned_contexts)"> <strong>NDIS_WWAN_PROVISIONED_CONTEXTS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PROVISIONED_CONTEXTS_REVISION_1</p>
<p>NDIS_WWAN_PROVISIONED_CONTEXTS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-context-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_CONTEXT_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-context-state)"><strong>NDIS_STATUS_WWAN_CONTEXT_STATE</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_CONTEXT_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state)"> <strong>NDIS_WWAN_CONTEXT_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_CONTEXT_STATE_REVISION_1</p>
<p>NDIS_WWAN_CONTEXT_STATE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-configuration" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_CONFIGURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-configuration)"><strong>NDIS_STATUS_WWAN_SMS_CONFIGURATION</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_configuration" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_CONFIGURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_configuration)"> <strong>NDIS_WWAN_SMS_CONFIGURATION</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_CONFIGURATION_REVISION_1</p>
<p>NDIS_WWAN_SMS_CONFIGURATION_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-receive" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_RECEIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-receive)"><strong>NDIS_STATUS_WWAN_SMS_RECEIVE</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_receive" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_RECEIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_receive)"> <strong>NDIS_WWAN_SMS_RECEIVE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_RECEIVE_REVISION_1</p>
<p>NDIS_WWAN_SMS_RECEIVE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-send" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_SEND&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-send)"><strong>NDIS_STATUS_WWAN_SMS_SEND</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_SEND_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status)"> <strong>NDIS_WWAN_SMS_SEND_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_SEND_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SMS_SEND_STATUS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-delete" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_DELETE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-delete)"><strong>NDIS_STATUS_WWAN_SMS_DELETE</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_DELETE_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete_status)"> <strong>NDIS_WWAN_SMS_DELETE_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_DELETE_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SMS_DELETE_STATUS_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-status" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-status)"><strong>NDIS_STATUS_WWAN_SMS_STATUS</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_status)"> <strong>NDIS_WWAN_SMS_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SMS_STATUS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-vendor-specific" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VENDOR_SPECIFIC&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-vendor-specific)"><strong>NDIS_STATUS_WWAN_VENDOR_SPECIFIC</strong></a>†</p>
<p>ベンダー定義の構造体を使用します。</p></td>
<td align="left"><p>なし</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_USSD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd)"><strong>NDIS_STATUS_WWAN_USSD</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_event" data-raw-source="[&lt;strong&gt;NDIS_WWAN_USSD_EVENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_event)"> <strong>NDIS_WWAN_USSD_EVENT</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_USSD_EVENT_REVISION_1</p>
<p>NDIS_WWAN_USSD_EVENT_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_supported_commands" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_supported_commands)"> <strong>NDIS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICES_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICES_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-response" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-response)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_response" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_RESPONSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_response)"> <strong>NDIS_WWAN_DEVICE_SERVICE_RESPONSE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICE_RESPONSE_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICE_RESPONSE_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-event" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-event)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_event" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_EVENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_event)"> <strong>NDIS_WWAN_DEVICE_SERVICE_EVENT</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICE_EVENT_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICE_EVENT_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_subscription" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_subscription)"> <strong>NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-auth-response" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_AUTH_RESPONSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-auth-response)"><strong>NDIS_STATUS_WWAN_AUTH_RESPONSE</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_response" data-raw-source="[&lt;strong&gt;NDIS_WWAN_AUTH_RESPONSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_response)"> <strong>NDIS_WWAN_AUTH_RESPONSE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_AUTH_RESPONSE_REVISION_1</p>
<p>NDIS_WWAN_AUTH_RESPONSE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-set-home-provider-complete" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-set-home-provider-complete)"><strong>NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE</strong></a></p>
<p>uses <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_home_provider" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SET_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_home_provider)"><strong>NDIS_WWAN_SET_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>なし</p>
<p>NDIS_WWAN_HOME_PROVIDER_REVISION_2</p></td>
</tr>
</tbody>
</table>

> [!NOTE]
> 前の表を次の注意事項が適用されます: † ミニポート ドライバーがサポートできる省略可能なインジケーターを表します。 ミニポート ドライバーでは、省略可能な OID をサポートする場合、ミニポート ドライバーもをサポートするように、対応するを示す値を認識します。 

## <a name="wwan-specific-indication-support-for-gsm-cdma-and-unsolicited-indications"></a>GSM、CDMA、一方的な兆候を WWAN 固有を示す値のサポート

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
<td align="left"><p><strong>要請されていません。</strong></p>
<p><strong>indication</strong></p>
<p><strong>許可しますか。</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps)"><strong>NDIS_STATUS_WWAN_DEVICE_CAPS</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_READY_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info)"><strong>NDIS_STATUS_WWAN_READY_INFO</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-radio-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_RADIO_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-radio-state)"><strong>NDIS_STATUS_WWAN_RADIO_STATE</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-info" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-info)"><strong>NDIS_STATUS_WWAN_PIN_INFO</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-list" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_LIST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-list)"><strong>NDIS_STATUS_WWAN_PIN_LIST</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-service-activation" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SERVICE_ACTIVATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-service-activation)"><strong>NDIS_STATUS_WWAN_SERVICE_ACTIVATION</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-providers)"><strong>NDIS_STATUS_WWAN_PREFERRED_PROVIDERS</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_REGISTER_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state)"><strong>NDIS_STATUS_WWAN_REGISTER_STATE</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-signal-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SIGNAL_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-signal-state)"><strong>NDIS_STATUS_WWAN_SIGNAL_STATE</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PACKET_SERVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service)"><strong>NDIS_STATUS_WWAN_PACKET_SERVICE</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PACKET_SERVICE_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state)"> <strong>NDIS_WWAN_PACKET_SERVICE_STATE</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts)"><strong>NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-context-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_CONTEXT_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-context-state)"><strong>NDIS_STATUS_WWAN_CONTEXT_STATE</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-configuration" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_CONFIGURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-configuration)"><strong>NDIS_STATUS_WWAN_SMS_CONFIGURATION</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-receive" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_RECEIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-receive)"><strong>NDIS_STATUS_WWAN_SMS_RECEIVE</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-send" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_SEND&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-send)"><strong>NDIS_STATUS_WWAN_SMS_SEND</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_SEND_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status)"> <strong>NDIS_WWAN_SMS_SEND_STATUS</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-delete" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_DELETE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-delete)"><strong>NDIS_STATUS_WWAN_SMS_DELETE</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-status" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-status)"><strong>NDIS_STATUS_WWAN_SMS_STATUS</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-vendor-specific" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VENDOR_SPECIFIC&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-vendor-specific)"><strong>NDIS_STATUS_WWAN_VENDOR_SPECIFIC</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_USSD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd)"><strong>NDIS_STATUS_WWAN_USSD</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-response" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-response)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-event" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-event)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-auth-response" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_AUTH_RESPONSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-auth-response)"><strong>NDIS_STATUS_WWAN_AUTH_RESPONSE</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-set-home-provider-complete" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-set-home-provider-complete)"><strong>NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>N</p></td>
</tr>
</tbody>
</table> 

## <a name="multi-carrier-specific-oids"></a>特定の Oid を複数の通信事業者

マルチ キャリア モードをサポートする NDIS 6.30 ミニポート ドライバーに、次の変更が適用されます。 ミニポート ドライバーのマルチ キャリア モードをサポートし、前の表を参照してくださいはしないかどうか。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>OID</strong>と<strong>Windows 8 の対応するデータ構造体</strong></p></td>
<td align="left"><p><strong>クエリ操作</strong></p></td>
<td align="left"><p><strong>設定操作</strong></p></td>
<td align="left"><p><strong>GSM/CDMA</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-home-provider" data-raw-source="[OID_WWAN_HOME_PROVIDER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-home-provider)">OID_WWAN_HOME_PROVIDER</a></p>
<p>uses <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_home_provider" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SET_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_home_provider)"><strong>NDIS_WWAN_SET_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>A</p></td>
<td align="left"><p>A</p></td>
<td align="left"><p>GSM、CDMA</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-preferred-providers" data-raw-source="[OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-preferred-providers)">OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preferred_multicarrier_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SET_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preferred_multicarrier_providers)"> <strong>NDIS_WWAN_SET_PREFERRED_MULTICARRIER_PROVIDERS</strong></a>します。 <strong>PreferredListHeader.ElementType</strong>に設定する必要があります<strong>WwanStructProvider2</strong> WWAN_PROVIDER2 であり、構造体。</p></td>
<td align="left"><p>A</p></td>
<td align="left"><p>A</p></td>
<td align="left"><p>GSM、CDMA</p></td>
</tr>
</tbody>
</table> 

## <a name="multi-carrier-specific-indications-corresponding-data-structures-and-os-revisions"></a>複数の通信事業者の特定がない、対応するデータ構造体、および OS のバージョン

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Indication</strong>と<strong>対応するデータ構造体</strong></p></td>
<td align="left"><p><strong>Windows 8 のリビジョン</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p>
<p>uses <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider2" data-raw-source="[&lt;strong&gt;NDIS_WWAN_HOME_PROVIDER2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider2)"><strong>NDIS_WWAN_HOME_PROVIDER2</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_HOME_PROVIDER_REVISION_2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers)"><strong>NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</strong></a></p>
<p>uses <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers)"><strong>NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS_REVISION_1. <strong>PreferredListHeader.ElementType</strong>に設定する必要があります<strong>WwanStructProvider2</strong>し、一覧は WWAN_PROVIDER2 構造体を含める必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)"> <strong>NDIS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_VISIBLE_PROVIDERS_REVISION_1. <strong>VisibleListHeader.ElementType</strong>に設定する必要があります<strong>WwanStructProvider2</strong>し、一覧は WWAN_PROVIDER2 構造体を含める必要があります。</p></td>
</tr>
</tbody>
</table> 

## <a name="multi-carrier-specific-indication-support-for-gsm-cdma-and-unsolicited-indications"></a>GSM、CDMA、一方的な兆候をマルチ キャリア具体的な表示のサポート

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Indication</strong>と<strong>対応するデータ構造体</strong></p></td>
<td align="left"><p><strong>GSM</strong></p></td>
<td align="left"><p><strong>CDMA</strong></p></td>
<td align="left"><p><strong>要請されていません。</strong></p>
<p><strong>indication</strong></p>
<p><strong>許可しますか。</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers)"><strong>NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p>
<p>使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)"> <strong>NDIS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>N</p></td>
</tr>
</tbody>
</table>
