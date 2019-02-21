---
title: NDIS_STATUS_RECEIVE_FILTER_QUEUE_PARAMETERS
description: NDIS_STATUS_RECEIVE_FILTER_QUEUE_PARAMETERS 状態は、NDIS と仮想マシン (VM) キューの現在のパラメーターは、ネットワーク アダプター上で変更されたドライバーの上にあることを示します。
ms.assetid: 30782C77-578F-4533-8B6B-9D2F64EE6189
ms.date: 08/08/2017
keywords: -NDIS_STATUS_RECEIVE_FILTER_QUEUE_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 463316f09dba21515a00594a7d256cfb8de65bd8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528230"
---
# <a name="ndisstatusreceivefilterqueueparameters"></a>NDIS\_状態\_受信\_フィルター\_キュー\_パラメーター


**NDIS\_状態\_受信\_フィルター\_キュー\_パラメーター** NDIS と関連付けたドライバーに状態を示しますが、現在の仮想マシン (VM) のキューネットワーク アダプターのパラメーターが変更されました。

<a name="remarks"></a>注釈
-------

ミニポート ドライバーを発行する必要があります、 **NDIS\_状態\_受信\_フィルター\_キュー\_パラメーター** VM キューの現在のパラメーターがある場合、状態の表示ネットワーク アダプターに変更します。 次の条件のいずれかが true の場合、VM のキューのパラメーターを変更できます。

-   VM のキューのパラメーターは、独立系ハードウェア ベンダー (IHV) によって開発された管理アプリケーションで変更されます。

-   負荷分散マルチプレクサー中間ドライバーによって管理されているフェールオーバー (LBFO) のチームに属している 1 つまたは複数のネットワーク アダプターの VM キューのパラメーターを変更します。 詳細については、次を参照してください。 [NDIS MUX 中間ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff566498)します。

ミニポート ドライバーを発行したとき、 **NDIS\_状態\_受信\_フィルター\_キュー\_パラメーター**状態を示す値、次の手順に従う必要があります。

1.  ミニポート ドライバーを初期化します、 [ **NDIS\_受信\_キュー\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567211)ネットワーク アダプターでは、現在の VM キュー パラメーターを含む構造体。 ドライバーを設定する必要がありますも、**フラグ**適切な NDIS を使用して、この構造体のメンバー\_受信\_キュー\_パラメーター\_*Xxx* \_変更されたフラグをレポートする**NDIS\_受信\_キュー\_パラメーター**が変更されたメンバーの値。

    **注**NDIS 6.30 以降、ミニポート ドライバーのみを発行でき、 **NDIS\_状態\_受信\_フィルター\_キュー\_パラメーター**状態レポートを示す値を変更する、 **InterruptCoalescingDomainId**メンバー。




ミニポート ドライバーを初期化すると、**ヘッダー**この構造体のメンバーは、設定、**型**のメンバー**ヘッダー** NDIS に\_オブジェクト\_型\_既定します。 ミニポート ドライバーのセット、**リビジョン**のメンバー**ヘッダー** NDIS に\_受信\_キュー\_パラメーター\_リビジョン\_2 と**サイズ**NDIS メンバー\_SIZEOF\_受信\_キュー\_パラメーター\_リビジョン\_2。


2.  ミニポート ドライバーを初期化します、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)次のように構造体。

    -   **StatusCode**にメンバーを設定する必要があります**NDIS\_状態\_受信\_フィルター\_キュー\_パラメーター**します。

    -   **StatusBuffer**へのポインターにメンバーを設定する必要があります、 [ **NDIS\_受信\_キュー\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567211)構造体。 この構造体には、NIC のスイッチの現在有効になっているハードウェア機能が含まれています。

    -   **StatusBufferSize** sizeof にメンバーを設定する必要があります ([**NDIS\_受信\_キュー\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff567211))。

3.  ミニポート ドライバーが呼び出すことによって、状態の通知を発行[ **NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)します。 ドライバーへのポインターを渡す必要があります、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体を*StatusIndication*パラメーター。

使用できるドライバーが重なって、 **NDIS\_状態\_受信\_フィルター\_キュー\_パラメーター**でキュー パラメーターの状態を示す値を現在の VM を確認ネットワーク アダプター。 また、これらのドライバーも発行できますオブジェクト識別子 (OID) のクエリ要求の[OID\_受信\_フィルター\_キュー\_パラメーター](oid-receive-filter-queue-parameters.md)をいつでもこれらのパラメーターを取得します。

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
<td><p>NDIS 6.30 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_受信\_キュー\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff567211)

[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[OID\_受信\_フィルター\_キュー\_パラメーター](oid-receive-filter-queue-parameters.md)








