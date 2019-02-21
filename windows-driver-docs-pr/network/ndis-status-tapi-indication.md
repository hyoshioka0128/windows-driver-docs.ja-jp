---
title: NDIS_STATUS_TAPI_INDICATION
description: NDIS_STATUS_TAPI_INDICATION 状態では、TAPI イベントが発生したことを示します。 対応 WAN ミニポート ドライバーには、TAPI の状態を示します。
ms.assetid: b90c5524-2e03-45e1-9ec9-478112eba01b
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_TAPI_INDICATION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6f587338985eedc6b1556c5795f07ac3caa0a3e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557245"
---
# <a name="ndisstatustapiindication"></a>NDIS\_状態\_TAPI\_を示す値


NDIS\_状態\_TAPI\_INDICATION 状態では、TAPI イベントが発生したことを示します。 対応 WAN ミニポート ドライバーには、TAPI の状態を示します。

<a name="remarks"></a>注釈
-------

NDIS 4。*x*と以前の NDIS WAN ミニポート ドライバーは、この状態を示す値を使用します。 NDIS 5.0 およびそれ以降の WAN ミニポート ドライバーには、いる CoNDIS WAN インターフェイスを使用する必要があります。 いる CoNDIS WAN インターフェイスの詳細については、次を参照してください。[実装いる CoNDIS WAN ミニポート ドライバー (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff546752)します。

*StatusBuffer*のパラメーター、 [ **NdisMIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff553538)関数にはへのポインターが含まれています、 [ **NDIS\_TAPI\_イベント**](https://msdn.microsoft.com/library/windows/hardware/ff558986)構造体。NDIS\_TAPI\_イベントの構造には、TAPI 行または呼び出しイベント (例では、行と呼び出しの状態を着信とリモート ノードで、既存のミニポート ドライバーまたは終了の到着の変更が発生したがについて説明します呼び出しまたは行)。

NDIS の詳細については\_状態\_TAPI\_を示す値を参照してください[を示す NDIS WAN ミニポート ドライバーの状態 (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff546867)します。

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
<td><p>NDIS 6.0 のドライバーまたは Windows Vista または Windows XP で 5.1 の NDIS ドライバーのサポートされていません。 NDIS 4.x ドライバーのサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_TAPI\_イベント**](https://msdn.microsoft.com/library/windows/hardware/ff558986)

[**NdisMIndicateStatus**](https://msdn.microsoft.com/library/windows/hardware/ff553538)

 

 




