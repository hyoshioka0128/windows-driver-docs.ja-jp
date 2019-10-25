---
title: WDI ドキュメントの変更履歴
description: このセクションでは、WDI ドキュメントページのドキュメント変更履歴の一覧を示します。
ms.assetid: 29268059-9C33-4768-8F80-195CB28B4663
ms.date: 02/21/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: e7cd4ccb2cad0d41c2605660d9904ec2b081382e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842931"
---
# <a name="wdi-doc-change-history"></a>WDI ドキュメントの変更履歴

## <a name="windows-10-version-1903"></a>Windows 10 バージョン 1903

ドキュメントは WDI バージョン1.1.8 に更新されました。

| トピック | 説明 |
| --- | --- |
| [WDI_TLV_STATION_CAPABILITIES](wdi-tlv-station-capabilities.md) | 詳細なタイミング測定 (FTM) のサポートを示すドライバーのサポートが追加されました。 |
| [OID_WDI_TASK_REQUEST_FTM](oid-wdi-task-request-ftm.md) | 新しく追加されたタスク OID。これにより、WDI は、アダプターが、ターゲットからのラウンドトリップ時間 (RTT) および場所の構成情報 (LCI) レポートを取得するための FTM プロシージャを開始するように要求できます。 |
| [WDI_TLV_FTM_REQUEST_TIMEOUT](wdi-tlv-ftm-request-timeout.md) | FTM 要求用に新しく追加された TLV。 |
| [WDI_TLV_FTM_TARGET_BSS_ENTRY](wdi-tlv-ftm-target-bss-entry.md) | FTM 要求用に新しく追加された TLV。 |
| [WDI_TLV_REQUEST_LCI_REPORT](wdi-tlv-request-lci-report.md) | FTM 要求用に新しく追加された TLV。 |
| [NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE](ndis-status-wdi-indication-request-ftm-complete.md) | OID_WDI_TASK_REQUEST_FTM のタスクの完了を示す通知としてホストによって送信された、新たに追加されたステータスの表示。 BSS ターゲットからの FTM 応答の一覧が含まれています。 |
| [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md) | FTM 応答用に新しく追加された TLV。 |
| [WDI_TLV_FTM_RESPONSE_STATUS](wdi-tlv-ftm-response-status.md) | FTM 応答用に新しく追加された TLV。 |
| [WDI_TLV_RETRY_AFTER](wdi-tlv-retry-after.md) | FTM 応答用に新しく追加された TLV。 |
| [WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS](wdi-tlv-ftm-number-of-measurements.md) | FTM 応答用に新しく追加された TLV。 |
| [WDI_TLV_RTT](wdi-tlv-rtt.md) | FTM 応答用に新しく追加された TLV。 |
| [WDI_TLV_RTT_ACCURACY](wdi-tlv-rtt-accuracy.md) | FTM 応答用に新しく追加された TLV。 |
| [WDI_TLV_RTT_VARIANCE](wdi-tlv-rtt-variance.md) | FTM 応答用に新しく追加された TLV。 |
| [WDI_TLV_LCI_REPORT_STATUS](wdi-tlv-lci-report-status.md) | FTM 応答用に新しく追加された TLV。 |
| [WDI_TLV_LCI_REPORT_BODY](wdi-tlv-lci-report-body.md) | FTM 応答用に新しく追加された TLV。 |
| [WDI_TLV_INTERFACE_CAPABILITIES](wdi-tlv-interface-capabilities.md) | マルチバンド操作 (MBO) およびビーコンレポートオフロードのサポートを示すためのドライバーの新機能が追加されました。 |
| [**WDI_ASSOC_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_assoc_status) | **WDI_ASSOC_STATUS_ASSOCIATION_DISALLOWED**の状態を追加しました。 |
| [WPA3-SAE 認証](wpa3-sae-authentication.md) | WPA3-SAE (Secure Authentication of Equals) 認証の概要を説明します。 |
| [WDI_TLV_INTERFACE_CAPABILITIES](wdi-tlv-interface-capabilities.md) | SAE 認証のサポートを示すためのドライバーの新機能が追加されました。 |
| [**WDI_AUTH_ALGORITHM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_auth_algorithm) | **WDI_AUTH_ALGO_WPA3_SAE**の定義を追加しました。 |
| [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md) | WDI からの SAE 認証パラメーターを要求するためにドライバーによって送信された、新たに追加されたステータス表示。 |
| [WDI_TLV_SAE_INDICATION_TYPE](wdi-tlv-sae-indication-type.md) | SAE 認証パラメーター要求の TLV が新しく追加されました。 |
| [WDI_TLV_SAE_COMMIT_RESPONSE](wdi-tlv-sae-commit-response.md) | SAE 認証パラメーター要求の TLV が新しく追加されました。 |
| [WDI_TLV_SAE_CONFIRM_RESPONSE](wdi-tlv-sae-confirm-response.md) | SAE 認証パラメーター要求の TLV が新しく追加されました。 |
| [WDI_TLV_SAE_STATUS](wdi-tlv-sae-status.md) | SAE 認証パラメーターの要求および SAE 認証パラメーターの設定用に新しく追加された TLV。 |
| [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md) | 新しく追加されたプロパティ OID。 SAE Commit または Confirm 要求を送信するために必要なパラメーター、または BSSID で SAE を実行できなかったことを示すエラーメッセージが含まれています。 |
| [WDI_TLV_SAE_REQUEST_TYPE](wdi-tlv-sae-request-type.md) | SAE 認証パラメーターを設定するために新しく追加された TLV。 |
| [WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md) | SAE 認証パラメーターを設定するために新しく追加された TLV。 |
| [WDI_TLV_SAE_FINITE_CYCLIC_GROUP](wdi-tlv-sae-finite-cyclic-group.md) | SAE 認証パラメーターを設定するために新しく追加された TLV。 |
| [WDI_TLV_SAE_SCALAR](wdi-tlv-sae-scalar.md) | SAE 認証パラメーターを設定するために新しく追加された TLV。 |
| [WDI_TLV_SAE_ELEMENT](wdi-tlv-sae-element.md) | SAE 認証パラメーターを設定するために新しく追加された TLV。 |
| [WDI_TLV_SAE_ANTI_CLOGGING_TOKEN](wdi-tlv-sae-anti-clogging-token.md) | SAE 認証パラメーターを設定するために新しく追加された TLV。 |
| [WDI_TLV_SAE_CONFIRM_REQUEST](wdi-tlv-sae-confirm-request.md) | SAE 認証パラメーターを設定するために新しく追加された TLV。 |
| [WDI_TLV_SAE_SEND_CONFIRM](wdi-tlv-sae-send-confirm.md) | SAE 認証パラメーターを設定するために新しく追加された TLV。 |
| [WDI_TLV_SAE_CONFIRM](wdi-tlv-sae-confirm.md) | SAE 認証パラメーターを設定するために新しく追加された TLV。 |
| [OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME](oid-wdi-task-p2p-send-request-action-frame.md) | 送信アクションフレームに対する P2P の検証を追加しました。 |
| [OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME](oid-wdi-task-p2p-send-response-action-frame.md) | 送信アクションフレームに対する P2P の検証を追加しました。 || 

