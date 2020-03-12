---
Description: Oem は、コンピューターに接続されたときに、デバイスが正しいメタデータを使用して列挙できるように、いくつかのレジストリ値を設定する必要があります。
title: 機能コントローラー ドライバー用 USB レジストリ設定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce5546ca1c7ee20beb181252f6b26256af0939fc
ms.sourcegitcommit: 387de60712790691970924e059b0564325e211bc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/11/2020
ms.locfileid: "79083152"
---
# <a name="usb-registry-settings-for-a-function-controller-driver"></a>機能コントローラー ドライバー用 USB レジストリ設定


**要約**

-   USB 記述子を定義するために Oem によって設定される必要があるレジストリキー。

**適用対象:**

-   Windows 10

**最終更新日時:**

-   2015 年 11 月

Oem は、コンピューターに接続されたときに、デバイスが正しいメタデータを使用して列挙できるように、いくつかのレジストリ値を設定する必要があります。 これらの値は、 [Windows の USB デバイス側ドライバー](usb-device-side-drivers-in-windows.md)のデバイス記述子と構成記述子を指定します。 独自のインターフェイスを作成して含める Oem は、インターフェイスを読み込んで使用するために、追加のレジストリ値を設定する必要があります。

デバイス側の USB ドライバーに関連するレジストリキーは次のとおりです。

**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\USBFN**

このトピックでは、デバイスのデバイス、構成、およびインターフェイス記述子を定義する、前のキーとサブキーの設定について説明します。

## <a name="usbfn-registry-key"></a>USBFN レジストリキー


USB デバイスの構成情報は次のとおりです。

**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\USBFN**

次の表では、そのサブキーについて説明します。 これらの一部は Oem によって変更される場合があります。 各サブキーでサポートされている値の詳細については、以下のセクションで説明します。

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
<td><strong>切り替える</strong></td>
<td>このサブキーには、1つまたは複数の代替設定を持つインターフェイスを説明する追加のサブキーが含まれています。</td>
</tr>
<tr class="even">
<td><strong>連盟</strong></td>
<td>このサブキーは、インターフェイスの関連付け記述子 (IADs) を定義します。 各 IAD では、複数のインターフェイスを1つの関数にグループ化することができます。 各サブキーは別の IAD を表し、Oem はそれらのサブキーの値を変更できます。</td>
</tr>
<tr class="odd">
<td><strong>既定</strong></td>
<td>このサブキーには、VID や PID などのデバイス固有の設定を記述するために使用される既定値が含まれています。 これは、値が親キーの値によってオーバーライドされる Microsoft 所有のサブキーです。</td>
</tr>
<tr class="even">
<td><strong>構成</strong></td>
<td>このサブキーには、USB 列挙中に使用される構成記述子の値を含むサブキーが含まれています。 たとえば、標準のテスト構成が<strong>HKEY_LOCAL_MACHINE \system\currentcontrolset\control\usbfn\configurations\testconfig</strong>の下に存在する場合があります。</td>
</tr>
<tr class="odd">
<td><strong>既定値 (既定)</strong></td>
<td>これは、Microsoft が所有するサブキーです。 既定の構成の値が含まれています。 <strong>HKEY_LOCAL_MACHINE \System\CurrentControlSet\Control\USBFN キーの下で<strong>Includedefaultcfg</strong>値が1に設定されている場合、既定の構成のインターフェイスは、現在の構成の前に追加されます。</td>
</tr>
<tr class="even">
<td><strong>Interfaces</strong></td>
<td>このサブキーには、特定のインターフェイス記述子を説明する追加のサブキーが含まれています。 たとえば、IP over USB インターフェイスは<strong>HKEY_LOCAL_MACHINE \system\currentcontrolset\control\usbfn\interfaces\ipoverusb</strong>の下に存在する場合があります。 このインターフェイスサブキーの名前は、USBFn クラスドライバーを読み込むための USBFN 子デバイスのハードウェア ID としても使用されます。 IP over USB の例では、USBFN 子デバイスのハードウェア ID は<strong>USBFN\IpOverUsb</strong>になります。</td>
</tr>
</tbody>
</table>

 

