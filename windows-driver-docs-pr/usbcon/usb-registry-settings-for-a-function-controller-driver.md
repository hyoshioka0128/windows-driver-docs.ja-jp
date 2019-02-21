---
Description: OEMs must set several registry values to make sure that their device enumerates with the correct metadata when connected to a computer.
title: 関数のコント ローラーのドライバーを USB レジストリ設定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18bf5bde14e3a9fc21d2ae1842ec19281e81a099
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537840"
---
# <a name="usb-registry-settings-for-a-function-controller-driver"></a>関数のコント ローラーのドライバーを USB レジストリ設定


**要約**

-   レジストリ キーの USB ディスクリプターを定義する Oem によって設定する必要があります。

**適用対象します。**

-   Windows 10

**最終更新日。**

-   2015 年 11 月

Oem は、自分のデバイスがコンピューターに接続されている場合は、正しいメタデータを持つ列挙ことを確認するいくつかのレジストリ値を設定する必要があります。 これらの値のデバイスと構成の記述子の指定、 [Windows での USB デバイス側ドライバー](usb-device-side-drivers-in-windows.md)します。 作成し、独自のインターフェイスは、Oem は、そのインターフェイスをロードして使用するために追加のレジストリ値を設定する必要があります。

デバイス側の USB ドライバーに関連するレジストリ キーは下です。

**HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Control**\\**USBFN**

このトピックでは、前のキーとデバイス、構成、およびデバイスのインターフェイスの記述子を定義するサブキーの設定について説明します。

## <a name="usbfn-registry-key"></a>USBFN レジストリ キー


USB デバイスの構成情報は、下は。

**HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Control**\\**USBFN**

このテーブルには、Oem は、このキーの下で変更できるサブキーがについて説明します。 詳細についてはサポートされている各サブキーの値の詳細については、以下のセクションで提供されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>サブキー</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>代替</strong></td>
<td>このサブキーには、1 つまたは複数の代替設定を持つインターフェイスについて説明する追加のサブキーが含まれています。
<p><strong>Hkey_local_machine \system\currentcontrolset\control</strong>&lt;強力な&gt;USBFN</strong>&lt;強力な&gt;交互に設定</strong></p></td>
</tr>
<tr class="even">
<td><strong>関連付け</strong></td>
<td>このサブキーは、インターフェイスの関連付け記述子 (Iad) を定義します。 各 IAD は、1 つの関数にグループ化する複数のインターフェイスを使用できます。 各サブキーは異なる IAD を表し、Oem は、それらのサブキーの値を変更できます。
<p><strong>Hkey_local_machine \system\currentcontrolset\control</strong>&lt;強力な&gt;USBFN</strong>&lt;強力な&gt;の関連付け</strong></p></td>
</tr>
<tr class="odd">
<td><strong>既定値</strong></td>
<td>このサブキーには、VID と PID などのデバイスに固有の設定の記述に使用される既定値が含まれています。 これは、Microsoft が所有しているサブキーの値は、親キーでによってオーバーライドされます。
<p><strong>Hkey_local_machine \system\currentcontrolset\control</strong>&lt;強力な&gt;USBFN</strong></p></td>
</tr>
<tr class="even">
<td><strong>構成</strong></td>
<td>このサブキーには、USB の列挙中に使用される構成記述子の値が含まれているその他のサブキーが含まれています。 標準のテスト構成が存在するなど、 <strong>hkey_local_machine \system\currentcontrolset\control</strong>&lt;強力な&gt;USBFN</strong>&lt;強力な&gt;構成</strong>&lt;強力な&gt;TestConfigClassic</strong>します。</td>
</tr>
<tr class="odd">
<td><strong>Configurations\Default</strong></td>
<td>このサブキーには、既定の構成の値が含まれています。 既定の構成でインターフェイスが現在の構成の前に追加表示するときに、 <strong>IncludeDefaultCfg</strong>で値を設定、 <strong>hkey_local_machine \system\currentcontrolset\control</strong>&lt;強力な&gt;USBFN</strong>キー。</td>
</tr>
<tr class="even">
<td><strong>インターフェイス</strong></td>
<td>このサブキーには、特定のインターフェイスの記述子を記述するその他のサブキーが含まれています。 たとえば、IP over USB 構成もという名前のサブキーの下に存在する<strong>hkey_local_machine \system\currentcontrolset\control</strong>&lt;強力な&gt;USBFN</strong>&lt;強力な&gt;インターフェイス</strong>&lt;強力な&gt;IpOverUsb</strong>します。 インターフェイスには、このサブキーの名前は、クラス ドライバーのハードウェア ID が決まります。 例の USB 経由で IP、ロード PDO の _HID には、 <strong>USBFN\IpOverUsb</strong>します。</td>
</tr>
</tbody>
</table>

 