## <a name="windows-10-version-1809"></a>Windows 10 Version 1809

ドキュメントは WDI バージョン1.1.7 に更新されました。

| トピック | 説明 |
| --- | --- |
| [**WDI_PHY_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_phy_type) | 802.11 ax PHY のサポートが追加されました。 |
| [**WDI_CONNECTION_QUALITY_HINT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_connection_quality_hint) | **WDI_CONNECTION_QUALITY_HIGH_CHANNEL_AVAILABILITY**値の名前を**WDI_CONNECTION_QUALITY_HIGH_THROUGHPUT**に変更しました。 この値の説明に変更はありません。 |
| [NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT](ndis-status-wdi-indication-device-service-event.md) | 要請されていないデバイスサービス通知のサポートを追加しました。 |

## <a name="windows-10-version-1803"></a>Windows 10 バージョン 1803

ドキュメントは WDI バージョン1.1.6 に更新されました。

| トピック | 説明 |
| --- | --- |
| [**WDI_TLV_OS_POWER_MANAGEMENT_FEATURES**](wdi-tlv-os-power-management-features.md) | この TLV を[OID_WDI_GET_ADAPTER_CAPABILITIES](oid-wdi-get-adapter-capabilities.md)に追加して、ドライバーがサポートしている OS 電源管理 (PM) の機能を示します。 |
| [**WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY**](wdi-tlv-pm-protocol-offload-80211rsn-rekey.md) | この TLV を更新して、 [OID_WDI_GET_PM_PROTOCOL_OFFLOAD](oid-wdi-get-pm-protocol-offload.md)でクエリを実行するときに、ドライバーが GTK/igtk キー情報を返すように指定しました (構成されている場合)。 |
| [NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED](ndis-status-wdi-indication-cipher-key-updated.md) | ドライバーがオフロード状態ではなく、キーが更新されたときに GTK/iGTK キーの更新の通知を提供するために、ドライバーに対してこのような通知を追加しました。 |
| [*MINIPORT_WDI_TX_SUSPECT_FRAME_LIST_ABORT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_suspect_frame_list_abort) | *TxSuspectFrameListAbortHandle*を*TxSuspectFrameListAbort*に更新しました。 |

