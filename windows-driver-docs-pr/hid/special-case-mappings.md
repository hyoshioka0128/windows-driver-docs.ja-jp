---
title: 特別な大文字小文字マップ
description: 特別な大文字小文字マップ
ms.assetid: 1691e0e5-7b05-40e1-8747-40926f2eba9c
keywords:
- ジョイスティックに WDK を非表示に軸
- 仮想ジョイスティックのドライバー WDK を非表示に軸
- VJoyD WDK HID、軸
- WDK ジョイスティックの軸
- WDK ジョイスティックの特別な大文字小文字マップ
- WDK ジョイスティックの大文字小文字マップ
- WDK のジョイスティックを z 軸の大文字と小文字のマッピング
- コント ローラーの大文字と小文字マッピング WDK ジョイスティックの自動車
- 軸のマッピング
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: efa2a676b2a220e56de1dc74c013060b6dea8e8d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573822"
---
# <a name="special-case-mappings"></a>特別な大文字小文字マップ





により、複雑さとさまざまな入力デバイスの現在利用可能なマッピングのセットを 1 つ使用できますないあらゆる種類のデバイスの。 DirectInput では、このセクションで説明する 2 つの特殊なケースをサポートします。

### <a name="special-case-mapping-for-z-axes"></a>Z 軸の特殊なケースのマッピング

HID で z 軸が説明されているまれなケースでは、目的の WinMM マッピング、2 つの使用可能な上書きがあります。 デバイスが 6 自由度のデバイスの場合は、タイプとサブタイプの上書きの設定 (の参照で説明されている**DIJOYTYPEINFO**) DI8DEVTYPE に\_1STPERSON と DI8DEVTYPE1STPERSON\_SIXDOF次の代替マッピングをそれぞれ呼び出します。

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
<td><p>GUID_RyAxis</p></td>
</tr>
<tr class="even">
<td><p>V</p></td>
<td><p>GUID_RxAxis</p></td>
</tr>
</tbody>
</table>



タイプのオーバーライドを JOYTYPE を含めるように設定する必要がある場合は、デバイスは、6 自由度のデバイスではないが、z 軸を DirectInput を計算する必要があります、\_INFOZISZ します。 このタイプのオーバーライドでは、DirectX 7.0 マッピングに戻す DirectInput をによりします。

GUID の hid を報告するデバイスがあるない既定のマッピング変更\_軸のスライダーでは、GUID の代わりに使用が不要になった\_ZAxis SetDataFormat メソッドと一致します。 HID 軸が本質的に WinMM 軸より詳細に説明されているため、ほとんどの場合に、既定値は動作します。 まれなケースでは、HID として (スロットルとして使用される多くの場合)、スライダーの軸が記述されている\_使用状況\_ページ\_ジェネリック、HID\_使用状況\_Z 軸 WinMM z 軸と同じ方法で使用されるためです。 このようなデバイスを一貫して使用できるかどうかを確認するデバイスに上書きフラグ JOYTYPE\_INFOZISSLIDER を使用することができます。

### <a name="special-case-mappings-for-car-controllers"></a>車のコント ローラーの特殊なマッピング

別の一連の特殊なマッピングが複数の 2 つの軸を宣言する車のコント ローラーの必要なものです。 残念ながら、この領域で、業界内で若干の整合性があります。 別のアクセラレータを表す、ブレーキ ペダル 3 つの一般的な方法が現在存在します。 DirectInput がメソッドに次の疑似コードで示すようなロジックと車のコント ローラーを使用して検出しようとするとします。

```cpp
    if( has_r and has_Z )
        use mappings:
        X => GUID_XAxis
        Z => GUID_YAxis
        R => GUID_RzAxis
    else if( has_r )
        use mappings:
        X => GUID_XAxis
        Y => GUID_YAxis
        R => GUID_RzAxis
    else if( has_z )
        use mappings:
        X => GUID_XAxis
        Y => GUID_RzAxis
        Z => GUID_YAxis
    else
        use default mappings.

   // If the device declares any other axes, they are mapped to sliders.
```

上記のロジックと同じ方法でアプリケーションに報告されるペダルのマッピングのすべて次の 3 つの既知の型になります。 既定のマッピングが失敗した場合、マッピングの種類を使用する選択を上書きフラグを設定できます。 上書きフラグ JOYTYPE\_INFOYYPEDALS、JOYTYPE\_INFOZYPEDALS、JOYTYPE\_INFOYRPEDALS と JOYTYPE\_INFOZRPEDALS がこのドキュメントで別の場所で説明されています。

