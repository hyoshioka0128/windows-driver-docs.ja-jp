---
title: ISCSI\_状態\_修飾子
description: ISCSI\_状態\_修飾子
ms.assetid: d39ed448-5608-4f19-b49c-bbd6727e9491
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f7d2827962ccf4ddbeb55e7c8afd78975d3591aa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378396"
---
# <a name="iscsistatusqualifiers"></a>ISCSI\_状態\_修飾子


## <span id="ddk_iscsi_status_qualifiers_kr"></span><span id="DDK_ISCSI_STATUS_QUALIFIERS_KR"></span>


ISCSI\_状態\_修飾子 WMI プロパティ修飾子は、iSCSI HBA イニシエーターを管理するミニポート ドライバーによって報告される状態値に対応します。 これらの値は、機能のコードと記載されている機能の状態コードとの重要度コードを組み合わせることによって構築されている*Ntstatus.h*します。

次の表に、ISCSI\_状態\_修飾子の値。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>成功しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_NON_SPECIFIC_ERROR (0xEFFF0001)</p></td>
<td align="left"><p>不特定のエラーです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_LOGIN_FAILED (0xEFFF0002)</p></td>
<td align="left"><p>ログオンに失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_CONNECTION_FAILED (0xEFFF0003)</p></td>
<td align="left"><p>接続に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INITIATOR_NODE_ALREADY_EXISTS (0xEFFF0004)</p></td>
<td align="left"><p>発信側ノードは既に存在します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INITIATOR_NODE_NOT_FOUND (0xEFFF0005)</p></td>
<td align="left"><p>発信側ノードが存在しません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_MOVED_TEMPORARILY (0xEFFF0006)</p></td>
<td align="left"><p>ターゲットが一時的に移動します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_TARGET_MOVED_PERMANENTLY (0xEFFF0007)</p></td>
<td align="left"><p>ターゲットは、完全に移動します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INITIATOR_ERROR (0xEFFF0008)</p></td>
<td align="left"><p>発信側エラーです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_AUTHENTICATION_FAILURE (0xEFFF0009)</p></td>
<td align="left"><p>認証に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_AUTHORIZATION_FAILURE (0xEFFF000A)</p></td>
<td align="left"><p>承認に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_NOT_FOUND (0xEFFF000B)</p></td>
<td align="left"><p>ターゲットが見つかりませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_REMOVED (0xEFFF000C)</p></td>
<td align="left"><p>ターゲットは削除されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_UNSUPPORTED_VERSION (0xEFFF000D)</p></td>
<td align="left"><p>サポートされていないバージョンです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TOO_MANY_CONNECTIONS (0xEFFF000E)</p></td>
<td align="left"><p>接続が多すぎます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_MISSING_PARAMETER (0xEFFF000F)</p></td>
<td align="left"><p>パラメーターがありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_CANT_INCLUDE_IN_SESSION (0xEFFF0010)</p></td>
<td align="left"><p>セッションの接続を含めることはできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_SESSION_TYPE_NOT_SUPPORTED (0xEFFF0011)</p></td>
<td align="left"><p>セッションの種類がサポートされていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_ERROR (0xEFFF0012)</p></td>
<td align="left"><p>ターゲット エラーです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_SERVICE_UNAVAILABLE (0XEFFF0013)</p></td>
<td align="left"><p>サービスは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_OUT_OF_RESOURCES (0xEFFF0014)</p></td>
<td align="left"><p>リソースが足りません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_CONNECTION_ALREADY_EXISTS (0xEFFF0015)</p></td>
<td align="left"><p>接続は、イニシエーターのノードに既に存在します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_SESSION_ALREADY_EXISTS (0xEFFF0016)</p></td>
<td align="left"><p>セッションは既に存在します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INITIATOR_INSTANCE_NOT_FOUND (0xEFFF0017)</p></td>
<td align="left"><p>発信側インスタンスが存在しません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_ALREADY_EXISTS (0xEFFF0018)</p></td>
<td align="left"><p>ターゲットは既に存在します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_DRIVER_BUG (0XEFFF0019)</p></td>
<td align="left"><p>ISCSI のドライバーの実装は、操作を正しく完了しませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INVALID_TEXT_KEY (0xEFFF001A)</p></td>
<td align="left"><p>無効なキーのテキストが発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_SENDTARGETS_TEXT (0xEFFF001B)</p></td>
<td align="left"><p>無効な endTargets の応答テキストが発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INVALID_SESSION_ID (0xEFFF001C)</p></td>
<td align="left"><p>無効なセッションの識別子 (ID) です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_SCSI_REQUEST_FAILED (0xEFFF001D)</p></td>
<td align="left"><p>SCSI 要求が失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TOO_MANY_SESSIONS (0xEFFF001E)</p></td>
<td align="left"><p>このイニシエーターに対する最大セッション数を超えています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_SESSION_BUSY (0XEFFF001F)</p></td>
<td align="left"><p>要求が既に進行中のため、セッションがビジーです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_MAPPING_UNAVAILABLE (0xEFFF0020)</p></td>
<td align="left"><p>ターゲットのマッピングは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_ADDRESS_TYPE_NOT_SUPPORTED (0xEFFF0021)</p></td>
<td align="left"><p>ターゲット アドレスの種類がサポートされていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_LOGON_FAILED (0xEFFF0022)</p></td>
<td align="left"><p>ログオンに失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_SEND_FAILED (0xEFFF0023)</p></td>
<td align="left"><p>TCP 送信に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TRANSPORT_ERROR (0xEFFF0024)</p></td>
<td align="left"><p>TCP トランスポートのエラーです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_VERSION_MISMATCH (0xEFFF0025)</p></td>
<td align="left"><p>iSCSI のバージョンが一致しません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_MAPPING_OUT_OF_RANGE (0xEFFF0026)</p></td>
<td align="left"><p>渡されるターゲット マッピングのアドレスは、アダプターの構成の範囲外です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_TARGET_PRESHAREDKEY_UNAVAILABLE (0xEFFF0027)</p></td>
<td align="left"><p>ターゲットまたはインターネット キー交換 (IKE) id ペイロードの事前共有キーは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_AUTHINFO_UNAVAILABLE (0xEFFF0028)</p></td>
<td align="left"><p>ターゲットの認証情報は、ご利用いただけません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_TARGET_NOT_FOUND (0XEFFF0029)</p></td>
<td align="left"><p>ターゲット名が見つからないか、マークがログオンから非表示になります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_LOGIN_USER_INFO_BAD (0xEFFF002A)</p></td>
<td align="left"><p>1 つまたは複数のパラメーターで指定されている、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_logintotarget_in" data-raw-source="[&lt;strong&gt;LoginToTarget_IN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_logintotarget_in)"> <strong>LoginToTarget_IN</strong> </a>構造が無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_TARGET_MAPPING_EXISTS (0xEFFF002B)</p></td>
<td align="left"><p>特定のターゲット マッピングが既に存在します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_HBA_SECURITY_CACHE_FULL (0xEFFF002C)</p></td>
<td align="left"><p>HBA のセキュリティ情報のキャッシュがいっぱいです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_PORT_NUMBER (0xEFFF002D)</p></td>
<td align="left"><p>イニシエーターに渡されるポート番号が正しくありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_OPERATION_NOT_ALL_SUCCESS (0xEFFF002E)</p></td>
<td align="left"><p>操作は、すべてのイニシエーター用に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_HBA_SECURITY_CACHE_NOT_SUPPORTED (0xEFFF002F)</p></td>
<td align="left"><p>アダプターのセキュリティ情報のキャッシュではありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_IKE_ID_PAYLOAD_TYPE_NOT_SUPPORTED (0xEFFF0030)</p></td>
<td align="left"><p>指定されている IKE ID ペイロードの種類がサポートされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_IKE_ID_PAYLOAD_INCORRECT_SIZE (0xEFFF0031)</p></td>
<td align="left"><p>指定されている IKE ID ペイロードのサイズが正しくありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_PORTAL_ALREADY_EXISTS (0xEFFF0032)</p></td>
<td align="left"><p>ターゲット ポータルの構造が既に存在します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_TARGET_ADDRESS_ALREADY_EXISTS (0xEFFF0033)</p></td>
<td align="left"><p>ターゲット アドレスの構造が既に存在します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_NO_AUTH_INFO_AVAILABLE (0xEFFF0034)</p></td>
<td align="left"><p>IKE 認証情報はありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_NO_TUNNEL_OUTER_MODE_ADDRESS (0xEFFF0035)</p></td>
<td align="left"><p>トンネル モードの外部アドレスが指定されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_CACHE_CORRUPTED (0xEFFF0036)</p></td>
<td align="left"><p>認証またはトンネル アドレスのキャッシュが破損しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_REQUEST_NOT_SUPPORTED (0xEFFF0037)</p></td>
<td align="left"><p>要求または操作がサポートされていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_OUT_OF_RESORCES (0xEFFF0038)</p></td>
<td align="left"><p>ターゲットには、指定された要求を処理するのに十分なリソースはありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_SERVICE_DID_NOT_RESPOND (0xEFFF0039)</p></td>
<td align="left"><p>発信側サービスは、ドライバーの送信要求に応答しませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_ISNS_SERVER_NOT_FOUND (0xEFFF003A)</p></td>
<td align="left"><p>ISNS サーバーが見つからなかったか、ご利用いただけません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_OPERATION_REQUIRES_REBOOT (0xAFFF003B)</p></td>
<td align="left"><p>操作は成功しましたが、ドライバーの再読み込みまたは有効にするために再起動が必要です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_NO_PORTAL_SPECIFIED (0xEFFF003C)</p></td>
<td align="left"><p>ターゲット ポータルのログオンを完了することはありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_CANT_REMOVE_LAST_CONNECTION (0xEFFF003D)</p></td>
<td align="left"><p>セッションの最後の接続を削除できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_SERVICE_NOT_RUNNING (0XEFFF003E)</p></td>
<td align="left"><p>ISCSI イニシエーター サービスが開始されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_TARGET_ALREADY_LOGGED_IN (0xEFFF003F)</p></td>
<td align="left"><p>ターゲットは iSCSI セッション経由既に記録されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_DEVICE_BUSY_ON_SESSION (0xEFFF0040)</p></td>
<td align="left"><p>セッションは、そのセッション上のデバイスは現在使用されているため、ログオフされることはできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_COULD_NOT_SAVE_PERSISTENT_LOGIN_DATA (0xEFFF0041)</p></td>
<td align="left"><p>永続的なログオン情報を保存できませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_COULD_NOT_REMOVE_PERSISTENT_LOGIN_DATA (0xEFFF0042)</p></td>
<td align="left"><p>永続的なログオン情報を削除できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_PORTAL_NOT_FOUND (0xEFFF0043)</p></td>
<td align="left"><p>指定されたイニシエーターの名前が見つかりませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INITIATOR_NOT_FOUND (0xEFFF0044)</p></td>
<td align="left"><p>指定したポータルは見つかりませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_DISCOVERY_MECHANISM_NOT_FOUND (0xEFFF0045)</p></td>
<td align="left"><p>指定した探索メカニズムは見つかりませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_IPSEC_NOT_SUPPORTED_ON_OS (0xEFFF0046)</p></td>
<td align="left"><p>iSCSI は、このバージョンのオペレーティング システムの IPsec プロトコルをサポートしていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_PERSISTENT_LOGIN_TIMEOUT (0xEFFF0047)</p></td>
<td align="left"><p>探索サービスは、すべての永続的なログオンを完了するを待機中にタイムアウトになりました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_SHORT_CHAP_SECRET (0xEFFF0048)</p></td>
<td align="left"><p>指定された CHAP シークレットは 96 ビットより小さいと、非 IPsec 接続経由で認証ネゴシエーションを使用することはできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_EVALUATION_PEROID_EXPIRED (0xEFFF0049)</p></td>
<td align="left"><p>ISCSI の探索サービスの評価期間が終了しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INVALID_CHAP_SECRET (0xEFFF004A)</p></td>
<td align="left"><p>CHAP シークレットは、、チャレンジ ハンドシェイク認証プロトコル (CHAP) ネットワーク Working Group Internet Engineering Task Force (IETF) の発行する仕様に準拠していません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_TARGET_CHAP_SECRET (0xEFFF004B)</p></td>
<td align="left"><p>ターゲット CHAP シークレットが無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INVALID_INITIATOR_CHAP_SECRET (0xEFFF004C)</p></td>
<td align="left"><p>イニシエーター CHAP シークレットが無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_CHAP_USER_NAME (0xEFFF004D)</p></td>
<td align="left"><p>CHAP のユーザー名が無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INVALID_LOGON_AUTH_TYPE (0xEFFF004E)</p></td>
<td align="left"><p>ログオン認証の種類が無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_TARGET_MAPPING (0xEFFF004F)</p></td>
<td align="left"><p>ターゲットのマッピング情報が無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INVALID_TARGET_ID (0xEFFF0050)</p></td>
<td align="left"><p>ターゲットのマッピングで 64 ビットの iSCSI ターゲット識別子が無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_ISCSI_NAME (0xEFFF0051)</p></td>
<td align="left"><p>指定されている iSCSI 名は無効な文字が含まれています。 またはが長すぎます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INCOMPATIBLE_ISNS_VERSION (0xEFFF0052)</p></td>
<td align="left"><p>ISNS サーバーから返された iSNS のバージョン番号は、iSNS クライアントには、このバージョンと互換性がありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_FAILED_TO_CONFIGURE_IPSEC (0xEFFF0053)</p></td>
<td align="left"><p>イニシエーターは、指定された接続の IPSec を構成できませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_BUFFER_TOO_SMALL (0xEFFF0054)</p></td>
<td align="left"><p>処理の指定されたバッファーが小さすぎます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_LOAD_BALANCE_POLICY (0xEFFF0055)</p></td>
<td align="left"><p>指定された負荷分散ポリシーが無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INVALID_PARAMETER (0xEFFF0056)</p></td>
<td align="left"><p>指定された 1 つまたは複数のパラメーターが無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_DUPLICATE_PATH_SPECIFIED (0xEFFF0057)</p></td>
<td align="left"><p>パスの冗長パスの間で負荷分散ポリシーを設定しようとしているときに指定された Id が重複しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_PATH_COUNT_MISMATCH (0xEFFF0058)</p></td>
<td align="left"><p>負荷分散ポリシーの設定で指定されたパスの数が、ターゲットから利用可能なパスの数と一致しません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_PATH_ID (0xEFFF0059)</p></td>
<td align="left"><p>負荷分散ポリシーの設定で指定されたパス ID が無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_MULTIPLE_PRIMARY_PATHS_SPECIFIED (0XEFFF005A)</p></td>
<td align="left"><p>1 つ以上のプライマリ パスは、1 つだけのプライマリ パスが予想される場合に指定されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_NO_PRIMARY_PATH_SPECIFIED (0xEFFF005B)</p></td>
<td align="left"><p>プライマリ パスが指定されて、少なくとも 1 つは発生しません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_DEVICE_ALREADY_PERSISTENTLY_BOUND (0xEFFF005C)</p></td>
<td align="left"><p>デバイスは、既に永続的にバインドされているデバイスです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_DEVICE_NOT_FOUND (0XEFFF005D)</p></td>
<td align="left"><p>デバイスが見つかりませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_DEVICE_NOT_ISCSI_OR_PERSISTENT (0xEFFF005E)</p></td>
<td align="left"><p>指定されたデバイスは、iSCSI ディスクまたは永続的な iSCSI ログインから取得していません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_DNS_NAME_UNRESOLVED (0xEFFF005F)</p></td>
<td align="left"><p>指定した DNS 名は解決されませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_NO_CONNECTION_AVAILABLE (0XEFFF0060)</p></td>
<td align="left"><p>要求を処理する iSCSI セッションで使用できる接続がありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_LB_POLICY_NOT_SUPPORTED (0xEFFF0061)</p></td>
<td align="left"><p>特定の負荷分散ポリシーがサポートされていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_REMOVE_CONNECTION_IN_PROGRESS (0xEFFF0062)</p></td>
<td align="left"><p>接続の削除要求が既に進行中のこのセッションです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_CONNECTION_ID (0xEFFF0063)</p></td>
<td align="left"><p>指定した接続が見つかりません、セッションでします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_CANNOT_REMOVE_LEADING_CONNECTION (0xEFFF0064)</p></td>
<td align="left"><p>セッション内の先頭の接続を削除できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_RESTRICTED_BY_GROUP_POLICY (0xEFFF0065)</p></td>
<td align="left"><p>このコンピューターに割り当てられているグループ ポリシーに準拠していないために、操作を実行できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_ISNS_FIREWALL_BLOCKED (0xEFFF0066)</p></td>
<td align="left"><p>インターネット ストレージ ネーム サーバー (iSNS) ファイアウォールの例外が有効になっていないために、操作を実行できません。</p></td>
</tr>
</tbody>
</table>

 

 

 





