---
title: WDI ドキュメントの変更履歴
description: このセクションでは、WDI ドキュメント ページのドキュメントの変更履歴を示します
ms.assetid: 29268059-9C33-4768-8F80-195CB28B4663
ms.date: 02/21/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 39293fe0e3930651b08c2296a530f11a4cd6a3f3
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903316"
---
# <a name="wdi-doc-change-history"></a>WDI ドキュメントの変更履歴

## <a name="windows-10-version-1903"></a>Windows 10、バージョンが 1903

ドキュメントをバージョン 1.1.8 WDI に更新します。

| トピック | 説明 |
| --- | --- |
| [WDI_TLV_STATION_CAPABILITIES](wdi-tlv-station-capabilities.md) | サポート問題タイミング測定 (FTM) を示すため、ドライバーのサポートが追加されました。 |
| [OID_WDI_TASK_REQUEST_FTM](oid-wdi-task-request-ftm.md) | 新しく追加されたタスクを要求できる WDI BSS ターゲットからのラウンド トリップ時間 (RTT) と場所の構成情報 (LCI) レポートを取得するアダプター開始 FTM プロシージャをできるようにする OID。 |
| [WDI_TLV_FTM_REQUEST_TIMEOUT](wdi-tlv-ftm-request-timeout.md) | FTM 要求の TLV が新しく追加します。 |
| [WDI_TLV_FTM_TARGET_BSS_ENTRY](wdi-tlv-ftm-target-bss-entry.md) | FTM 要求の TLV が新しく追加します。 |
| [WDI_TLV_REQUEST_LCI_REPORT](wdi-tlv-request-lci-report.md) | FTM 要求の TLV が新しく追加します。 |
| [NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE](ndis-status-wdi-indication-request-ftm-complete.md) | 新しく追加されたホストによって、タスクの完了を示す値として送信され OID_WDI_TASK_REQUEST_FTM の状態を示す値。 BSS ターゲットから FTM 応答の一覧が含まれています。 |
| [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md) | FTM 応答の TLV が新しく追加します。 |
| [WDI_TLV_FTM_RESPONSE_STATUS](wdi-tlv-ftm-response-status.md) | FTM 応答の TLV が新しく追加します。 |
| [WDI_TLV_RETRY_AFTER](wdi-tlv-retry-after.md) | FTM 応答の TLV が新しく追加します。 |
| [WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS](wdi-tlv-ftm-number-of-measurements.md) | FTM 応答の TLV が新しく追加します。 |
| [WDI_TLV_RTT](wdi-tlv-rtt.md) | FTM 応答の TLV が新しく追加します。 |
| [WDI_TLV_RTT_ACCURACY](wdi-tlv-rtt-accuracy.md) | FTM 応答の TLV が新しく追加します。 |
| [WDI_TLV_RTT_VARIANCE](wdi-tlv-rtt-variance.md) | FTM 応答の TLV が新しく追加します。 |
| [WDI_TLV_LCI_REPORT_STATUS](wdi-tlv-lci-report-status.md) | FTM 応答の TLV が新しく追加します。 |
| [WDI_TLV_LCI_REPORT_BODY](wdi-tlv-lci-report-body.md) | FTM 応答の TLV が新しく追加します。 |
| [WDI_TLV_INTERFACE_CAPABILITIES](wdi-tlv-interface-capabilities.md) | Multiband 操作 (MBO) とビーコン レポート オフロードのサポートを示すため、ドライバーの新機能を追加します。 |
| [**WDI_ASSOC_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_assoc_status) | 追加**WDI_ASSOC_STATUS_ASSOCIATION_DISALLOWED**状態。 |
| [WPA3 SAE 認証](wpa3-sae-authentication.md) | WPA3 SAE (セキュリティで保護された認証の値) の認証の新しい概要です。 |
| [WDI_TLV_INTERFACE_CAPABILITIES](wdi-tlv-interface-capabilities.md) | SAE 認証のサポートを示すため、ドライバーの新しい機能を追加します。 |
| [**WDI_AUTH_ALGORITHM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_auth_algorithm) | 定義を追加**WDI_AUTH_ALGO_WPA3_SAE**します。 |
| [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md) | 新しく追加されたドライバーによって、WDI からの要求 SAE 認証パラメーターに送信される状態を示す値。 |
| [WDI_TLV_SAE_INDICATION_TYPE](wdi-tlv-sae-indication-type.md) | SAE 認証パラメーターの要求の TLV が新しく追加します。 |
| [WDI_TLV_SAE_COMMIT_RESPONSE](wdi-tlv-sae-commit-response.md) | SAE 認証パラメーターの要求の TLV が新しく追加します。 |
| [WDI_TLV_SAE_CONFIRM_RESPONSE](wdi-tlv-sae-confirm-response.md) | SAE 認証パラメーターの要求の TLV が新しく追加します。 |
| [WDI_TLV_SAE_STATUS](wdi-tlv-sae-status.md) | TLV は、SAE 認証パラメーターの要求と SAE 認証パラメーターを設定するために新しく追加されました。 |
| [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md) | 新しく追加されたプロパティ、SAE コミットまたは確認要求または SAE、BSSID での実行の失敗を示すエラー メッセージを送信するために必要なパラメーターを格納する OID。 |
| [WDI_TLV_SAE_REQUEST_TYPE](wdi-tlv-sae-request-type.md) | SAE 認証パラメーターの設定の TLV が新しく追加します。 |
| [WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md) | SAE 認証パラメーターの設定の TLV が新しく追加します。 |
| [WDI_TLV_SAE_FINITE_CYCLIC_GROUP](wdi-tlv-sae-finite-cyclic-group.md) | SAE 認証パラメーターの設定の TLV が新しく追加します。 |
| [WDI_TLV_SAE_SCALAR](wdi-tlv-sae-scalar.md) | SAE 認証パラメーターの設定の TLV が新しく追加します。 |
| [WDI_TLV_SAE_ELEMENT](wdi-tlv-sae-element.md) | SAE 認証パラメーターの設定の TLV が新しく追加します。 |
| [WDI_TLV_SAE_ANTI_CLOGGING_TOKEN](wdi-tlv-sae-anti-clogging-token.md) | SAE 認証パラメーターの設定の TLV が新しく追加します。 |
| [WDI_TLV_SAE_CONFIRM_REQUEST](wdi-tlv-sae-confirm-request.md) | SAE 認証パラメーターの設定の TLV が新しく追加します。 |
| [WDI_TLV_SAE_SEND_CONFIRM](wdi-tlv-sae-send-confirm.md) | SAE 認証パラメーターの設定の TLV が新しく追加します。 |
| [WDI_TLV_SAE_CONFIRM](wdi-tlv-sae-confirm.md) | SAE 認証パラメーターの設定の TLV が新しく追加します。 |
| [OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME](oid-wdi-task-p2p-send-request-action-frame.md) | 追加された追加の検証 P2P IEs の送信アクションのフレームにします。 |
| [OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME](oid-wdi-task-p2p-send-response-action-frame.md) | 追加された追加の検証 P2P IEs の送信アクションのフレームにします。 || 

