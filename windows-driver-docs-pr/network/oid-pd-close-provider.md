---
title: OID_PD_CLOSE_PROVIDER
description: NDIS プロトコルまたはフィルター ドライバーは、おプロバイダー オブジェクトの PD 機能へのアクセスを断念するおプロバイダーに OID_PD_CLOSE_PROVIDER のオブジェクト識別子 (OID) メソッド要求を送信します。
ms.assetid: 8A504A81-6DC8-415C-9FDC-F03657A0EB87
ms.date: 08/08/2017
keywords: -OID_PD_CLOSE_PROVIDER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: cb89d22693c13b4fa2aa8ee966c6edf0a46acf2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551217"
---
# <a name="oidpdcloseprovider"></a>OID\_PD\_閉じる\_プロバイダー


OID のオブジェクト識別子 (OID) メソッド要求を送信する NDIS プロトコルまたはフィルター ドライバー\_PD\_閉じる\_おプロバイダーおプロバイダー オブジェクトの PD 機能へのアクセスを提供するプロバイダー。

NDIS プロトコルまたはフィルター ドライバーは、バインドの解除通知を一時停止を示す値、省電力イベントの場合、または、バインディング、PD が無効になっているかを示す PD 構成変更イベントを受信すると、この OID を呼び出す必要があります。

この OID を呼び出す前に NDIS プロトコルまたはフィルター ドライバーをする必要があることは、クローズされ、キュー、カウンター、および PD プロバイダーのインスタンスを作成したフィルターなどのすべての PD オブジェクトを解放ことが確認します。 NDIS プロトコルまたはフィルター ドライバーする必要があることを保証しない PD プロバイダーのディスパッチのいずれかに進行中の呼び出しテーブル関数この OID を発行する前にします。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*MiniportOidRequest*](https://msdn.microsoft.com/library/windows/hardware/ff559416)

[**NDIS\_PD\_閉じる\_プロバイダー\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/dn931834)

[NDIS\_状態\_PD\_現在\_構成](https://msdn.microsoft.com/library/windows/hardware/dn931850)

[OID\_PD\_オープン\_プロバイダー](oid-pd-open-provider.md)

 

 




