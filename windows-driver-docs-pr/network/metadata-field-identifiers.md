---
title: メタデータ フィールド識別子
description: このセクションでは、Windows Filtering Platform コールアウト ドライバーのメタデータ フィールドの識別子について説明します。
ms.assetid: 2157bace-9fae-41e8-a435-c4a412873ee1
keywords:
- ネットワーク ドライバーをメタデータ フィールドの識別子
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b7184bf3303cc236f1d78e4cbcc265d51b978a8
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349881"
---
# <a name="metadata-field-identifiers"></a>メタデータ フィールド識別子

メタデータ フィールドの識別子は、各ビット フィールドで表されます。 これらの識別子の定義は次のとおりです。

<table>
<tr>
<th>
メタデータ フィールドの識別子 
      </th>
<th>
説明 
      </th>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_ALE_CLASSIFY_REQUIRED</p>
</td>
<td>
<p>受信パケットが、FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4 と FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6 フィルター レイヤーにも示されます。</p>
<p>
<div class="alert"><b>注</b>  Windows Server 2008、Windows Vista Service Pack 1 (SP1) ではサポートされて以降。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_COMPARTMENT_ID</p>
</td>
<td>
<p>パケットが受信したまたは送信されるルーティングのコンパートメントの識別子。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_COMPLETION_HANDLE</p>
</td>
<td>
<p>完了のハンドルは、保留に、現在のフィルター処理を使用します。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_DESTINATION_INTERFACE_INDEX</p>
</td>
<td>
<p>送信パケットを送信するネットワーク インターフェイスのインデックス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_DESTINATION_PREFIX</p>
</td>
<td>
<p>宛先 IPV4 または IPV6 アドレスとサブネット マスク発信パケットの。</p>
<div class="alert"><b>注</b>  Windows 7 以降ではサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_DISCARD_REASON</p>
</td>
<td>
<p>データが破棄されたことの理由です。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_ETHER_FRAME_LENGTH</p>
</td>
<td>
<p>このメタデータ フィールドの識別子が現在サポートされていません。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_FLOW_HANDLE</p>
</td>
<td>
<p>データ フローのハンドル。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_FORWARD_LAYER_INBOUND_PASS_THRU</p>
</td>
<td>
<p>FWPM_LAYER_IPFORWARD_V4 または FWPM_LAYER_IPFORWARD_V6 前方レイヤーを通過するパケットの送信先がローカル (送信先がホストのインターフェイスに割り当てられているアドレスと一致する)。</p>
<p>
<div class="alert"><b>注</b>  Windows Server 2008、Windows Vista sp1 では、以降でサポートされています。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_FORWARD_LAYER_OUTBOUND_PASS_THRU</p>
</td>
<td>
<p>FWPM_LAYER_IPFORWARD_V4 または FWPM_LAYER_IPFORWARD_V6 を通過するパケットは、ローカルで発生したレイヤーを転送します。</p>
<p>
<div class="alert"><b>注</b>  Windows Server 2008、Windows Vista sp1 では、以降でサポートされています。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_FRAGMENT_DATA</p>
</td>
<td>
<p>受信パケットのフラグメントのフラグメント データ。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_ICMP_ID_AND_SEQUENCE</p>
</td>
<td>
<p>ICMP エコー要求またはエコー応答パケットの識別子とシーケンス番号フィールドです。</p>
<p>
<div class="alert"><b>注</b>  Windows 7 以降ではサポートされています。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_IP_HEADER_SIZE</p>
</td>
<td>
<p>IP ヘッダーのサイズ。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_LOCAL_REDIRECT_TARGET_PID</p>
</td>
<td>
<p>接続がリダイレクトされたプロセス ID。</p>
<p>
<div class="alert"><b>注</b>  Windows 7 以降ではサポートされています。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_ORIGINAL_DESTINATION</p>
</td>
<td>
<p>A <a href="https://msdn.microsoft.com/library/windows/hardware/ff570825"> <b>SOCKADDR_STORAGE</b> </a>パケットの元の送信先を指定する構造体。</p>
<p>
<div class="alert"><b>注</b>  Windows 7 以降ではサポートされています。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_PACKET_DIRECTION</p>
</td>
<td>
<p>(受信または送信) のネットワーク トラフィックの方向です。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_PACKET_SYSTEM_CRITICAL</p>
</td>
<td>
<p>システムの使用に予約されています。 使わないでください。</p>
<p>
<div class="alert"><b>注</b>  Windows Server 2008、Windows Vista sp1 では、以降でサポートされています。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_PARENT_ENDPOINT_HANDLE</p>
</td>
<td>
<p>エンドポイントの親のソケットのハンドル。</p>
<p>
<div class="alert"><b>注</b>  Windows 7 以降ではサポートされています。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_PATH_MTU</p>
</td>
<td>
<p>パケットの送信パス最大転送単位 (MTU のパス)。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_PROCESS_ID</p>
</td>
<td>
<p>エンドポイントを所有するプロセスのプロセス ID。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_PROCESS_PATH</p>
</td>
<td>
<p>エンドポイントを所有するプロセスの完全パスです。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_REDIRECT_RECORD_HANDLE</p>
</td>
<td>
<p>リダイレクト レコードを処理分類メタデータで ALE_CONNECT_REDIRECT コールアウトに示されます。</p>
<p>
<div class="alert"><b>注</b>  Windows 8 以降でサポートされています。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_REMOTE_SCOPE_ID</p>
</td>
<td>
<p>送信トランスポート レイヤーの挿入に使用するリモートのスコープの識別子です。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_RESERVED</p>
</td>
<td>
<p>システムの使用に予約されています。 使わないでください。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_SOURCE_INTERFACE_INDEX</p>
</td>
<td>
<p>着信パケットを受信したネットワーク インターフェイスのインデックス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_SUB_PROCESS_TAG</p>
</td>
<td>
<p>システムの使用に予約されています。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_SYSTEM_FLAGS</p>
</td>
<td>
<p>フィルター エンジンによって内部的に使用されるシステム フラグ。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_TOKEN</p>
</td>
<td>
<p>ユーザーのアクセス許可を検証するために使用するトークンです。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_TRANSPORT_CONTROL_DATA</p>
</td>
<td>
<p>省略可能なソケット コントロールのデータ オブジェクト。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_TRANSPORT_ENDPOINT_HANDLE</p>
</td>
<td>
<p>パケットを送信トランスポート レイヤーに挿入される最後のハンドル。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_TRANSPORT_HEADER_INCLUDE_HEADER</p>
</td>
<td>
<p>Raw ソケットからパケットが送信された場合は、IP ヘッダー。</p>
<p>
<div class="alert"><b>注</b>  Windows Server 2008、Windows Vista sp1 では、以降でサポートされています。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_TRANSPORT_HEADER_SIZE</p>
</td>
<td>
<p>トランスポート ヘッダーのサイズ。</p>
</td>
</tr>
</table>