## <a name="windows-10-version-1809"></a>Windows 10 Version 1809

ドキュメントが WDI バージョン 1.1.7 に更新します。

| トピック | 説明 |
| --- | --- |
| [**WDI_PHY_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_phy_type) | 802.11ax サポートが追加されました PHY します。 |
| [**WDI_CONNECTION_QUALITY_HINT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_connection_quality_hint) | 名前を変更、 **WDI_CONNECTION_QUALITY_HIGH_CHANNEL_AVAILABILITY**値を**WDI_CONNECTION_QUALITY_HIGH_THROUGHPUT**します。 この値の説明を変更はありません。 |
| [NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT](ndis-status-wdi-indication-device-service-event.md) | 要請されていないデバイスのサービス通知のサポートが追加されました。 |

## <a name="windows-10-version-1803"></a>Windows 10 バージョン 1803

ドキュメントが WDI 1.1.6 のバージョンに更新します。

| トピック | 説明 |
| --- | --- |
| [**WDI_TLV_OS_POWER_MANAGEMENT_FEATURES**](wdi-tlv-os-power-management-features.md) | 追加するには、この TLV [OID_WDI_GET_ADAPTER_CAPABILITIES](oid-wdi-get-adapter-capabilities.md)に OS の電源管理 (PM) 機能、ドライバーがサポートするかを示します。 |
| [**WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY**](wdi-tlv-pm-protocol-offload-80211rsn-rekey.md) | 更新のエントリの構成でクエリを実行している場合、ドライバーする必要があります GTK/iGTK キーの情報が返すようになりましたを指定するには、この TLV [OID_WDI_GET_PM_PROTOCOL_OFFLOAD](oid-wdi-get-pm-protocol-offload.md)します。 |
| [NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED](ndis-status-wdi-indication-cipher-key-updated.md) | このキーが更新されるは、ドライバーはオフロード状態ではありません、GTK/iGTK の重要な更新の通知を提供するドライバーを示す値を追加します。 |
| [*MINIPORT_WDI_TX_SUSPECT_FRAME_LIST_ABORT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_tx_suspect_frame_list_abort) | 更新*TxSuspectFrameListAbortHandle*に*TxSuspectFrameListAbort*します。 |

