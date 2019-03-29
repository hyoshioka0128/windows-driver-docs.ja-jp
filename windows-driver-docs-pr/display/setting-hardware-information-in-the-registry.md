---
title: レジストリ内のハードウェア情報の設定
description: レジストリ内のハードウェア情報の設定
ms.assetid: 82f5d399-58c3-4bed-a3f2-3501f21fa3e8
keywords:
- ハードウェア WDK ビデオのミニポート
- レジストリ WDK ビデオのミニポート
- VideoPortSetRegistryParameters
- VideoPortGetRegistryParameters
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb9433dc4aec4fe869b674e1531b4094827f63f3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570487"
---
# <a name="setting-hardware-information-in-the-registry"></a>レジストリ内のハードウェア情報の設定


## <span id="ddk_setting_hardware_information_in_the_registry_gg"></span><span id="DDK_SETTING_HARDWARE_INFORMATION_IN_THE_REGISTRY_GG"></span>


[*HwVidFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff567332)呼び出すことができます、 [ **VideoPortGetRegistryParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff570316)と[ **VideoPortSetRegistryParameters**](https://msdn.microsoft.com/library/windows/hardware/ff570365)関数を取得および構成情報をレジストリに設定します。 たとえば、 *HwVidFindAdapter*呼び出すことができます**VideoPortSetRegistryParameters**次回のブート レジストリの不揮発性の構成情報を設定します。 呼び出すことがあります**VideoPortGetRegistryParameters**インストール プログラムによってレジストリに書き込む、バス相対、アダプターに固有の構成パラメーターを取得します。

ミニポート ドライバーが、ユーザーとデバッグについての支援に有用な情報を表示するレジストリの特定のハードウェア情報を設定することをお勧めします。 ミニポート ドライバーには、チップの種類、DAC 型、(アダプター) のメモリ サイズおよびアダプターを識別する文字列を設定できます。 この情報は、コントロール パネルの 表示プログラムで表示されます。

ドライバーは、呼び出すことでこの情報を設定**VideoPortSetRegistryParameters**します。 ドライバーの呼び出しは、通常、その*HwVidFindAdapter*ルーチン。

次の表に、ドライバーを選択し、登録できますの詳細を提供情報、 *ValueName*と*ValueData*パラメーターの**VideoPortSetRegistryParameters**:

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
<td align="left"><p>HardwareInformation.ChipType</p></td>
<td align="left"><p>チップの名前を含む null で終わる文字列。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DAC 型</p></td>
<td align="left"><p>HardwareInformation.DacType</p></td>
<td align="left"><p>DAC の名前または ID を含む null で終わる文字列</p></td>
</tr>
<tr class="odd">
<td align="left"><p>メモリ サイズ</p></td>
<td align="left"><p>HardwareInformation.MemorySize</p></td>
<td align="left"><p>アダプターのビデオ メモリの量を MB 単位でを保持する ULONG。</p></td>
</tr>
<tr class="even">
<td align="left"><p>アダプター ID</p></td>
<td align="left"><p>HardwareInformation.AdapterString</p></td>
<td align="left"><p>アダプターの名前を表す、null で終わる文字列。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>BIOS</p></td>
<td align="left"><p>HardwareInformation.BiosString</p></td>
<td align="left"><p>BIOS に関する情報を含む null で終わる文字列。</p></td>
</tr>
</tbody>
</table>

 

 

 





