---
title: 軸の選択の上書き
description: 軸の選択の上書き
ms.assetid: 151c3d19-2f80-4d71-a004-10c16c691fb9
keywords:
- ジョイスティックに WDK を非表示に軸
- 仮想ジョイスティックのドライバー WDK を非表示に軸
- VJoyD WDK HID、軸
- WDK ジョイスティックの軸
- 軸の選択 WDK ジョイスティックをオーバーライドします。
- WDK HID 使用法をページします。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7e9a71b9b80628ad79a6b560ab9afd01bd12ae18
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578662"
---
# <a name="axis-selection-overrides"></a>軸の選択の上書き





DirectX 8.0 リリースには、DirectInput の HID 準拠のデバイスの軸を割り当てる方法を変更することをハードウェア ベンダーに提供する新しいメカニズムが導入されています。 最初の軸の選択が軸インスタンスでデバイスに HID の使用状況/使用量のページ ペアの間のアソシエーションを通して行われます。 軸のインスタンスは、オプションのレジストリ サブキーの下に記載されて、**軸**デバイスの種類のキーのサブキー。 (なお、**軸**サブキーは、デバイスの種類のキーの下のオプションのキーもです)。内で、**軸**サブキー、属性の値が DIOBJECTATTRIBUTES 構造体を格納します。 DirectX 8.0 では、前に、 **wUsagePage**と**wUsage** DIOBJECTATTRIBUTES 構造体のフィールドが非 HID デバイス上のオブジェクトに HID の使用状況 ページと使用状況を割り当てられています。 これらのメンバーは、HID 準拠デバイスに対して無視されました。

DirectX 8.0 のリリースでは、これらのメンバーと関連する HID 準拠のデバイスにもなりました。 これらは、HID の使用状況 ページと、検索する特定の DirectInput 軸のジョイスティックのデータ形式で DirectInput を参照する必要がある使用状況について説明します。 ハードウェア ベンダーでは、大きい DirectInput がさまざまな Windows オペレーティング システムでの軸をマップする方法の一貫性を強制するこれらのフィールドを利用できます。 ただし、これらはリマップ軸の推奨メカニズムではありません。

**注**  軸マッピングは静的な場合は、デバイスを使用中に、これらの値が変更された場合、動作は定義されませんので。 軸の推奨一致を行えず、提案されているマッピングがないものとして処理は続行されます。

 

たとえば、HID の完全な実装のプラットフォームで使用できるように設計ジョイスティック デバイス\_使用状況\_ページ\_ゲーム制御します。 このようなデバイスとして HID で X と Y 軸を表す場合があります。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>Axis</th>
<th>使用状況 ページ</th>
<th>使用方法</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>x</p></td>
<td><p>5</p></td>
<td><p>24</p></td>
<td><p>ゲームのページで、左/右に移動します。</p></td>
</tr>
<tr class="even">
<td><p>Y</p></td>
<td><p>5</p></td>
<td><p>25</p></td>
<td><p>ゲームのページ、前方/後方移動</p></td>
</tr>
</tbody>
</table>

 

DirectInput (または JoyHID) でこれらのシナリオが直接認識されないためには、ゲームに非常に便利なことはできません。 DirectInput で X と Y 軸として認識させるには、次のレジストリ エントリを追加できます。

```cpp
[DIRECT_INPUT_TYPES\ VID_vvvv&PID_pppp)\Axes\0]
     Binary Attributes = 00 00 00 00 05 00 24 00

[DIRECT_INPUT_TYPES\ VID_vvvv&PID_pppp)\Axes\1]
     Binary Attributes = 00 00 00 00 05 00 25 00

Where "DIRECT_INPUT_TYPES" is a token for the following root key:
HKLM\SYSTEM\CurrentControlSet\Control\MediaProperties\PrivateProperties\Joystick\OEM
```

このメカニズムは、インターフェイス、DirectInput 8.0 のインターフェイスと、JoyHID.Vxd、WinMM サポートのために使用する VJoyD ミニドライバーの上下 DirectInput 7.0 で実装されています。

Windows 95/98/Me では、USB ゲーム コント ローラーの 3 つのデータ パスがあります。

-   IHV は、ミニドライバーは他の方法の VJoyD VJoyD ミニドライバーで同じデータを報告する VxD を提供できます。 この場合、軸の選択は、IHV の制御下では完全には。

-   DirectInput は、デバイスと通信するために、オペレーティング システムで提供される HID 実装を使用できます。 この場合、軸の選択がデバイスのファームウェアまたはレジストリ フラグ (前述) に従って行われます。

-   システム既定 HID-VJoyD にドライバー (JoyHID.VxD) を使用できます。

DirectInput (VJoyD.VxD) を使用して JoyHID.VxD を使用して、DIRECTINPUT の指定されたアプリケーションのデータを読み取る\_バージョンより小さいは 0x0700 の場合は、JOYTYPE\_NOHIDDIRECT フラグは、デバイスに指定されました。 場合、直接\_INPUTVERSION は 0x0700 以上、DirectInput は HID を使用して、デバイスと対話します。

JoyHID VJoyD/パスが実行したときに、次の表は HID の使用状況/使用量のページ ペアを WinMM 軸と一致します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>WinMM 軸</th>
<th>使用状況 ページ</th>
<th>使用方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>x</p></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_X</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_RY</p></td>
</tr>
<tr class="odd">
<td><p>Y</p></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_Y</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_RX</p></td>
</tr>
<tr class="odd">
<td><p>Z</p></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_Z</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>HID_USAGE_PAGE_SIMULATION</p></td>
<td><p>HID_USAGE_SIMULATION_THROTTLE</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_SLIDER</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_DIAL</p></td>
</tr>
<tr class="odd">
<td><p>R</p></td>
<td><p>HID_USAGE_PAGE_SIMULATION</p></td>
<td><p>HID_USAGE_SIMULATION_RUDDER</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_RZ</p></td>
</tr>
<tr class="odd">
<td><p>U</p></td>
<td><p>HID_USAGE_PAGE_SIMULATION</p></td>
<td><p>HID_USAGE_SIMULATION_THROTTLE</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_SLIDER</p></td>
</tr>
<tr class="odd">
<td></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_DIAL</p></td>
</tr>
<tr class="even">
<td></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_RY</p></td>
</tr>
<tr class="odd">
<td><p>V</p></td>
<td><p>HID_USAGE_PAGE_GENERIC</p></td>
<td><p>HID_USAGE_GENERIC_RX</p></td>
</tr>
</tbody>
</table>

 

**注**  マッピング、R、するおよび V の軸のラベルへ流れ落ちる、[次へ] の軸のマッピングが存在しない場合 X、Y、Z のマッピングは互いに完全に独立します。 これは VJoyD.VxD のみの連続軸のセットをサポートするためです (たとえば、X、Y、Z の R はサポートされているが U、X、Y、Z はありません)。 この規則に対する唯一の例外が行われるの正確な組み合わせを使用して、ジョイスティック X、Y と R、または X、Y、Z、R および V します。マッピングのこのメソッドは、JoyHID.VxD VJoyD.VxD を許容できない軸の割り当ては、可能性を回避するのに役立ちます。

 

 

 