次の表に Oem が変更できる値の説明、 **HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール**\\ **USBFN**キー。 この表に記載されていない値には、Microsoft によって定義された既定値が前提としています**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール** \\ **USBFN**\\**既定**します。

すべての Oem を設定する必要があります、 **idVendor**、 **idProduct**、 **ManufacturerString**、および**ProductString**値。 作成し、独自のインターフェイスを設定する必要がありますも追加する Oem**設定になっています**の下のサブキーの名前に**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール**\\**USBFN**\\**構成**でそのインターフェイスを含む**InterfaceList**します。

| Value                    | 種類       | 所有者 | 説明                                                                                                                                                                                                                                                                                                                |
|--------------------------|------------|-------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **idVendor**             | REG\_DWORD | OEM   | 列挙中に、ホストに送信されるデバイス記述子の仕入先の識別子です。                                                                                                                                                                                                                               |
| **idProduct**            | REG\_DWORD | OEM   | 列挙中に、ホストに送信されるデバイス記述子の製品識別子。                                                                                                                                                                                                                              |
| **ManufacturerString**   | REG\_SZ    | OEM   | デバイスの製造元を識別するために、ホストに送信される製造元の文字列。                                                                                                                                                                                                                               |
| **ProductString**        | REG\_SZ    | OEM   | 製品としてデバイスを説明する文字列。 既定値は、Windows 10 Mobile デバイスです。 この値は、接続されているコンピューターのユーザー インターフェイスでデバイスの表示名として使用されます。 Oem は、この値が PhoneModelName DeviceTargetingInfo サブキーの下の値と一致することを確認してください。 |
| **iSerialNumber**        | REG\_DWORD | OEM   | この値が 0 に設定されている場合そのデバイスには、シリアル番号項目がありません。 存在しないまたは値が 0 以外の場合、シリアル番号が生成されます一意にデバイスごと。                                                                                                                                            |
| **CurrentConfiguration** | REG\_SZ    | OEM   | この文字列は、構成のサブキーの名前に対応する必要があります。 この文字列は、USB デバイスの列挙の構成記述子の構築に使用するには、どの構成を決定します。                                                                                                                                       |

 

## <a name="usbfnconfigurations-registry-key"></a>USBFN\\レジストリ キーの構成


Oem は、下のサブキーを変更できる値を表**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール**\\ **USBFN**\\**構成**します。 各サブキーは、別の USB 構成を表します。 OEM が独自のインターフェイスを作成する場合は、OEM を使用するインターフェイスを含む新しい構成を定義する必要があります。 これを行うには、下のサブキーを作成**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール**\\**USBFN**\\**構成**を構成の名前を使用し、このテーブル内の値とサブキーを作成します。 さらに、新しい構成を使用する USB ドライバーを**設定になっています**値 (上記の表で説明) は、構成のサブキーの名前に設定する必要があります。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>種類</th>
<th>所有者</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>InterfaceList</strong></td>
<td>REG_MULTI_SZ</td>
<td>OEM または Microsoft</td>
<td><p>インターフェイスのサブキーに対応するインターフェイス名の一覧を含む<strong>hkey_local_machine \system\currentcontrolset\control</strong>&lt;強力な&gt;USBFN</strong>&lt;強力な&gt;インターフェイス</strong>、下で定義されている IAD 関連付け<strong>hkey_local_machine \system\currentcontrolset\control</strong>&lt;強力な&gt;USBFN</strong>&lt;強力な&gt;アソシエーション</strong>とで定義されている代替インターフェイス<strong>hkey_local_machine \system\currentcontrolset\control</strong>&lt;強力な&gt;USBFN</strong>&lt;強力な&gt;代替</strong>します。 これらのキーは、複合構成記述子の記述に使用するインターフェイスを決定します。</p>
<p>場合、 <strong>IncludeDefaultCfg</strong>値、 <strong>hkey_local_machine \system\currentcontrolset\control</strong>&lt;強力な&gt;USBFN</strong>キーが 1 に設定されている、この一覧は、デバイスを列挙するために使用するインターフェイスの完全な一覧を作成する既定の Microsoft が所有しているインターフェイスの一覧に追加されます。</p></td>
</tr>
<tr class="even">
<td><strong>MSOSCompatIdDescriptor</strong></td>
<td>REG_BINARY</td>
<td>OEM または Microsoft</td>
<td><p>(省略可能)。 記述子を定義する拡張互換性 ID OS 機能の構成。 場合、 <strong>IncludeDefaultCfg</strong>値、 <strong>hkey_local_machine \system\currentcontrolset\control</strong>&lt;強力な&gt;USBFN</strong> 1、関数にキーが設定されています。この記述子では、関数と既定の構成でインターフェイスに追加されます。</p></td>
</tr>
</tbody>
</table>

 

