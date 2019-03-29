---
title: AddReg エントリの設定
description: AddReg エントリの設定
ms.assetid: 6b3e3eea-96d6-4f39-907a-80ef64ba61a9
keywords:
- INF ファイル WDK ジョイスティック、AddReg エントリ
- AddReg エントリ WDK ジョイスティック
- レジストリの WDK ジョイスティック
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: da0fadb5af3a7fdc0b0f386e90e15179845b9961
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582654"
---
# <a name="setting-up-addreg-entries"></a>AddReg エントリの設定





また、INF ファイルは、インストール セクションの AddReg エントリが選択したセクションでは、レジストリ エントリを設定する必要があります。 ミニドライバーを必要とするデバイスでは、以下する必要があります、ドライバーがマルチ メディアのシステム ドライバーが正しく関連付けられていることを確認するように設定。

```cpp
HKR,,DevLoader,,mmdevldr.vxd
HKR,Drivers,,,
HKR,Drivers,MIGRATED,,0
HKR,Drivers\joystick,,,
HKR,,Driver,,vjoyd.vxd
HKR,Drivers\joystick\msjstick.drv,,,
HKR,Drivers\joystick\msjstick.drv,Description,,%OEMJoy.DeviceDesc%
HKR,Drivers\joystick\msjstick.drv,Driver,,msjstick.drv
```

%OEMJoy.DeviceDesc% 文字列は、あらゆるデバイス名の文字列が呼び出されたに置換されます。

このジョイスティックを記述する値は、OEM が定義したキー パス REGSTR 以降の下のレジストリに格納\_パス\_JOYOEM (HKEY 下にある\_ローカル\_マシン)。 このキーの下、OEM が、OEM ジョイスティック ジョイスティックの調整プログラムでは Windows 95/98/me 用のアプリケーションへの表示方法をカスタマイズする静的な値の数を設定できます。 値の名前は、レジストリ内に表示される名前ではなく、以下で説明するこれらの定数の名前は Regstr.h で定義されます。 OEM 定義のすべてのデバイスは、その基本的なプロパティが定義されていると、コントロール パネルの ジョイスティック選択ボックスが表示する名が少なくとも必要です。 読み込まれるミニドライバー、値はミニドライバー VxD (.vxd 拡張機能を含む) の名前を含める必要があります。 OEM 名の値 (REGSTR\_VAL\_JOYOEMNAME)、およびミニドライバー ファイルの名前 (REGSTR\_VAL\_JOYOEMCALLOUT) 値は、単純な文字列。 基本プロパティ REGSTR\_VAL\_JOYOEMDATA 値があることを意味の詳細については、次の文のバイナリ データ。

2 つのダブルワード; があります。最初にはフラグのセットが含まれています、2 つ目は、デバイスがボタンの数。

フラグは、どの軸が存在する場合は、デバイスと解釈する方法の種類を指定します。

フラグのほとんどは、Mmddk.h で定義されます。 DirectX 3.0 で追加された 2 つの新しいフラグは、Dinput.h で定義されます。 次のフラグは、OEM が定義したアナログ ジョイスティック VJoyD によって直接ポーリングの軸を再マップにのみ使用されます。 これらには、アナログのポーリングを行うときに VJoyD の既定の動作を変更するが、ミニドライバーによって返されるデータへの影響はありません。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>JOY_HWS_XISJ1Y</p></td>
<td><p>X は J1 Y 軸です。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_XISJ2X</p></td>
<td><p>X は、J2 X 軸です。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_XISJ2Y</p></td>
<td><p>X は J2 Y 軸です。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_YISJ1X</p></td>
<td><p>Y は、J1 X 軸です。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_YISJ2X</p></td>
<td><p>Y は、J2 X 軸です。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_YISJ2Y</p></td>
<td><p>Y は、J2 Y 軸です。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_RISJ1X</p></td>
<td><p>J1 X 軸には R です。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_RISJ1Y</p></td>
<td><p>J1 Y 軸は R です。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_RISJ2Y</p></td>
<td><p>J2 Y 軸は R です。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_ZISJ1X</p></td>
<td><p>Z は J1 X 軸になります。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_ZISJ1Y</p></td>
<td><p>Z は J1 Y 軸になります。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_ZISJ2X</p></td>
<td><p>Z は J2 X 軸になります。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_POVISJ1X</p></td>
<td><p>J1 X 軸はポーリング ハット スイッチです。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_POVISJ1Y</p></td>
<td><p>J1 Y 軸はポーリング ハット スイッチです。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_POVISJ2X</p></td>
<td><p>J2 X 軸はポーリング ハット スイッチです。</p></td>
</tr>
</tbody>
</table>

 

既定の動作は次のとおりです。

-   J1 X 軸に X が既定値です。

-   J1 Y 軸と Y の既定値です。

-   R (ラダー) は、J2 X 軸を既定値です。

-   J2 Y 軸に Z の既定値です。

-   ハット スイッチ hat (ポーリングとして実装される) 場合は、J2 Y 軸を既定値です。