## <a name="windows-10-version-1709"></a>Windows 10 バージョン 1709

ドキュメントが WDI バージョン 1.1.5 に更新します。

| トピック | 説明 |
| --- | --- |
| [WDI_TLV_TCP_OFFLOAD_CAPABILITIES](wdi-tlv-tcp-offload-capabilities.md) | 新規追加[ **WDI_TLV_OFFLOAD_SCOPE** ](wdi-tlv-offload-scope.md)またはすべてのポートにのみ STA ポートに指定したオフロードが適用されるかどうかを示します。 |
| [NDIS_STATUS_WDI_INDICATION_SEND_AP_ASSOCIATION_RESPONSE_COMPLETE](ndis-status-wdi-indication-send-ap-association-response-complete.md) | 変更、 [ **WDI\_TLV\_PHY\_型\_一覧**](wdi-tlv-phy-type-list.md)パラメーターが必須にします。 |
| [IHV のトレース ログ記録でフィードバックをユーザーが開始しました。](user-initiated-feedback-with-ihv-trace-logging.md) | IHV がフィードバックをユーザーが開始したシナリオへのログ記録を追加する方法を説明する新しいセクションが追加されました。 |

## <a name="windows10-version-1607"></a>Windows 10 バージョン 1607


ドキュメント バージョン 1.0.21 WDI に更新します。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn925955" data-raw-source="[OID_WDI_TASK_P2P_DISCOVER](https://msdn.microsoft.com/library/windows/hardware/dn925955)">OID_WDI_TASK_P2P_DISCOVER</a></p></td>
<td align="left"><p>新しいタスク パラメーターを追加しました。</p>
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/mt769912" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769912)"><strong>WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/mt769913" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769913)"><strong>WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL</strong></a></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn925838" data-raw-source="[OID_WDI_GET_ADAPTER_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/dn925838)">OID_WDI_GET_ADAPTER_CAPABILITIES</a></p></td>
<td align="left"><p>追加された新しい get プロパティ結果:<a href="https://msdn.microsoft.com/library/windows/hardware/mt769918" data-raw-source="[&lt;strong&gt;WDI_TLV_SUPPORTED_GUIDS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769918)"><strong>WDI_TLV_SUPPORTED_GUIDS</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn897802" data-raw-source="[&lt;strong&gt;WDI_CIPHER_ALGORITHM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897802)"><strong>WDI_CIPHER_ALGORITHM</strong></a></p></td>
<td align="left"><p>追加された新しい値。<strong>WDI_CIPHER_ALGO_GCMP</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn926105" data-raw-source="[&lt;strong&gt;WDI_PHY_TYPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926105)"><strong>WDI_PHY_TYPE</strong></a></p></td>
<td align="left"><p>追加された新しい値。<strong>WDI_PHY_TYPE_DMG</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn926101" data-raw-source="[&lt;strong&gt;WDI_P2P_SERVICE_DISCOVERY_TYPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926101)"><strong>WDI_P2P_SERVICE_DISCOVERY_TYPE</strong></a></p></td>
<td align="left"><p>追加された新しい値:</p>
<ul>
<li><strong>WDI_P2P_SERVICE_DISCOVERY_TYPE_ASP2_SERVICE_NAME_ONLY</strong></li>
<li><strong>WDI_P2P_SERVICE_DISCOVERY_TYPE_ASP2_SERVICE_INFORMATION</strong></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt769911" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769911)"><strong>WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt769912" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769912)"><strong>WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt769913" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769913)"><strong>WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt769914" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INSTANCE_NAME&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769914)"><strong>WDI_TLV_P2P_INSTANCE_NAME</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt769915" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INSTANCE_NAME_HASH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769915)"><strong>WDI_TLV_P2P_INSTANCE_NAME_HASH</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt769916" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SERVICE_TYPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769916)"><strong>WDI_TLV_P2P_SERVICE_TYPE</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt769917" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SERVICE_TYPE_HASH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769917)"><strong>WDI_TLV_P2P_SERVICE_TYPE_HASH</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt769918" data-raw-source="[&lt;strong&gt;WDI_TLV_SUPPORTED_GUIDS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769918)"><strong>WDI_TLV_SUPPORTED_GUIDS</strong></a></p></td>
<td align="left"><p>新しく追加された TLVs します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn897860" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ADVERTISED_SERVICES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897860)"><strong>WDI_TLV_P2P_ADVERTISED_SERVICES</strong></a></p></td>
<td align="left"><p>追加の包含 TLV:<a href="https://msdn.microsoft.com/library/windows/hardware/mt769911" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769911)"><strong>WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn897836" data-raw-source="[&lt;strong&gt;WDI_TLV_INTERFACE_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897836)"><strong>WDI_TLV_INTERFACE_CAPABILITIES</strong></a></p></td>
<td align="left"><p>デバイスが IP のドッキング機能をサポートするかどうかを指定する新しい値を追加します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn897865" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897865)"><strong>WDI_TLV_P2P_CAPABILITIES</strong></a></p></td>
<td align="left"><p>ASP2 サービス名の検索がサポートされているかどうかを指定する新しい値を追加します。</p>
<p>ASP2 サービス情報の検出がサポートされているかどうかを指定する新しい値を追加します。</p></td>
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt297593" data-raw-source="[&lt;em&gt;MINIPORT_WDI_TX_TARGET_DESC_DEINIT&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/mt297593)"><em>MINIPORT_WDI_TX_TARGET_DESC_DEINIT</em></a></p></td>
<td align="left"><p>この呼び出しのコンテキストでは何を行うには、IHV ミニポートは許可されていないメモを追加します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt297594" data-raw-source="[&lt;em&gt;MINIPORT_WDI_TX_TARGET_DESC_INIT&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/mt297594)"><em>MINIPORT_WDI_TX_TARGET_DESC_INIT</em></a></p></td>
<td align="left"><p>この呼び出しのコンテキストでは何を行うには、IHV ミニポートは許可されていないメモを追加します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="windows10-version-1511"></a>Windows 10 バージョン 1511