WinMM と同様は、車のコント ローラーは、HID データ パスを使用している場合に特別なケースのマッピングを必要とします。 デバイスのファームウェアで報告されている正しいシミュレーション ページの使用法の可能性を考慮する余分なバリエーションが WinMM の場合と同様、ここでは同じ方法では、マッピングが行われます。

ジェネリックの軸が同じマッピングが表示され、同じ使用できますがレポートされているデバイスでは、HID と WinMM の両方のデータ パスでのメカニズムをオーバーライドします。 ただし、これらのオーバーライドは汎用主軸だけの影響を与えるデバイス上のすべての軸に対して使用するマッピング テーブルは変わりません。

### <a name="axis-overrides-under-windows-9598me"></a>Windows 95/98/Me 軸の上書き

次のインターフェイスは、軸の上書きによって影響があります。

-   WinMM JoyGetPos()
-   WinMM JoyGetPosEx()
-   **IDirectInput2**
-   **IDirectInput7**
-   **IDirectInput8**

### <a name="to-perform-an-axis-override"></a>実行するには、軸をオーバーライドします。

1.  軸がオーバーライドされるデバイスを接続します。 Joy.cpl またはこのデバイスのレジストリ キーを初期化するために、他の DirectInput アプリケーションを実行します。 デバイスを取り外します。

2.  レジストリを開き、検索 HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\MediaProperties\\PrivateProperties\\ジョイスティック\\OEM

3.  軸がオーバーライドされるデバイスのキーを探します。 キーは、このキーの下にあります、VID & PID の組み合わせによって指定します。

4.  次のサブキーを作成します。

    -   軸
    -   「軸」キーの下には、(軸キー) をオーバーライドする軸ごとに 1 つのキーを指定します。 キーは GUID と軸の情報を記述する 7 を 0 から 1 桁の番号で指定します。

        <table>
        <colgroup>
        <col width="33%" />
        <col width="33%" />
        <col width="33%" />
        </colgroup>
        <thead>
        <tr class="header">
        <th>キー名</th>
        <th>DirectX の GUID</th>
        <th>WinMM 軸</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td><p>0</p></td>
        <td><p>GUID_XAxis</p></td>
        <td><p>x</p></td>
        </tr>
        <tr class="even">
        <td><p>1</p></td>
        <td><p>GUID_YAxis</p></td>
        <td><p>Y</p></td>
        </tr>
        <tr class="odd">
        <td><p>2</p></td>
        <td><p>GUID_ZAxis</p></td>
        <td><p>Z</p></td>
        </tr>
        <tr class="even">
        <td><p>3</p></td>
        <td><p>GUID_RxAxis</p></td>
        <td><p>-</p></td>
        </tr>
        <tr class="odd">
        <td><p>4</p></td>
        <td><p>GUID_RyAxis</p></td>
        <td><p>-</p></td>
        </tr>
        <tr class="even">
        <td><p>5</p></td>
        <td><p>GUID_RzAxis</p></td>
        <td><p>R</p></td>
        </tr>
        <tr class="odd">
        <td><p>6</p></td>
        <td><p>GUID_Slider</p></td>
        <td><p>U</p></td>
        </tr>
        <tr class="even">
        <td><p>7</p></td>
        <td><p>GUID_Slider</p></td>
        <td><p>V</p></td>
        </tr>
        </tbody>
        </table>




-   各軸のキーの下には、オーバーライドする軸を指定します。 という名前のバイナリ値を作成する**属性**に設定します。00 00 00 00 00 HUP HU 00 です。 HUP は、2 桁の 16 進数が無効にするデバイス オブジェクト (軸) の HID の使用に関するページを指定することです。 HU は、デバイス オブジェクトの HID 使用法を指定する 2 桁の 16 進数です。 DIQuick を使用して、これらの値を判断するまたは HID 仕様を参照してください。
-   ケーブルを接続するデバイスでバックアップして任意のプログラムを使用して、上書きが機能するかどうかを確認します。


### <a name="meaning-of-the-registry-keys"></a>レジストリ キーの意味

最初にすべての DirectX インターフェイスの軸のマッピングと WinMM インターフェイスとを区別する必要があります。