次の表では、 **\_ローカル\_コンピューター\\システム\\CurrentControlSet\\コントロール\\USBFN**キーで oem が定義できる値について説明します。 このキーで定義されていない値は、 **HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\コントロール\\USBFN\\default**の下で、Microsoft によって定義された既定値を前提としています。

すべての Oem は**Idvendor**、 **idvendor**、 **ManufacturerString**、および**productstring**の値を設定する必要があります。 また、独自のインターフェイスを作成して追加するには、[HKEY] の下のサブキーの名前に**Currentconfiguration**を設定する必要があります。これは、 **interfacelist**内のインターフェイスを含む **\_ローカル\_コンピューター\\システム\\CurrentControlSet\\コントロール\\usbfn\\構成**です。

| 値 | 種類 | 所有者 | 説明|
|--|--|--|--|
| **IncludeDefaultCfg** | REG\_DWORD | OEM | Oem が IpOverUsb や MTP などの既定の構成のインターフェイスを含める場合は、を1に設定します。 |
| **idVendor** | REG\_DWORD | OEM | 列挙中にホストに送信されるデバイス記述子のベンダー識別子。 |
| **idProduct** | REG\_DWORD | OEM | 列挙中にホストに送信されるデバイス記述子の製品識別子。 |
| **ManufacturerString** | REG\_SZ| OEM | デバイスの製造元を識別するためにホストに送信される製造元文字列。 |
| **ProductString** | REG\_SZ| OEM | デバイスを製品として記述する文字列。 既定値は Windows 10 Mobile デバイスです。 この値は、接続されているコンピューターのユーザーインターフェイスのデバイスの表示名として使用されます。 Oem は、この値が DeviceTargetingInfo サブキーの下にある PhoneModelName の値と一致することを確認する必要があります。 |
| **iSerialNumber**| REG\_DWORD | OEM | この値が0に設定されている場合、デバイスにはシリアル番号がありません。 この値が0以外の場合、または存在しない場合、シリアル番号はデバイスごとに一意に生成されます。 |
| **CurrentConfiguration** | REG\_SZ | OEM | この文字列は、構成サブキーの名前に対応している必要があります。 この文字列は、USB デバイス列挙の構成記述子の作成に使用する構成を決定します。 |

 

## <a name="usbfnconfigurations-registry-key"></a>USBFN\\構成のレジストリキー


次の表では、 **HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\コントロール\\USBFN\\構成**のサブキーに対して oem が定義できる値について説明します。 各サブキーは、異なる USB 構成を表します。 OEM が独自のインターフェイスを作成する場合は、使用するインターフェイスを含む新しい構成を OEM が定義する必要があります。 これを行うには、HKEY の下にサブキーを作成し **\_LOCAL\_MACHINE\\System\\CurrentControlSet\\** 構成の名前を使用してサブキーにこのテーブルの値を設定します。\\\\ さらに、USB ドライバーで新しい構成を使用するには、前の表に記載されている**Currentconfiguration**値を構成サブキーの名前に設定する必要があります。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
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
<td><p><strong>HKEY_LOCAL_MACHINE \system\currentcontrolset\control\usbfn\interfaces</strong>の下のインターフェイスサブキー、 <strong>HKEY_LOCAL_MACHINE \system\currentcontrolset\control\usbfn\associations</strong>で定義されている iad アソシエーション、および<strong>HKEY_LOCAL_MACHINE \system\currentcontrolset\control\usbfn\alternates</strong>で定義されている代替インターフェイスに対応するインターフェイス名の一覧が含まれています。 これらのキーは、複合構成記述子の記述に使用されるインターフェイスを決定します。</p>
<p><strong>HKEY_LOCAL_MACHINE \system\currentcontrolset\control\usbfn</strong>キーの<strong>includedefaultcfg</strong>値が1に設定されている場合、この一覧は、デバイスが列挙に使用する完全なインターフェイスリストを作成するために、Microsoft が所有する既定のインターフェイスリストに追加されます。</p></td>
</tr>
<tr class="even">
<td><strong>MSOSCompatIdDescriptor</strong></td>
<td>REG_BINARY</td>
<td>OEM または Microsoft</td>
<td><p>省略可。 構成の拡張された Compat ID OS 機能記述子を定義します。 <strong>HKEY_LOCAL_MACHINE \system\currentcontrolset\control\usbfn</strong>キーの<strong>includedefaultcfg</strong>値が1に設定されている場合、この記述子の関数は、既定の構成の関数とインターフェイスに追加されます。</p></td>
</tr>
</tbody>
</table>

 

