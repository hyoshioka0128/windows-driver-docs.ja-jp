---
title: OID_WWAN_CONNECT
description: OID_WWAN_CONNECT は、特定のパケットコンテキストをアクティブ化または非アクティブ化し、コンテキストのアクティベーション状態を読み取ります。
ms.assetid: 51be35fe-750b-4c2b-aab3-a9df59711f7d
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_WWAN_CONNECT
ms.localizationpriority: medium
ms.openlocfilehash: c00e90cf4058f577f9e47a8cd9cd3e53fe94c0db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843869"
---
# <a name="oid_wwan_connect"></a>OID\_WWAN\_接続


OID\_WWAN\_接続は、特定のパケットコンテキストをアクティブ化または非アクティブ化し、コンテキストのアクティベーション状態を読み取ります。

ミニポートドライバーは、セットおよびクエリ要求を非同期的に処理し、最初に NDIS\_の\_状態を返し、元の要求に対して必要な\_を通知し、その後、 [**ndis\_ステータス\_WWAN\_コンテキストを送信する必要があります。** ](ndis-status-wwan-context-state.md)set 要求またはクエリ要求の完了に関係なく、MB デバイスのパケットデータプロトコル (PDP) コンテキストの状態を示す[**NDIS\_WWAN\_コンテキスト\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state)構造を含む\_状態状態通知。

MB デバイスのパケットデータプロトコル (PDP) コンテキストの状態を設定するように要求している呼び出し元は、 [**NDIS\_WWAN\_\_コンテキスト\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_context_state)構造をミニポートドライバーに設定し、適切な情報を提供します。

<a name="remarks"></a>注釈
-------

この OID の使用方法の詳細については、「 [WWAN パケットコンテキスト管理](https://docs.microsoft.com/windows-hardware/drivers/network/mb-packet-context-management)」を参照してください。

このオブジェクトは、特定のパケットコンテキストをアクティブ化または非アクティブ化し、コンテキストのアクティベーション状態を読み取ります。 ミニポートドライバーは、アクティベーション状態が変化するたびに適切なイベント通知を送信する必要があります。

このオブジェクトは、ミニポートドライバーが**Wwanregisterstatehome**、 **wwanregisterstatehome**、または**WwanRegisterStateRoaming**の登録状態である場合にのみ呼び出されます。 パケットサービスがアクティブになっている場合、デバイスは、 **Wwanpacketservicestateattached**のアタッチ状態でもある必要があります。

このオブジェクトでは、set 操作と query 操作の両方がサポートされています。

-   Set 要求の処理にはネットワークアクセスが必要ですが、SIM アクセスは必要ありません。

-   クエリ要求の処理では、ネットワークまたは SIM へのアクセスは必要ありません。

この OID のデータ構造は NDIS\_WWAN\_\_コンテキスト\_状態に設定されます。 ミニポートドライバーは、set 要求とクエリ要求の両方について、NDIS\_ステータス\_WWAN\_コンテキスト\_状態の状態を示します。

このバージョンのドライバーモデルでは、ミニポートドライバーは、MB サービスで指示されたとおりにコンテキストのアクティブ化を試行します。 (ミニポートドライバーは、以降のバージョンでネットワークによって開始されたコンテキストをアクティブにする場合があります)。ミニポートドライバーは、登録またはシグナルが失われた後でも、コンテキストを自動的にアクティブにすることはできません。 アクティベーション要求でアクセス文字列が指定されていない場合、ミニポートドライバーは既定の文字列を提供しません。 代わりに、空のアクセス文字列を使用してコンテキストのアクティブ化を続行する必要があります。

一方、ミニポートドライバーは、MB サービスによって指示されたコンテキストを非アクティブにする場合があります。 これは、シグナルの一時的な損失のしきい値を超えた期間、または正常なシャットダウンまたは状態のクリーンアップの一部として、ネットワーク接続が失われた場合に発生する可能性があります。

このバージョンでサポートされているアクティブ化コンテキストは1つだけなので、レイヤー 2 MB 接続を設定または解除するために、特定のコンテキスト量をアクティブ化または非アクティブ化します。

Set 要求の場合、MB サービスは、WWAN\_コンテキスト\_状態データ構造の**ConnectionId**と**ActivationCommand**の両方のパラメーターを提供します。 このメソッドは、 **ActivationCommand**パラメーター値*WwanActivationCommandActivate*または*WwanActivationCommandDeactivate*に基づいて、 **ConnectionId**によって識別されるパケットコンテキストをアクティブ化または非アクティブ化するようにミニポートドライバーに指示します。

-   サービスまたはサブスクリプションにアクティブ化が必要な場合、ミニポートドライバーは、エラーコード WWAN\_ステータス\_サービス\_\_アクティブ化されていないことを返します。 PDP ライセンス認証は、サービスまたはサブスクリプションがアクティブになるまで発生しない可能性があります。 すべての緊急サービスは、デバイスとオペレーターからのサポートの対象となる場合があります。 オペレーティングシステムは、このエラーコードに対する応答として、\_WWAN\_サービス\_アクティブ化の OID を呼び出す場合があります。

-   別のパケットコンテキストが現在アクティブになっているときに、ミニポートドライバーがコンテキストアクティブ化要求を受信すると、エラーコード WWAN\_ステータス\_最大\_アクティブ化された\_コンテキストに戻ります。

-   ミニポートドライバーがコンテキスト非アクティブ化要求を受信しても、 **ConnectionId**によって識別されたコンテキストが現在アクティブになっていない場合は、エラーコード WWAN\_ステータス\_コンテキスト\_\_アクティブ化されていないことを示します。

ミニポートドライバーは、次のロジックを使用して、set 要求からの AccessString、UserName、および Password の設定の有効性を判断します。

-   **ActivationCommand**が*WwanActivationCommandDeactivate*の場合、ミニポートドライバーは、これら3つのパラメーターの設定を無視する必要があります。 その他のケースでは、 **ActivationCommand**が*WwanActivationCommandActivate*の場合にのみ考慮されます。

コンテキストのアクティブ化は、ユーザーのログオンとログオフをまたいで保持されます。 ログオンユーザーごとではありません。

クエリ要求では、MB サービスはこのオブジェクトを使用してアクティブ化の状態を確認します。

クエリ要求への応答として、ミニポートドライバーは、NDIS\_ステータス\_WWAN\_コンテキスト\_状態通知を送信します。

**重要**  注意:

 

まれに、特定の状況では、Windows 7 の MB サービスが自動接続を試行する前に、既存の接続に対して、または既存の接続のインターネット接続が一時的に中断しているときに、インターネットへの接続が試行されることがあります。数. これにより、MB と WLAN/イーサネット接続が同時に発生する可能性があります。 たとえば、システムの起動時に、MB などの接続が同時に試行され、Network List Manager サービスがアクティブおよびパッシブの方法を使用して他の接続のインターネット接続を確認しようとしているときに、この問題が発生する可能性があります。 また、企業のプロキシサーバーや ISP ネットワークなどのネットワークインフラストラクチャの一時的な停止によっても発生する可能性があります。 このため、[代替のインターネット接続が利用できない場合にのみ自動接続する] オプションが選択されているかどうかに関係なく、MB サービスはインターネットへの自動接続を試行することがあります。

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
<td><p>Windows 7 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[WWAN パケットコンテキスト管理](https://docs.microsoft.com/windows-hardware/drivers/network/mb-packet-context-management)

 

 




