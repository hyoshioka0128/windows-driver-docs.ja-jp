---
title: WPA3 SAE 認証
description: このトピックで説明をバージョン 1.1.8 WDI WPA3 SAE 認証およびそれ以降。
ms.assetid: BE6EF8E4-F4EB-4D39-AC33-B67F8935DCBC
ms.date: 02/21/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 90ead0fe0ef244a3ee0f5a5e3439ba0f6ae530e0
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905430"
---
# <a name="wpa3-sae-authentication"></a>WPA3 SAE 認証

WPA3 SAE とも呼ばれますの WPA3 個人は、WDI バージョン 1.1.8 と Windows でサポートされている以降です。 フレームのコンテンツの生成と SAE (セキュリティで保護された認証の値) の認証用の解析で、Windows 内で行われますが、OS WPA3 SAE 認証フレームを送受信するためのドライバーのサポートが必要です。

## <a name="wpa3-sae-capabilities"></a>WPA3 SAE 機能

ミニポート ドライバーでは、次の手順に従って、SAE サポートを指定します。

1. サポートされている SAE 機能を設定します。  
    ドライバーのセット、 **SAEAuthenticationSupported**機能[WDI_TLV_INTERFACE_ATTRIBUTES](wdi-tlv-interface-attributes.md)呼び出し中に[OID_WDI_GET_ADAPTER_CAPABILITIES](oid-wdi-get-adapter-capabilities.md)します。
2. MFP 機能を設定します。  
    ドライバーのセット、 **MFPCapable**機能[WDI_TLV_STATION_ATTRIBUTES](wdi-tlv-station-attributes.md)呼び出し中に[OID_WDI_GET_ADAPTER_CAPABILITIES](oid-wdi-get-adapter-capabilities.md)します。
3. 追加、 **WDI_AUTH_ALGO_WPA3_SAE**認証方法。  
    ドライバーが含まれています**WDI_AUTH_ALGO_WPA3_SAE**への呼び出しで返される認証暗号の組み合わせの一覧で[OID_WDI_GET_ADAPTER_CAPABILITIES](oid-wdi-get-adapter-capabilities.md)します。 これは、次のセクションで追加する必要があります。
    - [WDI_TLV_STATION_ATTRIBUTES](wdi-tlv-station-attributes.md) :。[WDI_TLV_UNICAST_ALGORITHM_LIST](wdi-tlv-unicast-algorithm-list.md)
    - [WDI_TLV_STATION_ATTRIBUTES](wdi-tlv-station-attributes.md) :。[WDI_TLV_MULTICAST_DATA_ALGORITHM_LIST](wdi-tlv-multicast-data-algorithm-list.md)

## <a name="wpa3-sae-authentication-flow"></a>WPA3 SAE 認証フロー

### <a name="connection-initiation"></a>接続を開始できません。

開始 SAE 接続[OID_WDI_TASK_CONNECT](oid-wdi-task-connect.md)または[OID_WDI_TASK_ROAM](oid-wdi-task-roam.md)します。 WDI 指定**WDI_AUTH_ALGO_WPA3_SAE** SAE 認証を行うドライバーが必要な場合に、認証方法として。 WDI は、接続/移動タスクで BSS リスト PMKID を提供する場合、ドライバーが SAE 認証をスキップし、Open Authentication を代わりに、実行後に、PMKID 要求を再関連付けします。

### <a name="authentication-flow"></a>認証フロー

![認証フローの WPA3 SAE](images/wpa3-sae-authentication-flow.png "WPA3 SAE 認証フロー")

#### <a name="initial-request-for-sae-parameters"></a>SAE パラメーターの最初の要求

ドライバーは、最初にすると、接続またはローミング BSS を選択や、WDI にからの要求コミット パラメーターをドライバー WDI をその BSS、PMKID 指定されませんだった場合、 [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)します。 この最初の表示で、ドライバーを示す値の型を設定**WDI_SAE_INDICATION_TYPE_COMMIT_REQUEST_PARAMS_NEEDED**します。 WDI は送信応答、 [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)次のオプションのいずれかのドライバーにします。

