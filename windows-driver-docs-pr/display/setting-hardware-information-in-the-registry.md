---
title: レジストリ内のハードウェア情報の設定
description: レジストリ内のハードウェア情報の設定
ms.assetid: 82f5d399-58c3-4bed-a3f2-3501f21fa3e8
keywords:
- ハードウェア WDK ビデオミニポート
- レジストリ WDK ビデオミニポート
- VideoPortSetRegistryParameters
- VideoPortGetRegistryParameters
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e584229255493126e6e6489493dd838a6fab246a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829501"
---
# <a name="setting-hardware-information-in-the-registry"></a>レジストリ内のハードウェア情報の設定


## <span id="ddk_setting_hardware_information_in_the_registry_gg"></span><span id="DDK_SETTING_HARDWARE_INFORMATION_IN_THE_REGISTRY_GG"></span>


[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)は、 [**VideoPortGetRegistryParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportgetregistryparameters)関数と[**VideoPortSetRegistryParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportsetregistryparameters)関数を呼び出して、レジストリ内の構成情報を取得および設定できます。 たとえば、 *HwVidFindAdapter*は**VideoPortSetRegistryParameters**を呼び出して、次回の起動時にレジストリに不揮発性構成情報を設定する場合があります。 インストールプログラムによってレジストリに書き込まれる、アダプター固有のバス相対構成パラメーターを取得するために、 **VideoPortGetRegistryParameters**を呼び出す場合があります。

ミニポートドライバーでは、レジストリ内の特定のハードウェア情報を設定して、ユーザーに有用な情報を表示したり、デバッグを支援したりすることをお勧めします。 ミニポートドライバーでは、チップの種類、DAC の種類、メモリサイズ (アダプター)、およびアダプターを識別する文字列を設定できます。 この情報は、コントロールパネルの [ディスプレイ] プログラムによって表示されます。

ドライバーは、 **VideoPortSetRegistryParameters**を呼び出すことによってこの情報を設定します。 通常、ドライバーは*HwVidFindAdapter*ルーチンで呼び出しを行います。

次の表は、ドライバーが登録できる情報と、 **VideoPortSetRegistryParameters**の*ValueName*と*valuedata*パラメーターの詳細を示しています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エントリの情報</th>
<th align="left"><em>ValueName</em></th>
<th align="left"><em>ValueData</em></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>チップの種類</p></td>
<td align="left"><p>ChipType</p></td>
<td align="left"><p>チップ名を含む Null で終了する文字列。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DAC 型</p></td>
<td align="left"><p>ハードウェア情報 DacType</p></td>
<td align="left"><p>DAC の名前または ID を含む Null で終了する文字列。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>メモリサイズ</p></td>
<td align="left"><p>ハードウェア情報. MemorySize</p></td>
<td align="left"><p>アダプターのビデオメモリの量を MB 単位で含む ULONG。</p></td>
</tr>
<tr class="even">
<td align="left"><p>アダプター ID</p></td>
<td align="left"><p>ハードウェア情報. AdapterString</p></td>
<td align="left"><p>Null で終わる、アダプターの名前を含む文字列。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>BIOS</p></td>
<td align="left"><p>ハードウェア情報 (BiosString)</p></td>
<td align="left"><p>BIOS に関する情報を格納している Null で終わる文字列。</p></td>
</tr>
</tbody>
</table>

 

 

 