## <a name="usbfninterfaces-registry-key"></a>USBFN\\インターフェイスのレジストリキー


次の表では、 **HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\コントロール\\USBFN\\インターフェイス**のサブキーについて、oem が変更できる値について説明します。

各サブキーは、異なる USB インターフェイスを表します。 インターフェイスを定義するには、HKEY の下にサブキーを作成し **\_LOCAL\_MACHINE\\System\\CurrentControlSet\\** インターフェイスの名前を使用して usbfn\\インターフェイスを作成し、次の表の値を設定します。\\ さらに、インターフェイスは、インターフェイスが**Currentconfiguration**の**interfacelist**の一部である場合にのみ含まれます。

| 値                              | 種類        | 所有者            | 説明                                                                                                                                                                                                                                                                                                  |
|------------------------------------|-------------|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **InterfaceDescriptor**            | REG\_バイナリ | OEM または Microsoft | USB 列挙中にホストに送信するインターフェイス記述子のバイナリ表現。 **BInterfaceNumber**値と**iinterface**値は、他のインターフェイス記述子との競合を避けるために、完全な構成記述子をコンパイルした後、USB 関数スタックによって自動的に設定されます。 |
| **InterfaceGUID**                  | REG\_SZ     | OEM または Microsoft | バス上のインターフェイスを一意に識別する GUID。                                                                                                                                                                                                                                                     |
| **InterfaceNumber**                | REG\_DWORD  | OEM または Microsoft | 省略可。 この値は、関数に固定のインターフェイス番号を割り当てるために使用されます。 インターフェイス番号 0-1F はレガシ関数用に予約されており、20-3F は Microsoft 用に予約されており、40 5F (は Oem が使用するために予約されています。                                                                                           |
| **MSOSExtendedPropertyDescriptor** | REG\_バイナリ | OEM または Microsoft | 省略可。 インターフェイスの拡張プロパティ OS 機能記述子を定義します。                                                                                                                                                                                                                              |

 

## <a name="usbfnalternates-registry-key"></a>USBFN\\代替レジストリキー


代替サブキーは、1つまたは複数の代替インターフェイスを持つ1つのインターフェイスを定義するために使用されます。 次の表では、 **HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Control\\USBFN\\代替**のサブキーに対して oem が変更できる値について説明します。

各サブキーは、異なるインターフェイスを表します。 代替設定を使用してインターフェイスを定義するには、HKEY の下にサブキーを作成し **\_LOCAL\_MACHINE\\System\\CurrentControlSet\\コントロール\\USBFN\\** インターフェイスの名前を使用して代替を行い、次の表に示す値を設定します。

| 値                              | 種類           | 所有者            | 説明                                                                                                                                                                                                                                                                                                                                                        |
|------------------------------------|----------------|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **InterfaceList**                  | REG\_複数\_SZ | OEM または Microsoft | HKEY で定義されているインターフェイスに対応する2つ以上のインターフェイス名のリスト。 **\_LOCAL\_MACHINE\\System\\CurrentControlSet\\コントロール\\USBFN\\インターフェイス**。 このキーは、別の設定を使用してインターフェイスをまとめて定義します。 1番目のインターフェイスは、別の設定0、2番目のインターフェイスが別の設定1などに対応します。 |
| **InterfaceNumber**                | REG\_DWORD     | OEM または Microsoft | 省略可。 この値は、関数に固定のインターフェイス番号を割り当てるために使用されます。 インターフェイス番号 0-1F はレガシ関数用に予約されており、20-3F は Microsoft 用に予約されており、40 5F (は Oem が使用するために予約されています。                                                                                                                                                 |
| **MSOSExtendedPropertyDescriptor** | REG\_バイナリ    | OEM または Microsoft | 省略可。 インターフェイスの拡張プロパティ OS 機能記述子を定義します。                                                                                                                                                                                                                                                                                    |

 

## <a name="usbfnassociations-registry-key"></a>USBFN\\Association レジストリキー


Oem は、インターフェイスの関連付け記述子 (IADs) を定義することで、関連付けを指定できます。 各 IAD では、複数のインターフェイスを1つの関数にグループ化することができます。 次の表では、 **HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\コントロール\\USBFN\\関連付け**のサブキーについて、oem が変更できる値について説明します。

各サブキーは、異なる IAD を表します。 アソシエーションを定義するには、 **HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Control\\USBFN\\association**の名前を使用して、次の表の値を設定してサブキーを作成します。

| 値                              | 種類           | 所有者            | 説明                                                                                                                                                                                                                 |
|------------------------------------|----------------|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **InterfaceList**                  | REG\_複数\_SZ | OEM または Microsoft | USB 関数に関連付けられているインターフェイスまたは代替インターフェイスの一覧。 リストのサイズが2未満の場合は、関数ドライバースタックの読み込みに失敗します。 その他の関数またはインターフェイスは引き続き読み込まれます。 |
| **bFunctionClass**                 | REG\_DWORD     | OEM または Microsoft | 関数のクラスコード。02に設定されます。                                                                                                                                                                                  |
| **bFunctionSubClass クラス**              | REG\_DWORD     | OEM または Microsoft | 0d に設定されている関数のサブクラスコード。                                                                                                                                                                               |
| **bFunctionProtocol**              | REG\_DWORD     |                  | 01に設定された関数のプロトコルコード。                                                                                                                                                                               |
| **MSOSExtendedPropertyDescriptor** | REG\_バイナリ    | OEM または Microsoft | 省略可。 インターフェイスの拡張プロパティ OS 機能記述子を定義します。                                                                                                                                             |

 

**ユースケース: MirrorLink の有効化**

MirrorLink は、モバイルデバイスと車のシステム間の統合を可能にする相互運用性の標準です。 デバイスは、MirrorLink クライアントに対して USB CDC NCM インターフェイスを公開する必要があります。 通信デバイスクラス (CDC) デバイスとして、インターフェイスの関連付け記述子 (IAD) と CDC 関数の共用体のいずれかの記述子を使用して、データインターフェイスを記述する必要があります。

Windows 10 Mobile デバイスで MirrorLink 接続を有効にするには、OEM は IAD を公開するためにこれらの変更を行う必要があります。

-   インターフェイス関連付け記述子 (IAD) を使用して、前の表に示したレジストリ値を設定することにより、通信インターフェイスとデータインターフェイスの関連付けを作成します。
-   レジストリ設定に加えて、このレジストリ値を0以外の値に設定します。

    | 値          | 種類       | 所有者            | 説明                                                                                                                     |
    |----------------|------------|------------------|---------------------------------------------------------------------------------------------------------------------------------|
    | **MirrorLink** | REG\_DWORD | OEM または Microsoft | 0以外の値は、インターフェイスが MirrorLink をサポートしていることを示します。 USB 関数スタックは、MirrorLink USB コマンドを停止しません。 |

     

-   クラス固有の記述子は、レジストリで定義されているインターフェイス記述子セットに含めることができます。 サイズフィールドは、USB 関数ドライバースタックが正確に解析できるように、これらの記述子で設定する必要があります。

また、CDC 関数の共用体記述子をクラス固有のインターフェイス記述子として定義することもできます。ただし、共用体記述子によって指定されたインターフェイス番号は静的であり、USB 関数ドライバースタックによって割り当てられることはありません。共用体記述子が存在しても、それによって記述されたインターフェイスが1つの子 PDO に関連付けられることはありません。 その関連付けには IAD が必要です。

## <a name="related-topics"></a>関連トピック
[Windows の USB デバイス側ドライバー](usb-device-side-drivers-in-windows.md)  
[USB ファンクション コントローラー用 Windows ドライバーの開発](developing-windows-drivers-for-usb-function-controllers.md)  