- コミット要求の送信 (**WDI_SAE_REQUEST_TYPE_COMMIT_REQUEST**)
- SAE 認証に失敗 (**WDI_SAE_REQUEST_TYPE_FAILURE**)

#### <a name="upon-receiving-a-commit-response"></a>コミットの応答の受信時に

コミットの応答を受信するには、ドライバーの送信[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)種類に設定された**WDI_SAE_INDICATION_TYPE_COMMIT_RESPONSE**します。 WDI は送信応答、 [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)次の要求のいずれかの。

- コミット要求の送信 (**WDI_SAE_REQUEST_TYPE_COMMIT_REQUEST**)
- 確認要求を送信 (**WDI_SAE_REQUEST_TYPE_CONFIRM_REQUEST**)
- SAE 認証に失敗 (**WDI_SAE_REQUEST_TYPE_FAILURE**)

#### <a name="upon-receiving-a-confirm-response"></a>確認応答の受信時に

ドライバーの送信、確認応答を受け取る[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)種類に設定された**WDI_SAE_INDICATION_TYPE_CONFIRM_RESPONSE**します。 WDI 送信[OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md) SAE 状態 フィールドでは成功または失敗に設定します。 ドライバーの送信タイムアウトまたはその他の理由により、ドライバーで SAE 認証に失敗した場合、 [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)を示す値を型 se **WDI_SAE_INDICATION_TYPE_ERROR**で指定したエラーの理由と[WDI_TLV_SAE_STATUS](wdi-tlv-sae-status.md)します。

### <a name="timeouts-and-retransmissions"></a>タイムアウトと再伝送

これらは、ドライバーによって処理されます。

## <a name="wpa3-sae-association"></a>WPA3 SAE の関連付け

デバイスは、次のオプションのいずれかを使用して、SAE ネットワークに接続します。

### <a name="reassociation-following-sae-exchange"></a>(Re)次の SAE exchange の関連付け

これは、通常、SAE ネットワークに最初の関連付けの試行です。 ドライバーは、アソシエーション要求フレームに RSN IE で SAE AKM を設定します。

### <a name="reassociation-using-pmkid"></a>(Re)PMKID を使用してアソシエーション

WDI は、ドライバーは、次のタスクでは、接続/ローミング、BSS エントリ、PMKID を指定: 場合

1. ドライバーでは、オープン認証 (Re) 関連の要求で PMKID を含めることによって後に実行します。
2. デバイスは、短期間で AP からの応答を受信しなかった場合、または AP が応答でアソシエーション エラーを返す場合、ドライバーは、この AP と SE 認証をスキップします。 を実行し、別の AP に移動しますかこの AP との完全な SAE 認証を行うにはフォールバックを実行します。

SAE 認証/関連付けが完了したら、SAE 接続が完了します。 前に、としてに、ドライバーは、ローミング データに接続またはタスクの最後に使用して次の問題を送信します。

- [NDIS_STATUS_WDI_INDICATION_ASSOCIATION_RESULT](ndis-status-wdi-indication-association-result.md)
- [NDIS_STATUS_WDI_INDICATION_CONNECT_COMPLETE](ndis-status-wdi-indication-connect-complete.md)

## <a name="error-handling"></a>エラー処理

### <a name="resending-the-sae-commit-request-frame"></a>SAE コミット要求フレームに再送信

をドライバーが、タイムアウトによってコミット フレームを再送信する必要がある場合に、WDI によって提供されていた元のスカラーまたは要素値を再送信するかで WDI から新しい一連のスカラーまたは要素の値を要求する[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)を示す値。

### <a name="resending-the-sae-confirm-response-frame"></a>SAE 確認応答フレームを再送信

新しいセットを要求する必要があります、ドライバーは、タイムアウトによって確認フレームを再送信する必要がある場合、 **SendConfirm**と**確認**で WDI から値を[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)の種類に設定を示す値**WDI_SAE_INDICATION_TYPE_CONFIRM_REQUEST_RESEND_REQUEST**します。
