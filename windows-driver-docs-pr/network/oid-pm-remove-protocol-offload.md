---
title: OID_PM_REMOVE_PROTOCOL_OFFLOAD
description: セットの要求、NDIS、およびプロトコルのドライバーでは、OID_PM_REMOVE_PROTOCOL_OFFLOAD OID を使用して、削除するようネットワーク アダプターから、電源管理プロトコルの負荷を軽減します。
ms.assetid: efca3018-28bf-4d91-b698-4b1c9e02f6e3
ms.date: 08/08/2017
keywords: -OID_PM_REMOVE_PROTOCOL_OFFLOAD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 4ef4fdfdc6f7b42980212c90bb1b4b69c9426392
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359507"
---
# <a name="oidpmremoveprotocoloffload"></a>OID\_PM\_削除\_プロトコル\_オフロード


OID を使用する NDIS およびプロトコルのドライバー セットの要求として\_PM\_削除\_プロトコル\_オフロードの OID を電源管理のプロトコルを削除するネットワーク アダプターから負荷を軽減します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 **ULONG**プロトコル識別子の負荷を軽減します。

<a name="remarks"></a>注釈
-------

OID を使用する NDIS とプロトコル ドライバー\_PM\_削除\_プロトコル\_プロトコルを削除する OID のオフロードの基になるネットワーク アダプターから負荷を軽減します。

**データ。設定\_INFORMATION.InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体を指す必要があります、 **ULONG**の値を先ほど追加したプロトコルのオフロード識別子。 NDIS このプロトコルのオフロード識別子の設定、 **ProtocolOffloadId**のメンバー、 [ **NDIS\_PM\_プロトコル\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566760)NDIS 送信する前に、構造体[OID\_PM\_追加\_プロトコル\_オフロード](oid-pm-add-protocol-offload.md)を基になるネットワーク アダプターに OID 要求。

### <a name="remarks-for-miniport-driver-writers"></a>ミニポート ドライバー作成者には、「解説」

NDIS により、バッファー サイズが少なくともが**sizeof**(**ULONG**) し、有効なプロトコルのオフロード ID が含まれます そのため、ミニポート ドライバーの[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)関数は、NDIS を返す必要があります\_状態\_この要求の成功します。

**注**  ミニポート ドライバーをリセットする場合、 [ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)関数は、NDIS を返す必要があります\_状態\_いない\_受理します。

 

### <a name="return-status-codes"></a>リターン状態コード

NDIS は、この要求の次のステータス コードのいずれかを返します。

<a href="" id="ndis-status-success"></a>**NDIS\_状態\_成功**  
プロトコルのオフロードが正常に削除されました。

<a href="" id="ndis-status-pending"></a>**NDIS\_状態\_PENDING**  
完了待ちになっています。 NDIS では、要求が完了した後、最終的な状態コードと結果を呼び出し元の OID 要求完了ハンドラーに渡すは。

<a href="" id="ndis-status-invalid-length"></a>**NDIS\_状態\_無効な\_長さ**  
情報バッファーが小さすぎます。 NDIS セット、**データ。設定\_情報。BytesNeeded**内のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)最小バッファー サイズ (バイト単位) を必要とされる構造体。

<a href="" id="ndis-status-file-not-found"></a>**NDIS\_状態\_ファイル\_いない\_が見つかりました**  
OID 要求のプロトコルのオフロード識別子が無効です。

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

[**NDIS\_PM\_プロトコル\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566760)

[OID\_PM\_追加\_プロトコル\_オフロード](oid-pm-add-protocol-offload.md)

 

 




