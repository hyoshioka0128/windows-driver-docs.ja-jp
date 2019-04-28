---
title: NDIS_STATUS_WAN_CO_LINKPARAMS
description: NDIS_STATUS_WAN_CO_FRAGMENT 状態では、VC いる CoNDIS ミニポート アダプターでアクティブになっている特定のパラメーターが変更されたことを示します。
ms.assetid: a28460fc-c9e6-49c4-949a-badd3491cdd6
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WAN_CO_LINKPARAMS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 996bfab89bfb5debd7fd1429c9fafb6a3d244354
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380917"
---
# <a name="ndisstatuswancolinkparams"></a>NDIS\_状態\_WAN\_CO\_LINKPARAMS


NDIS\_状態\_WAN\_CO\_フラグメントの状態は、VC いる CoNDIS ミニポート アダプターでアクティブになっている特定のパラメーターが変更されたことを示します。

<a name="remarks"></a>注釈
-------

**StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体にはへのポインターが含まれています、 [ **WAN\_CO\_LINKPARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff565819)構造体。 WAN\_CO\_LINKPARAMS 構造は、VC の新しいパラメーターをについて説明します。

NDIS の詳細については\_状態\_WAN\_CO\_LINKPARAMS を参照してください[を示している CoNDIS WAN ミニポート ドライバー ステータス](https://msdn.microsoft.com/library/windows/hardware/ff554825)します。 いる CoNDIS WAN インターフェイスの詳細については、次を参照してください。[いる CoNDIS の WAN ミニポート ドライバーを実装する](https://msdn.microsoft.com/library/windows/hardware/ff553805)します。

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
<td><p>NDIS 6.0 および NDIS 5.1 のドライバーを Windows Vista でサポートされています。 Windows XP で 5.1 の NDIS ドライバーのサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**WAN\_CO\_LINKPARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff565819)

 

 




