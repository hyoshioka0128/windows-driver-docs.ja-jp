---
title: OID_WWAN_CONNECT
description: OID_WWAN_CONNECT は、アクティブにまたは特定のパケットのコンテキストを非アクティブ化し、コンテキストのアクティブ化の状態を読み取ります。
ms.assetid: 51be35fe-750b-4c2b-aab3-a9df59711f7d
ms.date: 08/08/2017
keywords: -OID_WWAN_CONNECT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a7f93008a12b7cee62c899d109e38d45e1e16adb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362859"
---
# <a name="oidwwanconnect"></a>OID\_WWAN\_接続


OID\_WWAN\_接続がアクティブにまたは特定のパケットのコンテキストを非アクティブ化し、コンテキストのアクティブ化の状態を読み取ります。

ミニポート ドライバー セットを処理する必要があり、クエリ要求が最初に、非同期に返す NDIS\_状態\_を示す値\_元の要求とそれ以降の送信に必要な[ **NDIS\_ステータス\_WWAN\_コンテキスト\_状態**](ndis-status-wwan-context-state.md)状態通知を含む、 [ **NDIS\_WWAN\_コンテキスト\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state)セットまたはクエリの要求の完了に関係なく MB デバイスのパケット データ プロトコル (PDP) コンテキストの状態を示す構造体。

MB デバイスのパケット データ プロトコル (PDP) コンテキストの状態を設定するように要求して呼び出し元に提供する[ **NDIS\_WWAN\_設定\_コンテキスト\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_context_state)適切な情報、ミニポート ドライバー構造体。

<a name="remarks"></a>注釈
-------

詳細については、この OID を使用して、次を参照してください。 [WWAN パケット コンテキスト管理](https://docs.microsoft.com/windows-hardware/drivers/network/mb-packet-context-management)します。

このオブジェクトをアクティブにまたは特定のパケットのコンテキストを非アクティブ化し、コンテキストのアクティブ化の状態を読み取ります。 ミニポート ドライバーは、アクティブ化の状態が変更されるたびに、適切なイベント通知を送信する必要があります。

このオブジェクトは、ミニポート ドライバーが、登録状態の場合にのみ呼び出されます。 **WwanRegisterStateHome**、 **WwanRegisterStatePartner**、または**WwanRegisterStateRoaming**します。 パケット サービスがアクティブの場合、デバイスのアタッチ状態である必要があります**WwanPacketServiceStateAttached**します。

両方の設定し、このオブジェクトのクエリ操作がサポートされています。

-   セットの要求の処理には、SIM アクセスは含まれませんが、ネットワーク アクセスが必要です。

-   クエリ要求の処理では、ネットワークまたは SIM へのアクセスは必要ありません。

この OID のデータ構造は、NDIS\_WWAN\_設定\_コンテキスト\_状態。 NDIS の状態表示の問題、ミニポート ドライバー\_状態\_WWAN\_コンテキスト\_セットとクエリの両方の要求の状態。

ドライバー モデルのこのバージョンでは、MB、サービスから指示された場合にのみ、ミニポート ドライバーがコンテキストのアクティブ化を試行します。 (ミニポート ドライバーは、以降のバージョンでネットワークによって開始されたコンテキストをアクティブ可能性があります)ミニポート ドライバーでは、コンテキストは自動的には登録または信号を失った後もアクティブする必要があります。 ライセンス認証要求でアクセス文字列を指定しない場合、ミニポート ドライバーしようとしないでください、既定の文字列を提供します。 代わりに、空の文字列を使用して、コンテキストをアクティブ化することを続行する必要があります。

その一方で、ミニポート ドライバーは非アクティブ化コンテキストの指示に従って MB サービス。 これは、ネットワーク接続が失われた場合のシグナル、または正常なシャット ダウンまたは状態のクリーンアップの一部として、一時的な損失のしきい値を超える期間に発生する可能性があります。

1 つのみのコンテキストでアクティブ化されるためは、このバージョンは、アクティブ化するかを設定するか、レイヤー 2 MB の接続解除を行う特定のコンテキストの金額を非アクティブ化でサポートされます。

セットの要求で MB サービスを提供両方**ConnectionId**と**ActivationCommand**パラメーターで、WWAN\_コンテキスト\_状態データ構造体。 識別されるパケットのコンテキストをアクティブ化またはミニポート ドライバーに指示が**ConnectionId**を基に、 **ActivationCommand**パラメーター値*WwanActivationCommandActivate*または*WwanActivationCommandDeactivate*します。

-   サービスまたはサブスクリプションのライセンス認証を必要とする場合、ミニポート ドライバーがエラー コード WWAN を返す必要があります\_状態\_サービス\_いない\_アクティブ化します。 PDP-アクティブ化になるまで、サービスまたはサブスクリプションがアクティブにします。 緊急のすべてのサービス、デバイスと、演算子からサポートされる使用可能な場合があります。 オペレーティング システムが、OID を呼び出すことができます\_WWAN\_サービス\_このエラー コードへの応答でのアクティブ化します。

-   エラー コード WWAN 返しますミニポート ドライバーがパケットの別のコンテキストが現在アクティブなときにコンテキストのアクティブ化要求を受け取る場合\_状態\_最大\_ACTIVATED\_コンテキスト。

-   ミニポート ドライバーで識別されるコンテキストがコンテキストの非アクティブ化要求を受け取った場合**ConnectionId**がアクティブ化されていない、エラー コード WWAN を返します\_状態\_コンテキスト\_されません\_アクティブ化します。

ミニポート ドライバーでは、次のロジックを使って、セットの要求から AccessString、UserName、およびパスワードの設定の有効性を決定します。

-   場合**ActivationCommand**は*WwanActivationCommandDeactivate*、ミニポート ドライバーがこれら 3 つのパラメーターの設定を無視する必要があります。 ケースの残りの部分のみ場合を考えますとき**ActivationCommand**は*WwanActivationCommandActivate*します。

コンテキストのアクティブ化は、ユーザー ログオンおよびログオフの間で永続化します。 各ユーザーのログオンはありません。

クエリの要求で MB サービスは、このオブジェクトを使用してアクティブ化の状態を確認します。

クエリ要求に応答して、ミニポート ドライバーを送信、NDIS\_状態\_WWAN\_コンテキスト\_状態通知します。

**重要な**  に注意してください。

 

まれですが、特定の状況では、Windows 7 MB サービス可能性がありますしようとすると、インターネットに接続または瞬間的な中断中に既存の接続用の既存のインターネット接続で判断された前に自動接続接続の数。 これは、結果、MB、WLAN/イーサネットの同時接続。 たとえば、これが発生するシステム ブート時に MB、その他の接続を同時に実行し、ネットワーク リスト マネージャー サービスは引き続きアクティブとパッシブのメソッドを使用して他の接続のインターネット接続を確認しようとしています。 これは、可能性があります、企業プロキシ サーバーなど、ISP ネットワークのネットワーク インフラストラクチャで一時的な停止のためにも発生します。 したがって、MB サービスは、「別のインターネット接続がない場合にのみ自動接続は使用」オプションが選択されているかどうかに関係なく、インターネットに自動接続試行可能性があります。

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
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[WWAN パケット コンテキスト管理](https://docs.microsoft.com/windows-hardware/drivers/network/mb-packet-context-management)

 

 