フラグは、ハット スイッチ データのボタンの組み合わせから、または軸から取得するかどうかを判断するも定義されます。 かどうか、デバイスが VJoyD、喜びによってポーリングされる\_HWS\_POVISBUTTONCOMBOS VJoyD、ハット スイッチを生成するためにボタンの組み合わせを解釈すると、アプリを確認する軸を使用するそれ以外の場合。 場合、ミニドライバーは、次の値をデバイスはポーリング**dwPOV**ハット スイッチ以外\_UNDEFINED とその他のすべてのハット スイッチ計算のオーバーライド。 ただし場合、楽しいこと\_HWS\_POVISBUTTONCOMBOS が設定されている、VJoyD はアナログのジョイスティックの場合と同様に、ボタンを解釈します。 ハット スイッチは Z 軸の値から実行される場合はそれ以外の場合楽しいこと\_HWS\_HASZ が設定されていない場合は R から。 可能であれば、ミニドライバーは、ミニドライバーはハードウェアの実装の詳細については、通常は、ハット スイッチの情報を解釈するジェネリック VJoyD をことを避ける必要があります。

次のフラグを使用して、デバイスがどの機能について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>JOY_HWS_HASZ</p></td>
<td><p>ジョイスティックには、Z (3 番目の軸) の情報。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_HASR</p></td>
<td><p>ジョイスティックには、R (4 番目の軸) の情報。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_HASU</p></td>
<td><p>ジョイスティックには、R (4 番目の軸) の情報。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_HASV</p></td>
<td><p>ジョイスティックには、R (4 番目の軸) の情報。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_HASPOV</p></td>
<td><p>ジョイスティックには、ハット スイッチ hat があります。</p></td>
</tr>
</tbody>
</table>

 

次のフラグを使用して、デバイスの種類について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>JOY_HWS_ISYOKE</p></td>
<td><p>デバイスは、フライト ヨークです。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_ISGAMEPAD</p></td>
<td><p>デバイスは、ゲーム パッドです。</p></td>
</tr>
<tr class="odd">
<td><p>JOY_HWS_ISCARCTRL</p></td>
<td><p>デバイスは、競合の車のコント ローラーです。</p></td>
</tr>
<tr class="even">
<td><p>JOY_HWS_ISHEADTRACKER</p></td>
<td><p>デバイスは、ヘッド トラッカー (DirectX 3.0 で定義) です。</p></td>
</tr>
</tbody>
</table>

 

最後に、楽しみ\_HWS\_DirectX 3.0 で追加された ISGAMEPORTDRIVER フラグは、このミニドライバーがゲームのポートの標準的なポーリングを置き換えられることを示します。

たとえば、8 つのボタンがあり、X の値を取得するデジタル ジョイスティックがあれば、Y、Z、R、および、ハット スイッチする必要があります喜びビットを設定する\_HWS\_HASZ、喜び\_HWS\_HASPOV、および喜び\_HWS\_HASR します。 これにより、次の。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td></td>
<td><p>0x00000001</p></td>
<td><p>JOY_HWS_HASZ</p></td>
<td><p>01,00,00,00</p></td>
</tr>
<tr class="even">
<td><p>|</p></td>
<td><p>0x00000002</p></td>
<td><p>JOY_HWS_HASPOV</p></td>
<td><p>02,00,00,00</p></td>
</tr>
<tr class="odd">
<td><p>|</p></td>
<td><p>0x00080000</p></td>
<td><p>JOY_HWS_HASR</p></td>
<td><p>00,00,08,00</p></td>
</tr>
<tr class="even">
<td><p>=</p></td>
<td><p>0x00080003</p></td>
<td><p>組み合わせ</p></td>
<td><p>03,00,08,00</p></td>
</tr>
</tbody>
</table>

 

これを配置する**DWORD**リトル エンディアン形式で後に、 **DWORD** INF ファイルで、必須 03,00,08,00,08,00,00,00、一連のバイトであることにより、ボタンの数。

INF ファイルで指定されて、残りのレジストリ設定はすべて、標準のコントロール パネルで指定された調整するための手順をカスタマイズし、次に示します。

<a href="" id="regstr-val-joyoemxylabel-"></a>REGSTR\_VAL\_JOYOEMXYLABEL   
この文字列は、テストで見つかった XY 位置コントロール下に表示され、ジョイスティック CPL のダイアログを調整します。

<a href="" id="regstr-val-joyoemzlabel-"></a>REGSTR\_VAL\_JOYOEMZLABEL   
この文字列は、テストの Z 位置コントロール下に表示され、ジョイスティック CPL のダイアログを調整します。

<a href="" id="regstr-val-joyoemrlabel-"></a>REGSTR\_VAL\_JOYOEMRLABEL   
この文字列は、テストで検出された R 位置コントロール下に表示され、ジョイスティック CPL のダイアログを調整します。

<a href="" id="regstr-val-joyoempovlabel-"></a>REGSTR\_VAL\_JOYOEMPOVLABEL   
この文字列は、テストで見つかったハット スイッチ hat コントロール下に表示され、ジョイスティック CPL のダイアログを調整します。

