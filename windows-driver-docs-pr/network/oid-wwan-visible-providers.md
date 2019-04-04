---
title: OID_WWAN_VISIBLE_PROVIDERS
description: OID_WWAN_VISIBLE_PROVIDERS は、現在表示されている MB デバイスの範囲内のネットワーク プロバイダーの一覧を返します。
ms.assetid: 4dfd4477-6332-4163-8b3e-a1604b11d175
ms.date: 08/08/2017
keywords: -OID_WWAN_VISIBLE_PROVIDERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c89393ed05e71b34bc042167077da386607d814d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574293"
---
# <a name="oidwwanvisibleproviders"></a>OID\_WWAN\_VISIBLE\_プロバイダー


OID\_WWAN\_VISIBLE\_プロバイダーが現在表示されている MB デバイスの範囲内でネットワーク プロバイダーの一覧を返します。

要求のセットがサポートされていません。

ミニポート ドライバーは、最初に、非同期的には、NDIS を返すクエリ要求を処理する必要があります\_状態\_INDICATION\_元の要求とそれ以降の送信に必要な[ **NDIS\_状態\_WWAN\_VISIBLE\_プロバイダー** ](ndis-status-wwan-visible-providers.md)状態通知を含む、 [ **NDIS\_WWAN\_表示される\_プロバイダー** ](https://msdn.microsoft.com/library/windows/hardware/ff567948)クエリ要求を完了するときに表示されているネットワーク プロバイダーに関する情報を提供する構造体。

*クエリ*要求指定 NDIS\_WWAN\_取得\_VISIBLE\_プロバイダーが入力として構造体します。 ときに、**アクション**WWAN でメンバー\_取得\_VISIBLE\_WWAN にプロバイダーが設定されている\_取得\_VISIBLE\_プロバイダー\_すべて、ミニポートには、参照できるすべてのプロバイダーを返す必要があります。 ときに、**アクション**WWAN でメンバー\_取得\_VISIBLE\_WWAN にプロバイダーが設定されている\_取得\_VISIBLE\_プロバイダー\_マルチミニポート ホーム プロバイダーとして設定できるマルチ キャリア プロバイダーの表示を返すのみ必要があります。

デバイスでする必要がありますが、プロバイダーの状態が正しく設定プロバイダーごとに表示されているプロバイダーの一覧が返されます。 たとえば、マルチ優先、プロバイダーは、WWAN としてタグ付けする必要があります\_プロバイダー\_状態\_優先\_マルチ、WWAN としてタグ付けする必要がありますいずれかの場合は、現在のホーム プロバイダー\_プロバイダー\_状態\_ホーム、現在では WWAN としてタグ付けする必要がありますいずれかの場合、プロバイダーが登録されている\_プロバイダー\_状態\_登録されています。

**Rssi**と**ErrorRate** WWAN のメンバー\_PROVIDER2 構造は、使用可能な場合、設定する必要があります。

<a name="remarks"></a>コメント
-------

詳細については、この OID を使用して、[WWAN プロバイダー操作](https://msdn.microsoft.com/library/windows/hardware/ff559101)を参照してください。

ミニポート ドライバー Subscriber Identity Module (SIM カード) にアクセスできる処理がクエリ操作が、プロバイダーのネットワークにアクセスしないでください。

ミニポート ドライバーを設定する必要があります、 **VisibleListHeader.ElementType**メンバー *WwanStructProvider*します。

CDMA ベースのネットワークでは、ミニポート ドライバーはネットワークで、優先ローミング リスト (PRL) のいずれかが現在表示されている場合は、ホーム プロバイダーのみを返す必要があります。 GSM ベースのネットワークでは、1 つ以上のプロバイダーが表示されているプロバイダーの一覧に存在する可能性があります。

デバイスをサポートしないスキャン表示されているプロバイダーの接続中には、WWAN を返す必要がありますの\_状態\_ビジー状態のエラー値、 **uStatus**の NDIS メンバー\_WWAN\_表示される\_プロバイダーの構造体。

GSM ベースし、CDMA ベースの両方のデバイスでは、登録済みのモードで表示されているプロバイダーのスキャンをサポートする必要があります。 ただし、ミニポート ドライバーは、パケット データ プロトコル (PDP) コンテキストがアクティブな間に表示されているプロバイダーのスキャンをサポートする必要はありません (たとえば、デバイスから、プロバイダーのネットワークに接続が)。

<a name="requirements"></a>必要条件
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


[**NDIS\_WWAN\_VISIBLE\_プロバイダー**](https://msdn.microsoft.com/library/windows/hardware/ff567948)

[**NDIS\_状態\_WWAN\_VISIBLE\_プロバイダー**](ndis-status-wwan-visible-providers.md)

[WWAN プロバイダー操作](https://msdn.microsoft.com/library/windows/hardware/ff559101)

 

 




