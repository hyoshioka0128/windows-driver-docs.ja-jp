---
title: 軸の選択
description: 軸の選択
ms.assetid: 5ba78609-d5e7-44b1-86e8-5a677a19aadd
keywords:
- ジョイスティックに WDK を非表示に軸
- 仮想ジョイスティックのドライバー WDK を非表示に軸
- VJoyD WDK HID、軸
- WDK ジョイスティックの軸
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec3007bcf34e6737329a3020ff6566ff42f7fc37
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581829"
---
# <a name="axis-selection"></a>軸の選択





このセクションには、DirectInput が DirectInput および Windows のマルチ メディア アプリケーションで使用するための軸をマップする方法についての情報が含まれています。

このセクションの内容:

[軸の選択の上書き](axis-selection-overrides.md)

[特別な大文字小文字マップ](special-case-mappings.md)

### <a name="windows-2000-legacy-interfaces"></a>Windows 2000 では、従来のインターフェイス

Windows 2000 では、DirectX 7.0 API を使用して、軸の割り当てがによって次の表に示すように、デバイス ドライバーを軸が公開されている順序で行われます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>使用状況 ページ</th>
<th>使用方法</th>
<th>DirectInput 軸</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_X</p></td>
<td><p>GUID_XAxis</p></td>
</tr>
<tr class="even">
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_Y</p></td>
<td><p>GUID_YAxis</p></td>
</tr>
<tr class="odd">
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_Z</p></td>
<td><p>GUID_ZAxis</p></td>
</tr>
<tr class="even">
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_WHEEL</p></td>
<td><p>GUID_ZAxis</p></td>
</tr>
<tr class="odd">
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_RX</p></td>
<td><p>GUID_RxAxis</p></td>
</tr>
<tr class="even">
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_RY</p></td>
<td><p>GUID_RyAxis</p></td>
</tr>
<tr class="odd">
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_RZ</p></td>
<td><p>GUID_RzAxis</p></td>
</tr>
<tr class="even">
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_HATSWITCH</p></td>
<td><p>GUID_POV</p></td>
</tr>
<tr class="odd">
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_SLIDER</p></td>
<td><p>GUID_Slider</p></td>
</tr>
<tr class="even">
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_DIAL</p></td>
<td><p>GUID_Slider</p></td>
</tr>
<tr class="odd">
<td><p>HID_USAGE_PAGE_SIMULATION</p></td>
<td><p>HID_USAGE_SIMULATION_STEERING</p></td>
<td><p>GUID_XAxis</p></td>
</tr>
<tr class="even">
<td><p>HID_USAGE_PAGE_SIMULATION</p></td>
<td><p>HID_USAGE_SIMULATION_ACCELERATOR</p></td>
<td><p>GUID_YAxis</p></td>
</tr>
<tr class="odd">
<td><p>HID_USAGE_PAGE_SIMULATION</p></td>
<td><p>HID_USAGE_SIMULATION_BRAKE</p></td>
<td><p>GUID_RzAxis</p></td>
</tr>
<tr class="even">
<td><p>HID_USAGE_PAGE_SIMULATION</p></td>
<td><p>HID_USAGE_SIMULATION_RUDDER</p></td>
<td><p>GUID_RzAxis</p></td>
</tr>
<tr class="odd">
<td><p>HID_USAGE_PAGE_SIMULATION</p></td>
<td><p>HID_USAGE_SIMULATION_THROTTLE</p></td>
<td><p>GUID_Slider</p></td>
</tr>
<tr class="even">
<td><p>HID_USAGE_PAGE_GAME</p></td>
<td><p>HID_USAGE_ SIMULATION_POV</p></td>
<td><p>GUID_POV</p></td>
</tr>
</tbody>
</table>

 

これらの Guid は、デバイス オブジェクトを要求したデータ形式と一致する SetDataFormat によって使用されます。 DIRECTINPUT でコンパイルされたアプリケーションの\_バージョン&lt;データ形式、GUID を指定する場合は 0x0600\_GUID の前に ZAxis\_(データ形式は既定のジョイスティック) としてスライダーとスライダーがで検出された、デバイスとして、z 軸、z 軸をし、スライダーを検索する前にします。 これは、HID との互換性を向上するためものです。

### <a name="windows-9x-platforms"></a>Windows 9x プラットフォーム

Windows 95/98/私に DirectX 7.0 インターフェイスを通じて DirectInput 軸に WinMM 軸のマッピングは 1 次元。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>WinMM 軸</th>
<th>DirectInput 割り当て</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>x</p></td>
<td><p>GUID_XAxis</p></td>
</tr>
<tr class="even">
<td><p>Y</p></td>
<td><p>GUID_YAxis</p></td>
</tr>
<tr class="odd">
<td><p>Z</p></td>
<td><p>GUID_ZAxis</p></td>
</tr>
<tr class="even">
<td><p>R</p></td>
<td><p>GUID_RzAxis</p></td>
</tr>
<tr class="odd">
<td><p>U</p></td>
<td><p>GUID_Slider</p></td>
</tr>
<tr class="even">
<td><p>V</p></td>
<td><p>GUID_Slider</p></td>
</tr>
</tbody>
</table>

 

WinMM 軸は、以下に示すよう、DirectX 8.0 インターフェイスを介して異なる方法でマップされます。

**注**  が JoyHID.VxD はまだステアリングの車両コントロールの使用法をマップする、高速化されず、ブレーキ、ハンドルの使用状況を確認し、1 つが見つかった場合は、WinMM 車のコント ローラーとして、デバイスを扱います。 また、いずれかのコピー JoyHID.VxD の DirectX 8.0 バージョン IHV WinMM コント ローラーの型のフラグを指定する (楽しいこと\_HWS\_ISYOKE、喜び\_HWS\_ISGAMEPAD、喜び\_HWS\_ISCARCTRL または喜び\_HWS\_ISHEADTRACKER) の数、ボタンでは、IHV OEMData のレジストリ値でこれらの型を設定できるようにします。

 

DirectX 8.0 インターフェイスによって行われたマッピングは、従来のインターフェイスで行われたものと異なるです。 次の表では、DirectX 8.0 インターフェイスでのマッピングについて説明します。

WinMM を介して取得したデータは、既定のマッピングは次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>WinMM 軸</th>
<th>DirectInput 割り当て</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>x</p></td>
<td><p>GUID_XAxis</p></td>
</tr>
<tr class="even">
<td><p>Y</p></td>
<td><p>GUID_YAxis</p></td>
</tr>
<tr class="odd">
<td><p>Z</p></td>
<td><p>GUID_Slider</p></td>
</tr>
<tr class="even">
<td><p>R</p></td>
<td><p>GUID_RzAxis</p></td>
</tr>
<tr class="odd">
<td><p>U</p></td>
<td><p>GUID_Slider</p></td>
</tr>
<tr class="even">
<td><p>V</p></td>
<td><p>GUID_Slider</p></td>
</tr>
</tbody>
</table>

 

ゲーム デバイスの 3 つ目の軸は z 軸ではまれであるために、これらのマッピングは、Windows 2000、Windows XP および Windows 95/98/Me HID との互換性を向上を実現するのに役立ちます。

 

 