<a href="" id="regstr-val-joyoemulabel-"></a>REGSTR\_VAL\_JOYOEMULABEL   
この文字列は、テストで見つかった U 位置コントロール下に表示され、ジョイスティック CPL のダイアログを調整します。

<a href="" id="regstr-val-joyoemvlabel-"></a>REGSTR\_VAL\_JOYOEMVLABEL   
この文字列は、テストで見つかった V 位置コントロール下に表示され、ジョイスティック CPL のダイアログを調整します。

<a href="" id="regstr-val-joyoemtestmovedesc-"></a>REGSTR\_VAL\_JOYOEMTESTMOVEDESC   
この文字列は、テスト ダイアログ ボックスの 移動 セクションに表示されます。 ジョイスティックをテストする方法をユーザーに説明します。

<a href="" id="regstr-val-joyoemtestbuttondesc-"></a>REGSTR\_VAL\_JOYOEMTESTBUTTONDESC   
この文字列は、テスト ダイアログ ボックスのボタンに表示されます。 ボタンをテストする方法をユーザーに説明します。

<a href="" id="regstr-val-joyoemtestmovecap-"></a>REGSTR\_VAL\_JOYOEMTESTMOVECAP   
この文字列は、テスト ダイアログ ボックスの移動」セクションを囲むグループ ボックスのキャプションとして表示されます。

<a href="" id="regstr-val-joyoemtestbuttoncap-"></a>REGSTR\_VAL\_JOYOEMTESTBUTTONCAP   
この文字列は、テスト ダイアログ ボックスのボタンのセクションを囲むグループ ボックスのキャプションとして表示されます。

<a href="" id="regstr-val-joyoemtestwincap-"></a>REGSTR\_VAL\_JOYOEMTESTWINCAP   
この文字列は、テスト ダイアログ ボックスのキャプションとして表示されます。

<a href="" id="regstr-val-joyoemcalcap-"></a>REGSTR\_VAL\_JOYOEMCALCAP   
この文字列は、[調整] ダイアログ ボックスのキャプションとして表示されます。

<a href="" id="regstr-val-joyoemcalwincap-"></a>REGSTR\_VAL\_JOYOEMCALWINCAP   
この文字列は、[調整] ダイアログ ボックスのキャプションとして表示されます。

<a href="" id="regstr-val-joyoemcal1-"></a>REGSTR\_VAL\_JOYOEMCAL1   
この文字列は、調整のジョイスティックの XY 部分を中央に揃える方法をユーザーに指示します。

<a href="" id="regstr-val-joyoemcal2-"></a>REGSTR\_VAL\_JOYOEMCAL2   
この文字列は、調整のジョイスティックの XY 部分に移動する方法をユーザーに指示します。

<a href="" id="regstr-val-joyoemcal3-"></a>REGSTR\_VAL\_JOYOEMCAL3   
この文字列が、ユーザーをどのように指示に戻しますキャリブレーション ジョイスティックの XY 部分。

<a href="" id="regstr-val-joyoemcal4-"></a>REGSTR\_VAL\_JOYOEMCAL4   
この文字列は、調整のジョイスティックの Z 部分に移動する方法をユーザーに指示します。

<a href="" id="regstr-val-joyoemcal5-"></a>REGSTR\_VAL\_JOYOEMCAL5   
この文字列は、調整のジョイスティックの R の部分に移動する方法をユーザーに指示します。

<a href="" id="regstr-val-joyoemcal6-"></a>REGSTR\_VAL\_JOYOEMCAL6   
この文字列は、調整のジョイスティックの U 部分に移動する方法をユーザーに指示します。

<a href="" id="regstr-val-joyoemcal7-"></a>REGSTR\_VAL\_JOYOEMCAL7   
この文字列は、調整のジョイスティックの V 部分に移動する方法をユーザーに指示します。

<a href="" id="regstr-val-joyoemcal8-"></a>REGSTR\_VAL\_JOYOEMCAL8   
この文字列は、調整のためにハット スイッチ hat を移動する方法をユーザーに指示します。

<a href="" id="regstr-val-joyoemcal9-"></a>REGSTR\_VAL\_JOYOEMCAL9   
この文字列は、ユーザー権利の調整をハット スイッチ hat を移動する方法を指示します。

<a href="" id="regstr-val-joyoemcal10-"></a>REGSTR\_VAL\_JOYOEMCAL10   
この文字列は、ハット スイッチ hat を調整の下に移動する方法をユーザーに指示します。

<a href="" id="regstr-val-joyoemcal11-"></a>REGSTR\_VAL\_JOYOEMCAL11   
この文字列は、調整の残りのハット スイッチ hat を移動する方法をユーザーに指示します。

<a href="" id="regstr-val-joyoemcal12-"></a>REGSTR\_VAL\_JOYOEMCAL12   
この文字列は、調整プロセスが完了したことをユーザーに通知するメッセージで構成されます。

 

 




