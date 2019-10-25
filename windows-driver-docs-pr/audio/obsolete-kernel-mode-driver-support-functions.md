---
title: 廃止されたカーネル モード ドライバー サポート関数
description: 廃止されたカーネル モード ドライバー サポート関数
ms.assetid: 8bdfbd2e-a0d6-424f-9092-297e533efa33
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ccb15f4d9cc89ad4d378ea4fed83811bae03089
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832553"
---
# <a name="obsolete-kernel-mode-driver-support-functions"></a>廃止されたカーネル モード ドライバー サポート関数


## <span id="ddk_obsolete_kernel_mode_driver_support_functions_ks"></span><span id="DDK_OBSOLETE_KERNEL_MODE_DRIVER_SUPPORT_FUNCTIONS_KS"></span>


ヘッダーファイル portcls は、互換性のために残されているカーネルモードドライバーサポート関数の名前を含む4つのマクロを定義します。 これらのマクロを使用すると、古い関数名への参照を含む古いソースコードを再コンパイルして、新しいカーネル関数を使用するようにソースファイルを編集する必要がなくなります。

互換性のために残されている名前を使用するソースコードをコンパイルするときに、パラメーター名として古い\_名\_定義します。 このパラメーターは、コンパイラのコマンドライン引数 "-DPC\_OLD\_NAMES" によって定義できます。これは、ステートメント `#define PC_OLD_NAMES` をソースファイル自体に導入するよりも便利です。

次の表に、左側の列にある、互換性のために残されているカーネルモードドライバーサポート関数の名前を示します。 古い名前については、右側の列に新しいカーネル関数の名前が表示されます。 どちらの場合も、マクロ定義の量は単純な名前変更になります。 互換性のために残されている関数と新しい関数の引数リストは同じです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">廃止された関数名</th>
<th align="left">新しい関数名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WIN95COMPAT_ReadPortUChar</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-read_port_uchar" data-raw-source="[&lt;strong&gt;READ_PORT_UCHAR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-read_port_uchar)"><strong>READ_PORT_UCHAR</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>WIN95COMPAT_WritePortUChar</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-write_port_uchar" data-raw-source="[&lt;strong&gt;WRITE_PORT_UCHAR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-write_port_uchar)"><strong>WRITE_PORT_UCHAR</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>WIN95COMPAT_ReadPortUShort</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-read_port_ushort" data-raw-source="[&lt;strong&gt;READ_PORT_USHORT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-read_port_ushort)"><strong>READ_PORT_USHORT</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>WIN95COMPAT_WritePortUShort</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-write_port_ushort" data-raw-source="[&lt;strong&gt;WRITE_PORT_USHORT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-write_port_ushort)"><strong>WRITE_PORT_USHORT</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 