ドキュメントをバージョン 1.0.10 WDI に更新します。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn925964" data-raw-source="[OID_WDI_TASK_START_AP](https://msdn.microsoft.com/library/windows/hardware/dn925964)">OID_WDI_TASK_START_AP</a></p></td>
<td align="left"><p>新しいタスクのパラメーターを追加するには。<a href="https://msdn.microsoft.com/library/windows/hardware/mt593242" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_BAND_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt593242)"><strong>WDI_TLV_AP_BAND_CHANNEL</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn925853" data-raw-source="[OID_WDI_SET_ADAPTER_CONFIGURATION](https://msdn.microsoft.com/library/windows/hardware/dn925853)">OID_WDI_SET_ADAPTER_CONFIGURATION</a></p></td>
<td align="left"><p>新しいタスクのパラメーターを追加するには。<a href="https://msdn.microsoft.com/library/windows/hardware/mt593243" data-raw-source="[&lt;strong&gt;WDI_TLV_PLDR_SUPPORT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt593243)"><strong>WDI_TLV_PLDR_SUPPORT</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt593242" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_BAND_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt593242)"><strong>WDI_TLV_AP_BAND_CHANNEL</strong></a></p></td>
<td align="left"><p>新しく追加された TLV します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn897865" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897865)"><strong>WDI_TLV_P2P_CAPABILITIES</strong></a></p></td>
<td align="left"><p>アダプターが 5 GHz 帯域の移動の操作をサポートするかどうかを指定する新しい値を追加します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt593243" data-raw-source="[&lt;strong&gt;WDI_TLV_PLDR_SUPPORT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt593243)"><strong>WDI_TLV_PLDR_SUPPORT</strong></a></p></td>
<td align="left"><p>新しく追加された TLV します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn898065" data-raw-source="[&lt;strong&gt;WDI_TLV_START_AP_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898065)"><strong>WDI_TLV_START_AP_PARAMETERS</strong></a></p></td>
<td align="left"><p>従来の SoftAP クライアントが接続できるようにするかどうかを指定する新しい値を追加します。</p>
<p>AP がで指定されたチャネルでのみ開始するかどうかを指定する新しい値を追加<a href="https://msdn.microsoft.com/library/windows/hardware/dn925964" data-raw-source="[OID_WDI_TASK_START_AP](https://msdn.microsoft.com/library/windows/hardware/dn925964)">OID_WDI_TASK_START_AP</a>を持つパラメーターをタスク<a href="https://msdn.microsoft.com/library/windows/hardware/mt593242" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_BAND_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt593242)"> <strong>WDI_TLV_AP_BAND_CHANNEL</strong> </a>.</p></td>
</tr>
</tbody>
</table>

 

## <a name="windows10"></a>Windows 10


最初のバージョン。

 

 





