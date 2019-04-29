---
title: OID_GEN_SUPPORTED_PACKET_FILTERS
description: NDIS と関連付けたドライバー ミニポート アダプターが初期化中にフィルター処理できます net のパケットの種類を取得します。
ms.assetid: c19cecf3-ae47-4fd1-b5dc-1f3de469e548
ms.date: 08/08/2017
keywords: -OID_GEN_SUPPORTED_PACKET_FILTERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 157b47e3be2f47858c051f0600a4c77161696f0f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387886"
---
# <a name="oidgensupportedpacketfilters"></a>OID\_GEN\_サポートされている\_パケット\_フィルター


NDIS と関連付けたドライバー ミニポート アダプターが初期化中にフィルター処理できます net のパケットの種類を取得します。

**注**  この OID は Windows Vista およびそれ以降のバージョンの Windows オペレーティング システムで実装されていません。 詳細については、「解説」を参照してください。

 

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
実装されていません。 (「解説」の「」を参照).

<a name="remarks"></a>注釈
-------

ミニポート ドライバーでは、初期化中に、サポートされているパケット フィルターを指定します。

サポートされているパケット フィルターを指定するミニポート ドライバーの設定、 **SupportedPacketFilters**のメンバー、 [ **NDIS\_ミニポート\_アダプター\_[全般]\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)構造体し、構造体を渡す、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)関数。

NDIS は、プロトコル ドライバーに情報を渡す、 **SupportedPacketFilters**のメンバー、 [ **NDIS\_バインド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff564832)構造体。

内の値**SupportedPacketFilters**フィルターのビットごとの OR 型のフラグが。 フィルターの型のフラグの一覧は、次を参照してください。、 [OID\_GEN\_現在\_パケット\_フィルター](oid-gen-current-packet-filter.md) OID。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)

[**NDIS\_バインド\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff564832)

[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)

[OID\_GEN\_現在\_パケット\_フィルター](oid-gen-current-packet-filter.md)

 

 