DirectX インターフェイスは、オブジェクトを識別するために使用される Guid と一致する Axiskeys を解釈します。 オブジェクトの Guid が、デバイスからのデータの読み取りに使用されで指定された**IDirectInputDevice8::SetDataFormat()** します。 オブジェクトのデータがプログラムによって読み取られたときにこのオブジェクトがオーバーライドされると、し、DirectInput がオーバーライドするオブジェクトからデータを返します。

ご覧のように、スライダー 0 とスライダー DirectInput インターフェイスでは 1 に違いはありません。 これは、6 または 7 の軸をオーバーライドするときに常にオーバーライドする使用可能な最初のスライダーを意味します。 0 のスライダーが軸としてまだ定義されていない、7 を軸にマップする場合は、スライダー 0 はオーバーライドされます。

WinMM インターフェイスはこれに対し、区別する、および V の軸 V 軸が、オーバーライドするオブジェクトからデータを受信する軸 7 がオーバーライドされた場合、軸 6 がオーバーライドされた場合、U 軸によって送信されるデータが変換されます。

### <a name="rules-to-keep-in-mind"></a>ルールに注意してください。

インターフェイスのと同じ動作を保証するために制限の厳しい規則に従う必要があります。 これらの規則は、WinMM インターフェイスの動作によって提供されます。

これらの規則に準拠していないマッピング WinMM インターフェイスの障害をこのデバイスのすべてのデータを報告することがあります。

スライダーのマッピングの相違にこれらの規則は適用されません。このような違いは、許容されます。

次の規則に分類されないすべてのマッピングはサポートされていません。

-   ないホールです。

    軸のマッピングは、上書きを適用した後に継続的である必要があります。 軸の 1 つだけ存在できるマップされていない状態では、「2」GUID =\_ZAxis Z を = です。 軸エントリを省略することはできません。 たとえば、X、Y、Z、R、U、V はシーケンスが無効ですが、X、Z、R、U、V との間に「穴」があるわけでは X、Z。

-   すべての軸が存在します。

    (属性の値で指定) の上書き操作を実行に使用されるすべての軸は、デバイス上に存在する必要があります。

-   マッピングがない「方向」軸を移動しません。

    軸では、上記の表に低いキー名が、する場合、軸 B マッピング軸 C 軸をせずに、軸を割り当てることはできません。

    マッピングなし上方向軸から移行する穴になります。

### <a name="if-the-mapping-is-not-reflected-by-the-interfaces"></a>インターフェイスでは、マッピングは反映されない場合

-   常に、マッピングを変更する前にデバイスを取り外します。 DirectInput を再初期化するために、マッピングを編集した後でデバイスに再度接続します。

-   DirectInput は、特別な上書きを拒否する可能性があります。 キーを確認します。HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\MediaProperties\\PrivateProperties\\DirectInput\\VID & PID、VID & PID が VID-PID-組み合わせ、デバイスです。 Flags2 値セットがある場合は、DirectInput が内部的に軸を軸にマップし、これらのマッピングをオーバーライドすることはできません。 たとえば DInput7/2 および WinMM インターフェイスの z 軸からのスライダーのマッピングを移動することができません。

-   ユーザーは、インストールし、ジョイスティックを調整する場合、結果の調整情報がレジストリに格納されます。 ドライバーがインストールされましたを設定する場合、軸を上書きの以前のレジストリに保存されているものとは異なる、DirectInput には、レジストリに格納されている上書きが適用されます。 レジストリの調整情報が軸のマッピングの変更を反映しないため、データが誤って報告される可能性がありますか、可能性がありますいないで報告されるすべてのオーバーライドの軸。

    これを防ぐために 2 つの方法はあります。

    -   ユーザーは、デバイスを改めることができます。
    -   ドライバーのベンダーのインストールには、レジストリの調整情報を削除できます。

デバイスがそのドライバーとして joyhid.vxd を使用しない場合は、wUsage と wUsagePage 値はどのような使用状況の説明にのみ使用されます使用状況 ページ、オブジェクトは、任意の形式ではなく、として報告する必要がありますをオーバーライドします。 デバイスで、レジストリ キーの HKEY 場合にのみ使用 joyhid.vxd\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\MediaProperties\\PrivateProperties\\ジョイスティック\\OEM\\VID & PID\\OEMCallout joyhid.vxd に等しい。