## <a name="windows-10-version-1709"></a>Windows 10 バージョン 1709

ドキュメントは WDI バージョン1.1.5 に更新されました。

| トピック | 説明 |
| --- | --- |
| [WDI_TLV_TCP_OFFLOAD_CAPABILITIES](wdi-tlv-tcp-offload-capabilities.md) | 指定したオフロードを STA ポートのみに適用するか、すべてのポートに適用するかを示す新しい[**WDI_TLV_OFFLOAD_SCOPE**](wdi-tlv-offload-scope.md)パラメーターを追加しました。 |
| [NDIS_STATUS_WDI_INDICATION_SEND_AP_ASSOCIATION_RESPONSE_COMPLETE](ndis-status-wdi-indication-send-ap-association-response-complete.md) | 必要になるように、 [**WDI\_TLV\_PHY\_TYPE\_LIST**](wdi-tlv-phy-type-list.md)パラメーターを変更しました。 |
| [IHV トレースログを使用したユーザーによるフィードバック](user-initiated-feedback-with-ihv-trace-logging.md) | ユーザーが開始したフィードバックシナリオに IHV ログを追加する方法について説明する新しいセクションが追加されました。 |

## <a name="windows10-version-1607"></a>Windows 10 バージョン1607


ドキュメントは WDI バージョン1.0.21 に更新されました。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-p2p-discover" data-raw-source="[OID_WDI_TASK_P2P_DISCOVER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-p2p-discover)">OID_WDI_TASK_P2P_DISCOVER</a></p></td>
<td align="left"><p>追加された新しいタスクのパラメーター:</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-asp2-service-information-discovery-entry" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-asp2-service-information-discovery-entry)"><strong>WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-include-listen-channel" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-include-listen-channel)"><strong>WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL</strong></a></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities" data-raw-source="[OID_WDI_GET_ADAPTER_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)">OID_WDI_GET_ADAPTER_CAPABILITIES</a></p></td>
<td align="left"><p>新しい get プロパティの結果を追加しました: <a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-supported-guids" data-raw-source="[&lt;strong&gt;WDI_TLV_SUPPORTED_GUIDS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-supported-guids)"> <strong>WDI_TLV_SUPPORTED_GUIDS</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm" data-raw-source="[&lt;strong&gt;WDI_CIPHER_ALGORITHM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm)"><strong>WDI_CIPHER_ALGORITHM</strong></a></p></td>
<td align="left"><p>追加された新しい値: <strong>WDI_CIPHER_ALGO_GCMP</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_phy_type" data-raw-source="[&lt;strong&gt;WDI_PHY_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_phy_type)"><strong>WDI_PHY_TYPE</strong></a></p></td>
<td align="left"><p>追加された新しい値: <strong>WDI_PHY_TYPE_DMG</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_service_discovery_type" data-raw-source="[&lt;strong&gt;WDI_P2P_SERVICE_DISCOVERY_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_service_discovery_type)"><strong>WDI_P2P_SERVICE_DISCOVERY_TYPE</strong></a></p></td>
<td align="left"><p>追加された新しい値:</p>
<ul>
<li><strong>WDI_P2P_SERVICE_DISCOVERY_TYPE_ASP2_SERVICE_NAME_ONLY</strong></li>
<li><strong>WDI_P2P_SERVICE_DISCOVERY_TYPE_ASP2_SERVICE_INFORMATION</strong></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-asp2-advertised-service-entry" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-asp2-advertised-service-entry)"><strong>WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-asp2-service-information-discovery-entry" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-asp2-service-information-discovery-entry)"><strong>WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-include-listen-channel" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-include-listen-channel)"><strong>WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-instance-name" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INSTANCE_NAME&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-instance-name)"><strong>WDI_TLV_P2P_INSTANCE_NAME</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-instance-name-hash" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INSTANCE_NAME_HASH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-instance-name-hash)"><strong>WDI_TLV_P2P_INSTANCE_NAME_HASH</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-service-type" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SERVICE_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-service-type)"><strong>WDI_TLV_P2P_SERVICE_TYPE</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-service-type-hash" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SERVICE_TYPE_HASH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-service-type-hash)"><strong>WDI_TLV_P2P_SERVICE_TYPE_HASH</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-supported-guids" data-raw-source="[&lt;strong&gt;WDI_TLV_SUPPORTED_GUIDS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-supported-guids)"><strong>WDI_TLV_SUPPORTED_GUIDS</strong></a></p></td>
<td align="left"><p>新しく追加された TLVs</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-advertised-services" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ADVERTISED_SERVICES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-advertised-services)"><strong>WDI_TLV_P2P_ADVERTISED_SERVICES</strong></a></p></td>
<td align="left"><p>含まれている TLV を追加しました: <a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-asp2-advertised-service-entry" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-asp2-advertised-service-entry)"> <strong>WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-interface-capabilities" data-raw-source="[&lt;strong&gt;WDI_TLV_INTERFACE_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-interface-capabilities)"><strong>WDI_TLV_INTERFACE_CAPABILITIES</strong></a></p></td>
<td align="left"><p>デバイスが IP ドッキング機能をサポートするかどうかを指定する新しい値が追加されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-capabilities" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-capabilities)"><strong>WDI_TLV_P2P_CAPABILITIES</strong></a></p></td>
<td align="left"><p>ASP2 サービス名の検出がサポートされているかどうかを指定する新しい値が追加されました。</p>
<p>ASP2 Service Information Discovery がサポートされているかどうかを示す新しい値が追加されました。</p></td>
</tr>
</tbody>
</table>

 

