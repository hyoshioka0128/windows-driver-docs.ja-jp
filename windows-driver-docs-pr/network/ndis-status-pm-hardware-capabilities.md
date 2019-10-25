---
title: NDIS_STATUS_PM_HARDWARE_CAPABILITIES
description: NDIS_STATUS_PM_HARDWARE_CAPABILITIES の状態は、ネットワークアダプターの電源管理 (PM) ハードウェア機能が変更されたことを示しています。
ms.assetid: A4AACA48-DCD2-44FA-B016-52C37EE9A1D6
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PM_HARDWARE_CAPABILITIES ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: ef77df27720c7ec00afb1a1d750712feddbf966b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843539"
---
# <a name="ndis_status_pm_hardware_capabilities"></a>NDIS\_STATUS\_PM\_ハードウェア\_機能


**NDIS\_STATUS\_PM\_ハードウェア\_機能**の状態は、ネットワークアダプターの電源管理 (pm) ハードウェア機能が変更されたことを示します。

<a name="remarks"></a>注釈
-------

以前に報告された電源管理機能を更新する必要がある場合は、ミニポートドライバーによって、 **\_PM\_ハードウェア\_機能**の状態を示す NDIS\_の状態が生成されます。

802.11 ネットワークアダプターのミニポートドライバーは、この状態を示すことができます。

また、負荷分散フェールオーバー (LBFO) のサポートを提供する MUX 中間ドライバーでも、この状態を示すことができます。 MUX ドライバーは、LBFO チームの一部である基になるネットワークアダプターの PM 機能を集約します。 アダプターがチームに追加または削除されたために PM 機能が変更された場合、MUX ドライバーはこのステータス表示を生成する必要があります。 LBFO MUX 中間ドライバーの詳細については、「 [NDIS Mux 中間ドライバー](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-mux-intermediate-drivers)」を参照してください。

[**Ndis\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体の**statusbuffer**メンバーには、更新された電源管理機能を使用して、 [**ndis\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)構造へのポインターが含まれています。

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
<td><p>NDIS 6.30 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis .h (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)

[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

 

 




