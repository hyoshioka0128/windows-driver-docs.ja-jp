---
title: NDIS_STATUS_PM_HARDWARE_CAPABILITIES
description: NDIS_STATUS_PM_HARDWARE_CAPABILITIES 状態は、後続のネットワーク アダプターの電源管理 (PM) のハードウェア機能の変更が発生したドライバーを示します。
ms.assetid: A4AACA48-DCD2-44FA-B016-52C37EE9A1D6
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PM_HARDWARE_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 61ecf125922f6c318968941532b461de36a8d811
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363088"
---
# <a name="ndisstatuspmhardwarecapabilities"></a>NDIS\_状態\_PM\_ハードウェア\_機能


**NDIS\_状態\_PM\_ハードウェア\_機能**ドライバーに関連する状態を示しますネットワークの電源管理 (PM) のハードウェア機能の変更アダプターが発生しました。

<a name="remarks"></a>コメント
-------

ミニポート ドライバーが生成されます、 **NDIS\_状態\_PM\_ハードウェア\_機能**と以前に報告された電源管理機能の更新プログラムの状態表示必要です。

802.11 のネットワーク アダプターのミニポート ドライバーでは、この状態を示す値を生成できます。

負荷分散のフェールオーバー (LBFO) のサポートを提供する MUX 中間ドライバーには、この状態を示す値を生成できます。 MUX driver は、基になるネットワーク アダプター LBFO チームの一部であるの PM 機能を集計します。 PM 機能は、アダプターが、追加または削除されたチームのために変更する場合、MUX ドライバーは、この状態を示す値を生成する必要があります。 LBFO MUX 中間ドライバーの詳細については、次を参照してください。 [NDIS MUX 中間ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff566498)します。

**StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体にはへのポインターが含まれています、 [ **NDIS\_PM\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)更新された電源管理機能を含む構造体。

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
<td><p>NDIS 6.30 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_PM\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)

[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

 

 