## <a name="march-2016"></a>2016 年 3 月


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_target_desc_deinit" data-raw-source="[&lt;em&gt;MINIPORT_WDI_TX_TARGET_DESC_DEINIT&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_target_desc_deinit)"><em>MINIPORT_WDI_TX_TARGET_DESC_DEINIT</em></a></p></td>
<td align="left"><p>この呼び出しのコンテキストで、IHV ミニポートでの表示が許可されていないことに注意してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_target_desc_init" data-raw-source="[&lt;em&gt;MINIPORT_WDI_TX_TARGET_DESC_INIT&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_target_desc_init)"><em>MINIPORT_WDI_TX_TARGET_DESC_INIT</em></a></p></td>
<td align="left"><p>この呼び出しのコンテキストで、IHV ミニポートでの表示が許可されていないことに注意してください。</p></td>
</tr>
</tbody>
</table>

 

## <a name="windows10-version-1511"></a>Windows 10 バージョン1511


ドキュメントは WDI バージョン1.0.10 に更新されました。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-start-ap" data-raw-source="[OID_WDI_TASK_START_AP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-start-ap)">OID_WDI_TASK_START_AP</a></p></td>
<td align="left"><p>新しいタスクパラメーターを追加しました: <a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ap-band-channel" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_BAND_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ap-band-channel)"><strong>WDI_TLV_AP_BAND_CHANNEL</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-adapter-configuration" data-raw-source="[OID_WDI_SET_ADAPTER_CONFIGURATION](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-adapter-configuration)">OID_WDI_SET_ADAPTER_CONFIGURATION</a></p></td>
<td align="left"><p>新しいタスクパラメーターを追加しました: <a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-pldr-support" data-raw-source="[&lt;strong&gt;WDI_TLV_PLDR_SUPPORT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-pldr-support)"><strong>WDI_TLV_PLDR_SUPPORT</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ap-band-channel" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_BAND_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ap-band-channel)"><strong>WDI_TLV_AP_BAND_CHANNEL</strong></a></p></td>
<td align="left"><p>新しく追加された TLV。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-capabilities" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-capabilities)"><strong>WDI_TLV_P2P_CAPABILITIES</strong></a></p></td>
<td align="left"><p>アダプターが5GHz バンドでの操作の実行をサポートするかどうかを指定する新しい値が追加されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-pldr-support" data-raw-source="[&lt;strong&gt;WDI_TLV_PLDR_SUPPORT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-pldr-support)"><strong>WDI_TLV_PLDR_SUPPORT</strong></a></p></td>
<td align="left"><p>新しく追加された TLV。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-start-ap-parameters" data-raw-source="[&lt;strong&gt;WDI_TLV_START_AP_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-start-ap-parameters)"><strong>WDI_TLV_START_AP_PARAMETERS</strong></a></p></td>
<td align="left"><p>レガシ SoftAP クライアントに接続を許可するかどうかを指定する新しい値が追加されました。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-start-ap" data-raw-source="[OID_WDI_TASK_START_AP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-start-ap)">OID_WDI_TASK_START_AP</a> TASK Parameters in <a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ap-band-channel" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_BAND_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ap-band-channel)"><strong>WDI_TLV_AP_BAND_CHANNEL</strong></a>で指定されたチャネルでのみ AP を開始できるかどうかを指定する新しい値を追加しました。</p></td>
</tr>
</tbody>
</table>

 

## <a name="windows10"></a>Windows 10


初期バージョン。

 

 





