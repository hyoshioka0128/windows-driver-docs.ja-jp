---
title: OID_PM_ADD_WOL_PATTERN
description: セットとしては、NDIS プロトコル ドライバーは、ネットワーク アダプターに電源管理の wake on LAN のパターンを追加するのに OID_PM_ADD_WOL_PATTERN OID を使用します。 NDIS_OID_REQUEST 構造体の InformationBuffer メンバーには、NDIS_PM_WOL_PATTERN 構造体へのポインターが含まれています。
ms.assetid: 1005cebb-8ead-4d16-b3ea-5a74da0b054f
ms.date: 08/08/2017
keywords: -OID_PM_ADD_WOL_PATTERN ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0d6e7bf7c4d7078e49b7022a69f9ac2422a3a831
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538242"
---
# <a name="oidpmaddwolpattern"></a>OID\_PM\_追加\_WOL\_パターン


NDIS プロトコル ドライバーが、OID を使用し、セットとして\_PM\_追加\_WOL\_ネットワーク アダプターに電源管理の wake on LAN のパターンを追加するパターンの OID。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_PM\_WOL\_パターン**](https://msdn.microsoft.com/library/windows/hardware/ff566768)構造体。

<a name="remarks"></a>注釈
-------

NDIS 6.20 が動作し、後でプロトコル ドライバーを使用して、OID\_PM\_追加\_WOL\_LAN (WOL) パターンにネットワーク アダプターに、ウェイクを追加するパターン。 OID 要求には、低電力状態にあるときに、ネットワーク アダプターが受信パケットと比較する必要があります条件が含まれています。 ネットワーク アダプターには、パターンの条件に一致するパケットを受信したときにイベントをウェイクを生成する必要があります。

プロトコル ドライバーは、基になるネットワーク アダプターに正常にバインドした後、および WOL パターンを設定する必要があるインターフェイスの IP アドレス) など、必要なデータとすぐに WOL パターンを追加できます。 プロトコル ドライバーに通知に応答していくつかその他の電源管理イベントで記述された拒否など、以前に追加された WOL パターンまたはオフロードのプロトコルの WOL パターンを追加できます。

NDIS およびその他のネットワーク アダプターを低電力状態に設定する NDIS の開始後に、同じミニポート アダプタにバインドされているプロトコル ドライバーでの競合状態を避けるためには、そのネットワーク アダプターにパターンを新しいウェイク アップを追加しようとすると失敗になります。 NDIS プロトコル ドライバーの処理のコンテキストで新しい WOL パターンを追加しようとする場合など、 **NetEventSetPower** NDIS そのネットワーク アダプターのイベント通知には、要求が失敗します。

NDIS は、NDIS ドライバーは、基になるまでこの OID 要求を送信または上にあるドライバーへの要求が完了すると、前に設定、ULONG **PatternId**のメンバー、 [ **NDIS\_PM\_WOL\_パターン**](https://msdn.microsoft.com/library/windows/hardware/ff566768)を一意の値構造体。 プロトコル ドライバーおよび NDIS でこのパターンの識別子を使用して、 [OID\_PM\_削除\_WOL\_パターン](oid-pm-remove-wol-pattern.md)WOL パターンを基になるネットワーク アダプターから削除する OID 要求。

**注**  パターン識別子は、ネットワーク アダプターに設定されているパターンのそれぞれに一意の値。 ただし、パターンの識別子はすべてミニポート アダプター間でグローバル一意識別ありませんなりました。

 

生成 NDIS または基になるネットワーク アダプターは、WOL パターンを削除した場合、 [ **NDIS\_状態\_PM\_WOL\_パターン\_REJECTED** ](https://msdn.microsoft.com/library/windows/hardware/ff567414)状態を示す値。 **StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体には却下された ULONG WOL パターン識別子が含まれていますWOL パターン。

ミニポート ドライバーでは、要求の状態コードの次のいずれかを返します。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求されたパターンが正常に追加されました。 **PatternId**の NDIS メンバー\_PM\_WOL\_パターンの構造にはパターン識別子が含まれています。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_PENDING  
完了待ちになっています。 NDIS では、要求が完了した後、最終的な状態コードと結果を呼び出し元の OID 要求完了ハンドラーに渡すは。

<a href="" id="ndis-status-pm-wol-pattern-list-full"></a>NDIS\_状態\_PM\_WOL\_パターン\_一覧\_完全  
パターンの一覧がいっぱいで、ネットワーク アダプターが別のパターンを追加することはできません、要求が失敗しました。

<a href="" id="ndis-status-resources"></a>NDIS\_状態\_リソース  
NDIS または基になるネットワーク アダプターでは、リソースが不足しているため、新しいパターンを追加でしたできません。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_状態\_無効な\_パラメーター  
NDIS で 1 つまたは複数のパラメーター\_PM\_WOL\_パターンの構造が無効です。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_状態\_バッファー\_すぎます\_短い  
情報バッファーが小さすぎます。 NDIS セット、**データ。設定\_情報。BytesNeeded** NDIS でメンバー\_OID\_構造体を最小バッファー サイズを要求が必要です。

<a href="" id="ndis-status-not-supported"></a>NDIS\_状態\_いない\_サポートされています。  
ネットワーク アダプターでは、要求された WOL パターンをサポートしません。

<a href="" id="ndis-status-failure"></a>NDIS\_状態\_エラー  
上記の理由以外の理由、要求が失敗しました。

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
<td><p>以降では、NDIS 6.20 が動作をサポートします。 ミニポート ドライバーには必須です。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_PM\_WOL\_パターン**](https://msdn.microsoft.com/library/windows/hardware/ff566768)

[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NDIS\_状態\_PM\_WOL\_パターン\_拒否済み**](https://msdn.microsoft.com/library/windows/hardware/ff567414)

[OID\_PM\_削除\_WOL\_パターン](oid-pm-remove-wol-pattern.md)

[OID\_PNP\_追加\_WAKE\_を\_パターン](oid-pnp-add-wake-up-pattern.md)

 

 




