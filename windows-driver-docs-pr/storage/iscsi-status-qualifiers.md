---
title: ISCSI\_の状態\_修飾子
description: ISCSI\_の状態\_修飾子
ms.assetid: d39ed448-5608-4f19-b49c-bbd6727e9491
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b9e05c4c2ff19408b2eb12060fcb0d69621312a6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823681"
---
# <a name="iscsi_status_qualifiers"></a>ISCSI\_の状態\_修飾子


## <span id="ddk_iscsi_status_qualifiers_kr"></span><span id="DDK_ISCSI_STATUS_QUALIFIERS_KR"></span>


ISCSI\_STATUS\_qualifier WMI プロパティ修飾子は、iSCSI HBA イニシエーターを管理するミニポートドライバーによって報告される状態値に対応します。 これらの値は、重大度コードと、「 *Ntstatus*」で説明されているファシリティの状態コードを組み合わせることによって作成されます。

次の表では、ISCSI\_の状態\_修飾子の値について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態の値</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>ブランド.</p></td>
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
<td align="left"><p>イニシエーターノードは既に存在します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INITIATOR_NODE_NOT_FOUND (0xEFFF0005)</p></td>
<td align="left"><p>イニシエーターノードが存在しません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_MOVED_TEMPORARILY (0xEFFF0006)</p></td>
<td align="left"><p>ターゲットが一時的に移動されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_TARGET_MOVED_PERMANENTLY (0xEFFF0007)</p></td>
<td align="left"><p>ターゲットが完全に移動されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INITIATOR_ERROR (0xEFFF0008)</p></td>
<td align="left"><p>イニシエーターエラー。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_AUTHENTICATION_FAILURE (0xEFFF0009)</p></td>
<td align="left"><p>認証エラーです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_AUTHORIZATION_FAILURE (0xEFFF000A)</p></td>
<td align="left"><p>承認エラーです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_NOT_FOUND (0xEFFF000B)</p></td>
<td align="left"><p>ターゲットが見つかりません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_REMOVED (0xEFFF000C)</p></td>
<td align="left"><p>ターゲットが削除されます。</p></td>
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
<td align="left"><p>セッションに接続を含めることはできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_SESSION_TYPE_NOT_SUPPORTED (0xEFFF0011)</p></td>
<td align="left"><p>セッションの種類がサポートされていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_ERROR (0xEFFF0012)</p></td>
<td align="left"><p>ターゲットエラーです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_SERVICE_UNAVAILABLE (0xEFFF0013)</p></td>
<td align="left"><p>サービスを利用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_OUT_OF_RESOURCES (0xEFFF0014)</p></td>
<td align="left"><p>リソースが不足しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_CONNECTION_ALREADY_EXISTS (0xEFFF0015)</p></td>
<td align="left"><p>接続は既にイニシエーターノードに存在します。</p></td>
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
<td align="left"><p>ISDSC_DRIVER_BUG (0xEFFF0019)</p></td>
<td align="left"><p>ISCSI ドライバーの実装は、操作を正しく完了しませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INVALID_TEXT_KEY (0xEFFF001A)</p></td>
<td align="left"><p>無効なキーテキストが見つかりました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_SENDTARGETS_TEXT (0xEFFF001B)</p></td>
<td align="left"><p>無効な endTargets 応答テキストが見つかりました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INVALID_SESSION_ID (0xEFFF001C)</p></td>
<td align="left"><p>無効なセッション識別子 (ID) です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_SCSI_REQUEST_FAILED (0xEFFF001D)</p></td>
<td align="left"><p>SCSI 要求が失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TOO_MANY_SESSIONS (0xEFFF001E)</p></td>
<td align="left"><p>このイニシエーターの最大セッション数を超えました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_SESSION_BUSY (0xEFFF001F)</p></td>
<td align="left"><p>要求が既に進行中のため、セッションがビジー状態です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_MAPPING_UNAVAILABLE (0xEFFF0020)</p></td>
<td align="left"><p>ターゲットマッピングは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_ADDRESS_TYPE_NOT_SUPPORTED (0xEFFF0021)</p></td>
<td align="left"><p>ターゲットアドレスの種類がサポートされていません。</p></td>
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
<td align="left"><p>TCP トランスポートエラーです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_VERSION_MISMATCH (0xEFFF0025)</p></td>
<td align="left"><p>iSCSI バージョンが一致しません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_MAPPING_OUT_OF_RANGE (0xEFFF0026)</p></td>
<td align="left"><p>渡されたターゲットマッピングアドレスがアダプター構成の範囲外です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_TARGET_PRESHAREDKEY_UNAVAILABLE (0xEFFF0027)</p></td>
<td align="left"><p>ターゲットまたはインターネットキー交換 (IKE) の識別ペイロードの事前共有キーを使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_AUTHINFO_UNAVAILABLE (0xEFFF0028)</p></td>
<td align="left"><p>ターゲットの認証情報は使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_TARGET_NOT_FOUND (0xEFFF0029)</p></td>
<td align="left"><p>ターゲット名が見つからないか、ログオンから非表示に設定されています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_LOGIN_USER_INFO_BAD (0xEFFF002A)</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_logintotarget_in" data-raw-source="[&lt;strong&gt;LoginToTarget_IN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_logintotarget_in)"><strong>LoginToTarget_IN</strong></a>構造体で指定された1つ以上のパラメーターが無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_TARGET_MAPPING_EXISTS (0xEFFF002B)</p></td>
<td align="left"><p>指定されたターゲットマッピングは既に存在します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_HBA_SECURITY_CACHE_FULL (0xEFFF002C)</p></td>
<td align="left"><p>HBA セキュリティ情報のキャッシュがいっぱいです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_PORT_NUMBER (0xEFFF002D)</p></td>
<td align="left"><p>渡されたポート番号がイニシエーターに対して無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_OPERATION_NOT_ALL_SUCCESS (0xEFFF002E)</p></td>
<td align="left"><p>すべてのイニシエーターに対して操作が成功しませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_HBA_SECURITY_CACHE_NOT_SUPPORTED (0xEFFF002F)</p></td>
<td align="left"><p>アダプターにセキュリティ情報キャッシュがありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_IKE_ID_PAYLOAD_TYPE_NOT_SUPPORTED (0xEFFF0030)</p></td>
<td align="left"><p>指定された IKE ID ペイロードの種類はサポートされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_IKE_ID_PAYLOAD_INCORRECT_SIZE (0xEFFF0031)</p></td>
<td align="left"><p>指定された IKE ID ペイロードのサイズが正しくありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_PORTAL_ALREADY_EXISTS (0xEFFF0032)</p></td>
<td align="left"><p>ターゲットポータル構造は既に存在します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_TARGET_ADDRESS_ALREADY_EXISTS (0xEFFF0033)</p></td>
<td align="left"><p>ターゲットアドレスの構造は既に存在します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_NO_AUTH_INFO_AVAILABLE (0xEFFF0034)</p></td>
<td align="left"><p>使用できる IKE 認証情報がありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_NO_TUNNEL_OUTER_MODE_ADDRESS (0xEFFF0035)</p></td>
<td align="left"><p>トンネルモードの外部アドレスが指定されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_CACHE_CORRUPTED (0xEFFF0036)</p></td>
<td align="left"><p>認証またはトンネルアドレスのキャッシュが破損しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_REQUEST_NOT_SUPPORTED (0xEFFF0037)</p></td>
<td align="left"><p>要求または操作はサポートされていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_OUT_OF_RESORCES (0xEFFF0038)</p></td>
<td align="left"><p>ターゲットには、指定された要求を処理するのに十分なリソースがありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_SERVICE_DID_NOT_RESPOND (0xEFFF0039)</p></td>
<td align="left"><p>発信側サービスが、ドライバーによって送信された要求に応答しませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_ISNS_SERVER_NOT_FOUND (0xEFFF003A)</p></td>
<td align="left"><p>ISNS サーバーが見つからないか、使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_OPERATION_REQUIRES_REBOOT (0Xfmri F003b)</p></td>
<td align="left"><p>操作は成功しましたが、有効になるにはドライバーの再読み込みまたは再起動が必要です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_NO_PORTAL_SPECIFIED (0xEFFF003C)</p></td>
<td align="left"><p>ログオンを完了するために使用できるターゲットポータルがありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_CANT_REMOVE_LAST_CONNECTION (0xEFFF003D)</p></td>
<td align="left"><p>セッションの最後の接続を削除できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_SERVICE_NOT_RUNNING (0xEFFF003E)</p></td>
<td align="left"><p>ISCSI イニシエーターサービスが開始されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_TARGET_ALREADY_LOGGED_IN (0xEFFF003F)</p></td>
<td align="left"><p>ターゲットは、iSCSI セッションを通じて既にログオンしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_DEVICE_BUSY_ON_SESSION (0xEFFF0040)</p></td>
<td align="left"><p>セッションのデバイスが現在使用されているため、セッションをログオフできません。</p></td>
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
<td align="left"><p>指定されたイニシエーター名が見つかりませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INITIATOR_NOT_FOUND (0xEFFF0044)</p></td>
<td align="left"><p>指定されたポータルが見つかりませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_DISCOVERY_MECHANISM_NOT_FOUND (0xEFFF0045)</p></td>
<td align="left"><p>指定された検出メカニズムが見つかりませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_IPSEC_NOT_SUPPORTED_ON_OS (0xEFFF0046)</p></td>
<td align="left"><p>iSCSI は、このバージョンのオペレーティングシステムの IPsec プロトコルをサポートしていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_PERSISTENT_LOGIN_TIMEOUT (0xEFFF0047)</p></td>
<td align="left"><p>すべての永続的なログオンが完了するのを待機しているときに、探索サービスがタイムアウトしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_SHORT_CHAP_SECRET (0xEFFF0048)</p></td>
<td align="left"><p>指定された CHAP シークレットは96ビット未満であり、非 IPsec 接続での認証ネゴシエーションには使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_EVALUATION_PEROID_EXPIRED (0xEFFF0049)</p></td>
<td align="left"><p>ISCSI discovery サービスの評価期間が終了しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INVALID_CHAP_SECRET (0xEFFF004A)</p></td>
<td align="left"><p>CHAP シークレットは、インターネット技術標準化委員会 (IETF) のネットワーク作業グループが公開するチャレンジハンドシェイク認証プロトコル (CHAP) の仕様に準拠していません。</p></td>
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
<td align="left"><p>CHAP ユーザー名が無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INVALID_LOGON_AUTH_TYPE (0xEFFF004E)</p></td>
<td align="left"><p>ログオン認証の種類が無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_TARGET_MAPPING (0xEFFF004F)</p></td>
<td align="left"><p>ターゲットマッピング情報が無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INVALID_TARGET_ID (0xEFFF0050)</p></td>
<td align="left"><p>ターゲットマッピングの64ビット iSCSI ターゲット id が無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_ISCSI_NAME (0xEFFF0051)</p></td>
<td align="left"><p>指定された iSCSI 名に無効な文字が含まれているか、または長すぎます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INCOMPATIBLE_ISNS_VERSION (0xEFFF0052)</p></td>
<td align="left"><p>Isns サーバーから返された isns バージョン番号は、このバージョンの iSNS クライアントと互換性がありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_FAILED_TO_CONFIGURE_IPSEC (0xEFFF0053)</p></td>
<td align="left"><p>イニシエーターは、指定された接続に対して IPSec を構成できませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_BUFFER_TOO_SMALL (0xEFFF0054)</p></td>
<td align="left"><p>処理用に指定されたバッファーが小さすぎます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_LOAD_BALANCE_POLICY (0xEFFF0055)</p></td>
<td align="left"><p>指定された負荷分散ポリシーが無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INVALID_PARAMETER (0xEFFF0056)</p></td>
<td align="left"><p>指定された1つ以上のパラメーターが無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_DUPLICATE_PATH_SPECIFIED (0xEFFF0057)</p></td>
<td align="left"><p>重複するパスに対して負荷分散ポリシーを設定しようとしているときに、重複したパス Id が指定されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_PATH_COUNT_MISMATCH (0xEFFF0058)</p></td>
<td align="left"><p>負荷分散ポリシーの設定で指定されたパスの数が、ターゲットから利用できるパスの数と一致しません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_PATH_ID (0xEFFF0059)</p></td>
<td align="left"><p>負荷分散ポリシーの設定で指定されたパス ID が無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_MULTIPLE_PRIMARY_PATHS_SPECIFIED (0xEFFF005A)</p></td>
<td align="left"><p>1つのプライマリパスのみが必要な場合は、複数のプライマリパスを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_NO_PRIMARY_PATH_SPECIFIED (0xEFFF005B)</p></td>
<td align="left"><p>少なくとも1つのが必要なときに、プライマリパスを指定することはできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_DEVICE_ALREADY_PERSISTENTLY_BOUND (0xEFFF005C)</p></td>
<td align="left"><p>デバイスは、既に永続的にバインドされているデバイスです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_DEVICE_NOT_FOUND (0xEFFF005D)</p></td>
<td align="left"><p>デバイスが見つかりませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_DEVICE_NOT_ISCSI_OR_PERSISTENT (0xEFFF005E)</p></td>
<td align="left"><p>指定されたデバイスは、iSCSI ディスクまたは永続的な iSCSI ログインからのものではありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_DNS_NAME_UNRESOLVED (0xEFFF005F)</p></td>
<td align="left"><p>指定された DNS 名は解決されませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_NO_CONNECTION_AVAILABLE (0xEFFF0060)</p></td>
<td align="left"><p>ISCSI セッションで要求を処理するために使用できる接続がありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_LB_POLICY_NOT_SUPPORTED (0xEFFF0061)</p></td>
<td align="left"><p>指定された負荷分散ポリシーはサポートされていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_REMOVE_CONNECTION_IN_PROGRESS (0xEFFF0062)</p></td>
<td align="left"><p>このセッションでは、接続の削除要求が既に進行中です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_CONNECTION_ID (0xEFFF0063)</p></td>
<td align="left"><p>指定された接続がセッションで見つかりませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_CANNOT_REMOVE_LEADING_CONNECTION (0xEFFF0064)</p></td>
<td align="left"><p>セッションの先頭の接続を削除できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_RESTRICTED_BY_GROUP_POLICY (0xEFFF0065)</p></td>
<td align="left"><p>このコンピューターに割り当てられているグループポリシーに準拠していないため、操作を実行できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_ISNS_FIREWALL_BLOCKED (0xEFFF0066)</p></td>
<td align="left"><p>インターネット記憶域ネームサーバー (iSNS) のファイアウォールの例外が有効になっていないため、操作を実行できません。</p></td>
</tr>
</tbody>
</table>

 

 

 





