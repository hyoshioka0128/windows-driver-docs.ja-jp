---
title: 廃止されたカーネル モード ドライバー サポート関数
description: 廃止されたカーネル モード ドライバー サポート関数
ms.assetid: 8bdfbd2e-a0d6-424f-9092-297e533efa33
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17ff682aae4bcfda4cd617aea7131fd531c4aba2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363201"
---
# <a name="obsolete-kernel-mode-driver-support-functions"></a>廃止されたカーネル モード ドライバー サポート関数


## <span id="ddk_obsolete_kernel_mode_driver_support_functions_ks"></span><span id="DDK_OBSOLETE_KERNEL_MODE_DRIVER_SUPPORT_FUNCTIONS_KS"></span>


ヘッダー ファイル portcls.hdefines 4 マクロの古いカーネル モード ドライバーのサポート関数の名前を格納します。 これらのマクロは、再コンパイルすると、ソース ファイルへの編集を必要とせず、新しいカーネル関数を使用する古い関数名への参照を含む古いソース コードを許可します。

古い形式の名前を使用するソース コードをコンパイルするときに定義のパラメーター名 PC\_古い\_名。 このパラメーターは、コンパイラのコマンドライン引数を定義できます"-DPC\_古い\_名"ステートメントを導入するよりも便利なかどうかは、`#define PC_OLD_NAMES`ソースにファイル自体。

次の表には、左側にある古いカーネル モード ドライバーのサポート関数名が一覧表示します。 古い名前ごとに、これを置き換える新しいカーネル関数の名前には、右側の列が含まれます。 各ケースでは、マクロ定義は、簡易名の変更に金額します。 古い関数の引数のリストし、新しい関数は同じです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">古い関数名</th>
<th align="left">新しい関数の名前</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WIN95COMPAT_ReadPortUChar</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-read_port_uchar" data-raw-source="[&lt;strong&gt;READ_PORT_UCHAR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-read_port_uchar)"><strong>READ_PORT_UCHAR</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>WIN95COMPAT_WritePortUChar</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-write_port_uchar" data-raw-source="[&lt;strong&gt;WRITE_PORT_UCHAR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-write_port_uchar)"><strong>WRITE_PORT_UCHAR</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>WIN95COMPAT_ReadPortUShort</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-read_port_ushort" data-raw-source="[&lt;strong&gt;READ_PORT_USHORT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-read_port_ushort)"><strong>READ_PORT_USHORT</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>WIN95COMPAT_WritePortUShort</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-write_port_ushort" data-raw-source="[&lt;strong&gt;WRITE_PORT_USHORT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-write_port_ushort)"><strong>WRITE_PORT_USHORT</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 