## <a name="usbfninterfaces-registry-key"></a>USBFN\\インターフェイスのレジストリ キー


Oem は、下のサブキーを変更できる値を表**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール**\\ **USBFN**\\**インターフェイス**します。

各サブキーは、別の USB インターフェイスを表します。 インターフェイスを定義するには、下のサブキーを作成**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール**\\ **USBFN**\\**インターフェイス**インターフェイスの名前を使用し、次の表の値を設定します。 さらに、インターフェイスにのみ含まれるインターフェイスがの一部である場合、 **InterfaceList**の**設定になっています**します。

| Value                              | 種類        | 所有者            | 説明                                                                                                                                                                                                                                                                                                  |
|------------------------------------|-------------|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **InterfaceDescriptor**            | REG\_バイナリ | OEM または Microsoft | USB の列挙中に、ホストに送信する、インターフェイスの記述子のバイナリ表現です。 **BInterfaceNumber**と**iInterface**値が、USB 関数のスタックで他のインターフェイスとの競合を回避するために完全な構成記述子をコンパイルした後、自動的に設定されます記述子。 |
| **InterfaceGUID**                  | REG\_SZ     | OEM または Microsoft | バスのインターフェイスを一意に識別する GUID です。                                                                                                                                                                                                                                                     |
| **InterfaceNumber**                | REG\_DWORD  | OEM または Microsoft | (省略可能)。 この値は、固定のインターフェイスの数。 関数に割り当てに使用されます。 インターフェイス番号 0-1 f はレガシ関数の予約済み、20-3 f は、Microsoft 用に予約されておよび 40 5 f は、使用するため、Oem で予約されています。                                                                                           |
| **MSOSExtendedPropertyDescriptor** | REG\_バイナリ | OEM または Microsoft | (省略可能)。 拡張 OS 機能のプロパティ記述子、インターフェイスを定義します。                                                                                                                                                                                                                              |

 

## <a name="usbfnalternates-registry-key"></a>USBFN\\代替レジストリ キー


代替のサブキーを使用して、1 つのインターフェイスを持つ 1 つ以上の代替インターフェイスを定義します。 Oem は、下のサブキーを変更できる値を表**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール**\\ **USBFN**\\**代替**します。

各サブキーは、別のインターフェイスを表します。 代替の設定でインターフェイスを定義するには、下のサブキーを作成**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール**\\ **USBFN**\\**代替**で、インターフェイスの名前を使用して、次の表の値を入力します。

| Value                              | 種類           | 所有者            | 説明                                                                                                                                                                                                                                                                                                                                                        |
|------------------------------------|----------------|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **InterfaceList**                  | REG\_マルチ\_SZ | OEM または Microsoft | 2 つの下で定義されているインターフェイスに対応する複数のインターフェイス名の一覧**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール**\\**USBFN**\\**インターフェイス**します。 そのキーは、まとめての代替設定を持つインターフェイスを定義します。 最初のインターフェイスに対応する 2 番目のインターフェイスが別の設定に対応して代替 0 を設定、1 という具合です。 |
| **InterfaceNumber**                | REG\_DWORD     | OEM または Microsoft | (省略可能)。 この値は、固定のインターフェイスの数。 関数に割り当てに使用されます。 インターフェイス番号 0-1 f はレガシ関数の予約済み、20-3 f は、Microsoft 用に予約されておよび 40 5 f は、使用するため、Oem で予約されています。                                                                                                                                                 |
| **MSOSExtendedPropertyDescriptor** | REG\_バイナリ    | OEM または Microsoft | (省略可能)。 拡張 OS 機能のプロパティ記述子、インターフェイスを定義します。                                                                                                                                                                                                                                                                                    |

 

