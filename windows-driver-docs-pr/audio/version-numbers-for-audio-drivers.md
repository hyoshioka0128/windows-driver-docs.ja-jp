---
title: オーディオ ドライバーのバージョン番号
description: オーディオ ドライバーのバージョン番号
ms.assetid: 6d621021-eb45-40ab-9452-97c9be2bbdd8
keywords:
- バージョン番号の WDK オーディオ
- オーディオのミニポート ドライバー WDK、バージョン番号
- ミニポート ドライバー WDK オーディオ、バージョン番号
- オーディオ ドライバー WDK、バージョン番号
- アダプターのオーディオ ドライバー WDK、バージョン番号
- アダプターのドライバー WDK オーディオ、バージョン番号
- オーディオ ドライバー WDK、サポートされているモデル
- ドライバー バージョン番号の WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f228b9b65cbe0500f1b618070dded00519f62bb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551233"
---
# <a name="version-numbers-for-audio-drivers"></a>オーディオ ドライバーのバージョン番号


## <span id="version_numbers_for_audio_drivers"></span><span id="VERSION_NUMBERS_FOR_AUDIO_DRIVERS"></span>


Windows オペレーティング システムは、3 種類のオーディオ ドライバー モデルをサポート: VxD、WDM、および NT4 (Microsoft Windows NT 4.0) ドライバー モデル。 バージョン番号、オーディオ ドライバーに割り当てることを使用することは、ターゲット、およびおそらく Microsoft DirectX リリースにも、Windows リリースしたドライバー モデルによって異なります。 次の 4 つのテーブルでは、ドライバー モデルによってドライバー バージョン番号を示します。

### <a name="span-iddrivermodelvxddriversforwindows95spanspan-iddrivermodelvxddriversforwindows95spandriver-model-vxd-drivers-for-windows-95"></a><span id="driver_model__vxd_drivers_for_windows_95"></span><span id="DRIVER_MODEL__VXD_DRIVERS_FOR_WINDOWS_95"></span>ドライバー モデル:Windows 95 のドライバーを VxD

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DirectX のリリース</th>
<th align="left">ドライバー バージョン番号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DirectX をサポートしていない windows 95</p></td>
<td align="left"><p>4.00.00.0096 に 4.02.00.0094</p></td>
</tr>
<tr class="even">
<td align="left"><p>DX1</p></td>
<td align="left"><p>4.02.00.0096 に 4.02.00.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DX2</p></td>
<td align="left"><p>4.03.00.1097 に 4.03.00.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>DX3</p></td>
<td align="left"><p>4.04.00.1097 に 4.04.00.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DX5</p></td>
<td align="left"><p>4.05.00.1000 に 4.05.00.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>DX6</p></td>
<td align="left"><p>4.06.00.1000 に 4.06.00.9999</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddrivermodelvxddriversforwindows98spanspan-iddrivermodelvxddriversforwindows98spandriver-model-vxd-drivers-for-windows-98"></a><span id="driver_model__vxd_drivers_for_windows_98"></span><span id="DRIVER_MODEL__VXD_DRIVERS_FOR_WINDOWS_98"></span>ドライバー モデル:Windows 98 VxD ドライバー

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DirectX のリリース</th>
<th align="left">ドライバー バージョン番号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DX5</p></td>
<td align="left"><p>4.05.01.2500 に 4.05.99.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>DX6</p></td>
<td align="left"><p>4.06.00.1000 に 4.06.00.9999</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddrivermodelwdmdriversforwindowsme98andwindows2000andlatespanspan-iddrivermodelwdmdriversforwindowsme98andwindows2000andlatespandriver-model-wdm-drivers-for-windows-me98-and-windows-2000-and-later"></a><span id="driver_model__wdm_drivers_for_windows_me_98__and_windows_2000_and_late"></span><span id="DRIVER_MODEL__WDM_DRIVERS_FOR_WINDOWS_ME_98__AND_WINDOWS_2000_AND_LATE"></span>ドライバー モデル:Windows 用の WDM ドライバー Me/98、および Windows 2000 以降

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows のリリース</th>
<th align="left">ドライバー バージョン番号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 98</p></td>
<td align="left"><p>4.10.00.2500 に 4.10.00.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 2000</p></td>
<td align="left"><p>5.00.00.3500 に 5.00.00.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Me</p></td>
<td align="left"><p>4.90.00.3500 に 4.90.00.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP</p></td>
<td align="left"><p>5.10.00.3500 に 5.10.00.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Vista</p></td>
<td align="left"><p>6.00.00.3500 に 6.00.00.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 7</p></td>
<td align="left"><p>7.00.00.3500 に 7.00.00.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows 8</p></td>
<td align="left"><p>8.00.00.3500 に 8.00.00.9999</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddrivermodelnt4driverswindowsnt40onlyspanspan-iddrivermodelnt4driverswindowsnt40onlyspandriver-model-nt4-drivers-windows-nt-40-only"></a><span id="driver_model__nt4_drivers__windows_nt_4_0_only_"></span><span id="DRIVER_MODEL__NT4_DRIVERS__WINDOWS_NT_4_0_ONLY_"></span>ドライバー モデル:NT4 ドライバー (Windows NT 4.0 のみ)

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows のリリース</th>
<th align="left">ドライバー バージョン番号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Windows NT 4.0</p></td>
<td align="left"><p>4.00.00.1400 に 4.00.00.9999</p></td>
</tr>
</tbody>
</table>

 

4.00.00.0096 以上、DirectX をサポートしていないデバイス ドライバーのバージョン番号があります 4.02.00.0094 以下。 DirectX のバージョン 1.0 をサポートするデバイス ドライバーは、範囲 4.02.00.0096 に 4.02.00.9999 バージョン番号が必要です。 DirectX の以降のバージョンをサポートするデバイス ドライバーは、前述の表に示すようの DirectX 分散バージョンに適切な範囲内でバージョン番号を持つ必要があります。

すべて WDM ドライバーよりも大きいバージョン番号が必要、または Windows 98 のバージョン番号の範囲の下限をある 4.10.00.2500 と等しい。

以降のバージョンも、以前のバージョンの Windows 向けに作成された WDM ドライバーが正しく動作に注意してください。 たとえば、Windows 2000 で実行に書き込まれた WDM ドライバーは、Microsoft Windows XP 以降をも実行されます。

DirectX のバージョン 1.0 ドライバーは、DirectX 2.0 がインストールされているシステムで動作します。 ただし、DirectX 2.0 がインストールされていない場合、DirectX 2.0 ドライバーが正しく動作しない操作を行います。 DirectX 3.0 と以降のリリースも同様です。

クロスプラット フォーム対応ドライバーは、ドライバーが実行されているプラットフォームの最新のバージョン番号にそのバージョン番号を設定する必要があります。 たとえば、仕入先は 5.00.00 のドライバー バージョン番号を使用する必要があります。*Xxxx* Windows 2000、Windows 98、Windows 98 SE、および Windows me. をサポートするドライバーについて

このセクションの内容:

[内部および外部のバージョン番号](internal-and-external-version-numbers.md)

[INF ドライバーのバージョンのエントリ](inf-driver-version-entry.md)

[DirectX のファイルのバージョン番号](directx-file-version-numbers.md)

 

 




