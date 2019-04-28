---
title: OID_PM_GET_PROTOCOL_OFFLOAD
description: ネットワーク アダプターからオフロード低電力のプロトコルのパラメーターの設定を取得する OID_PM_GET_PROTOCOL_OFFLOAD の OID メソッド要求を遮断のドライバーの問題です。
ms.assetid: c14b9278-6f24-41a1-bc2e-536a75460ecd
ms.date: 08/08/2017
keywords: -OID_PM_GET_PROTOCOL_OFFLOAD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7b2c88f2d96334bdf074d3ac1dcb994922e2bd6b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362317"
---
# <a name="oidpmgetprotocoloffload"></a>OID\_PM\_取得\_プロトコル\_オフロード


OID の OID メソッド要求を発行する上位のドライバー\_PM\_取得\_プロトコル\_オフロード低電力のプロトコルのパラメーターの設定を取得するネットワーク アダプターから負荷を軽減します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体には最初に ULONG プロトコルのオフロードへのポインターが含まれています識別子です。 OID メソッドの要求から正常に戻った後、 **InformationBuffer**のメンバー、 **NDIS\_OID\_要求**構造体にはへのポインターが含まれています、 [**NDIS\_PM\_プロトコル\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566760)構造体。

<a name="remarks"></a>注釈
-------

NDIS 6.20 が動作し、後でプロトコル ドライバーを使用して、OID\_PM\_取得\_プロトコル\_オフロード メソッド低電力プロトコル パラメーター設定を取得する OID のネットワーク アダプターから負荷を軽減します。

情報バッファーは、ULONG 型プロトコル オフロード識別子 をポイントする必要があります。 NDIS でこのプロトコルのオフロード識別子の設定、 **ProtocolOffloadId**のメンバー、 [ **NDIS\_PM\_プロトコル\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566760)NDIS 送信する前に、構造体[OID\_PM\_追加\_プロトコル\_オフロード](oid-pm-add-protocol-offload.md)を基になるネットワーク アダプターに OID 要求。

ミニポート ドライバーでは、要求の状態コードの次のいずれかを返します。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求されたデータが正常に取得されたとします。 情報に対応する NDIS\_PM\_プロトコル\_オフロード構造体。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_PENDING  
完了待ちになっています。 最終的な状態コードと結果は、呼び出し元の OID 要求完了ハンドラーに渡されるされます。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_状態\_無効な\_パラメーター  
指定したプロトコルのオフロード識別子が無効です。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_状態\_バッファー\_すぎます\_短い  
情報バッファーが小さすぎます。 NDIS セット、**データ。クエリ\_情報。BytesNeeded** NDIS でメンバー\_OID\_構造体を最小バッファー サイズを要求が必要です。

<a href="" id="ndis-status-not-supported"></a>NDIS\_状態\_いない\_サポートされています。  
ミニポート ドライバーの NDIS バージョン 6.20 次に示します。

<a href="" id="ndis-status-failure"></a>NDIS\_状態\_エラー  
上記の理由以外の理由、要求が失敗しました。

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
<td><p>以降では、NDIS 6.20 が動作をサポートします。 ミニポート ドライバーには必須です。 (「解説」の「」を参照).</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_PM\_プロトコル\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566760)

[OID\_PM\_追加\_プロトコル\_オフロード](oid-pm-add-protocol-offload.md)

 

 