## <a name="usbfnassociations-registry-key"></a>USBFN\\レジストリ キーの関連付け


Oem は、インターフェイスの関連付け記述子 (Iad) を定義することで、アソシエーションを指定できます。 各 IAD は、1 つの関数にグループ化する複数のインターフェイスを使用できます。 Oem は、下のサブキーを変更できる値を表**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール**\\ **USBFN**\\**アソシエーション**します。

各サブキーは、さまざまな IAD を表します。 アソシエーションを定義するには、サブキーを作成**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール**\\ **USBFN**\\**アソシエーション**で、IAD の名を使用し、次の表の値を設定します。

| Value                              | 種類           | 所有者            | 説明                                                                                                                                                                                                                 |
|------------------------------------|----------------|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **InterfaceList**                  | REG\_マルチ\_SZ | OEM または Microsoft | インターフェイス、または USB 関数に関連付けられている代替インターフェイスの一覧。 リストのサイズが 2 未満の場合は、関数のドライバー スタックは読み込みに失敗します。 他の関数またはインターフェイスは、読み込みを続行します。 |
| **bFunctionClass**                 | REG\_DWORD     | OEM または Microsoft | 関数のクラスのコードは、02 に設定します。                                                                                                                                                                                  |
| **bFunctionSubClass**              | REG\_DWORD     | OEM または Microsoft | 関数のサブクラス コードは、0 d に設定します。                                                                                                                                                                               |
| **bFunctionProtocol**              | REG\_DWORD     |                  | 関数のプロトコルのコードは 01 に設定します。                                                                                                                                                                               |
| **MSOSExtendedPropertyDescriptor** | REG\_バイナリ    | OEM または Microsoft | (省略可能)。 拡張 OS 機能のプロパティ記述子、インターフェイスを定義します。                                                                                                                                             |

 

**ユース ケース。MirrorLink を有効にします。**

MirrorLink は、モバイル デバイスと車インフォテインメント システム間の統合が可能にする相互運用性標準です。 デバイスは、MirrorLink クライアントに USB CDC NCM インターフェイスを公開する必要があります。 通信デバイス クラス (CDC) デバイスとしてインターフェイスの関連付け記述子 (IAD) または CDC 関数の共用体の記述子を使用してデータのインターフェイスを記述することが必要です。

Windows 10 Mobile デバイスに接続して MirrorLink を有効にするには、OEM は、IAD を公開するこれらの変更をようにする必要があります。

-   インターフェイスでの通信やデータの関連付けを作成するには、上記の表に示すようにレジストリ値を設定してインターフェイスの関連付け記述子 (IAD) を使用します。
-   レジストリ設定に加えには、このレジストリ値を 0 以外の値に設定します。

    | Value          | 種類       | 所有者            | 説明                                                                                                                     |
    |----------------|------------|------------------|---------------------------------------------------------------------------------------------------------------------------------|
    | **MirrorLink** | REG\_DWORD | OEM または Microsoft | 0 以外の値は、インターフェイス MirrorLink のサポートを示します。 USB 関数のスタックは MirrorLink USB コマンドを停止できません。 |

     

-   クラスに固有の記述子は、レジストリで定義されているインターフェイス記述子のセットに含めることができます。 USB ドライバー スタック関数が正確に解析するため、これらの記述子でサイズ フィールドを設定する必要があります。

また、CDC 関数の共用体記述子もとして定義できますクラス固有のインターフェイス記述子。ただし、共用体の記述子によって指定されたインターフェイスの番号は静的とはできません、USB 機能ドライバー スタックで割り当てられ、共用体の記述子の存在に 1 つの子の PDO を関連付けることによって記述されたインターフェイスは発生しません。 IAD は、関連付けを表す必要があります。

## <a name="related-topics"></a>関連トピック
[Windows での USB デバイス側のドライバー](usb-device-side-drivers-in-windows.md)  
[関数の USB コント ローラーの Windows ドライバーの開発](developing-windows-drivers-for-usb-function-controllers.md)  



