---
Description: このトピックでは、WinUSB デバイスを Windows 8 で認識する方法について学びます。
title: WinUSB デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab0ae35ab57fdbea90f6b7c4a143b3c36b161cfc
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464166"
---
# <a name="winusb-device"></a>WinUSB デバイス


このトピックでは、方法について説明しますが、 *WinUSB デバイス*が Windows 8 で認識されます。

このトピックの情報は、OEM または独立系ハードウェア ベンダー (IHV) が Winusb.sys で使用される関数のドライバーとカスタム INF を提供することがなく、ドライバーを自動的にロードするデバイスを開発する場合に適用されます。

- [WinUSB デバイス](#winusb-device)
  - [WinUSB デバイスとは](#what-is-a-winusb-device)
  - [WinUSB インボックス Winusb.inf を使用してデバイスのインストール](#winusb-device-installation-by-using-the-in-box-winusbinf)
    - [USBDevice クラスの使い方。](#about-using-the-usbdevice-class)
  - [WinUSB デバイスのデバイスの説明を変更する方法](#how-to-change-the-device-description-for-a-winusb-device)
  - [WinUSB デバイスを構成する方法](#how-to-configure-a-winusb-device)
  - [関連トピック](#related-topics)

## <a name="what-is-a-winusb-device"></a>WinUSB デバイスとは


WinUSB デバイスは、ユニバーサル シリアル バス (USB) デバイスのファームウェアが特定の Microsoft オペレーティング システム (OS) 機能の記述子を"WINUSB"としてレポート互換性 ID を定義します。

WinUSB デバイスの目的は、カスタムの INF ファイルを使用せず、デバイスの機能のドライバーとして Winusb.sys を読み込む Windows を有効にするのには。 WinUSB デバイスの場合必要はありませんし、デバイスの INF ファイルを配布するのでエンドユーザーにとってドライバーのインストール プロセスを単純です。 逆に、カスタム INF を提供する必要がある場合必要がありますいない WinUSB デバイスとして、デバイスを定義して、INF でデバイスのハードウェア ID を指定します。

Microsoft では、USB デバイスのデバイス ドライバーとして Winusb.sys をインストールするために必要な情報を含む Winusb.inf を提供します。

Windows 8 では、前に関数のドライバーとして Winusb.sys の読み込みにするために必要なカスタム INF を提供します。 カスタムの INF では、デバイス固有のハードウェア ID を指定しもインボックス Winusb.inf からのセクションでは含まれています。 これらのセクションでは、サービスをインスタンス化し、受信トレイのバイナリをコピーして、デバイス インターフェイス デバイスを見つけてと対話するために必要なアプリケーションの GUID を登録するために必要です。 カスタム INF の記述については、次を参照してください。 [WinUSB (Winusb.sys) インストール](winusb-installation.md#inf)します。

Windows 8 で自動的に、INF を WinUSB デバイスと一致するように Windows を有効にするインボックス Winusb.inf ファイルが更新されました。

## <a name="winusb-device-installation-by-using-the-in-box-winusbinf"></a>WinUSB インボックス Winusb.inf を使用してデバイスのインストール


Windows 8、インボックス Winusb.inf ファイルが更新されました。 INF にはと呼ばれる、互換性のある ID を参照するインストール セクションが含まれています"USB\\MS\_COMP\_WINUSB"。

```cpp
[Generic.Section.NTamd64]
%USB\MS_COMP_WINUSB.DeviceDesc%=WINUSB,USB\MS_COMP_WINUSB 
```

更新された INF では、"USBDevice"と呼ばれる新しいセットアップ クラスも含まれています。

"USBDevice"セットアップ クラスは、Microsoft が、インボックス ドライバーを行いませんそれらのデバイスで利用可能です。 通常、このようなデバイスしないなど、オーディオ、Bluetooth、および、明確に定義された USB クラスに属しているようにし、カスタムのドライバーが必要です。 デバイスが最も高い WinUSB のデバイスの場合、デバイスが USB クラスに属していません。 そのため、"USBDevice"セットアップ クラスで、デバイスをインストールする必要があります。 更新された Winusb.inf には、その要件が容易になります。

### <a name="about-using-the-usbdevice-class"></a>USBDevice クラスの使い方。

Unclassified デバイス セットアップ クラスが、"USB"を使用しないでください。 そのクラスは、コント ローラー、ハブ、および複合デバイスをインストールするために予約されています。 "USB"クラスの不正使用については、大きな信頼性とパフォーマンスの問題につながります。 Unclassified デバイスは、"USBDevice"を使用します。

Windows 8 では、"USBDevice"デバイス クラスを使用する追加するだけでこれを INF:

```cpp
  …
  [Version] 
  Class=USBDevice 
  ClassGuid={88BAE032-5A81-49f0-BC3D-A4FF138216D6}
  …
```

デバイス マネージャーで新しいノードをわかります**ユニバーサル シリアル バスの USB デバイス**とノードの下に、デバイスが表示されます。
<p>Windows 7 で、前の行だけでなく必要があります、INF でこれらのレジストリ設定を作成します。

```cpp
  ;---------- Add Registry Section ----------
  [USBDeviceClassReg] 
  HKR,,,,"Universal Serial Bus devices"
  HKR,,NoInstallClass,,1
  HKR,,SilentInstall,,1 
  HKR,,IconPath,%REG_MULTI_SZ%,"%systemroot%\system32\setupapi.dll,-20"
```

デバイス マネージャーで、下に表示されます、デバイスにわかります**ユニバーサル シリアル バスの USB デバイス**します。 ただし、デバイス クラスの説明は、INF で指定されたレジストリ設定から派生します。

*-Eliyas Yakub、Microsoft Windows USB コア チーム*

 

"USBDevice"クラスが WinUSB に制限がないことに注意してください。 カスタム ドライバーがあるデバイスの場合は、カスタムの INF で"USBDevice"セットアップ クラスを使用できます。

デバイスの列挙中には、USB ドライバー スタックは、デバイスから互換性のある ID を読み取ります。 互換性のある ID が"WINUSB"の場合は、Windows はデバイス識別子として使用し更新のインボックス Winusb.inf で一致が検出し、デバイスの機能のドライバーとして Winusb.sys を読み込みます。

このイメージは、MUTT デバイス WinUSB デバイスとして定義されている 1 つのインターフェイスと Winusb.sys がデバイスの機能のドライバーとして読み込まれるためです。

![デバイス マネージャーが winusb デバイスを表示します。](images/winusb-device.png)

Windows 8 より前のバージョンの Windows の更新された Winusb.inf を利用**Windows Update**します。 ドライバーの更新を自動的に取得するコンピューターの構成された場合、WinUSB ドライバーが新しい INF パッケージを使用して、ユーザーの介入なしインストールを取得します。

## <a name="how-to-change-the-device-description-for-a-winusb-device"></a>WinUSB デバイスのデバイスの説明を変更する方法


WinUSB デバイスの場合は、デバイス マネージャーは、デバイスの説明として「WinUsb デバイス」を表示します。 その文字列は Winusb.inf から派生します。 WinUSB の複数のデバイスがある場合、すべてのデバイスは、同じデバイスの説明を取得します。

Windows 8 を一意に識別し、デバイス マネージャーでデバイスを区別する、デバイスによって報告されたデバイスの説明を優先するシステムに指示するデバイス クラスの新しいプロパティを提供します (でその**iProduct**文字列記述子) 経由での INF で説明します。 Windows 8 で定義されている"USBDevice"クラスは、このプロパティを設定します。 つまり、"USBDevice"クラスのデバイスがインストールされている、システムはデバイスの説明については、デバイスのクエリし、クエリの内容を取得するデバイス マネージャーの文字列を設定します。 その場合は、INF で提供されるデバイスの説明は無視されます。 デバイスの説明文字列を確認します。"MUTT"上の図。 文字列は、その製品の文字列記述子での USB デバイスによって提供されます。

Windows の以前のバージョンでは、クラスの新しいプロパティがサポートされていません。 カスタマイズされたデバイスの説明がある Windows の以前のバージョンでは、するには、独自のカスタム INF を記述する必要があります。

## <a name="how-to-configure-a-winusb-device"></a>WinUSB デバイスを構成する方法


WinUSB デバイスとしての USB デバイスを識別するためには、Microsoft OS ディスクリプターがデバイスのファームウェアにあります。 記述子の詳細については、ここで説明されている仕様を参照してください。[Microsoft OS ディスクリプター](microsoft-defined-usb-descriptors.md)します。

**記述子の拡張機能をサポートしています。**

USB ドライバー スタック、デバイスが拡張機能の記述子をサポートしていることを把握するためには、デバイスは、文字列インデックス 0 xee に格納されている OS 文字列記述子を定義する必要があります。 列挙体の中には、ドライバー スタックは、文字列記述子に照会します。 記述子が存在する場合、ドライバー スタックは、デバイスには、1 つまたは複数の OS 機能ディスクリプターとそれらの機能の記述子を取得するには、必要なデータが含まれていると仮定します。

取得した文字列記述子が、 **bMS\_VendorCode**フィールドの値。 値は、USB ドライバー スタックは、拡張機能の記述子を取得するために使用する必要がありますベンダー コードを示します。

文字列記述子、OS を定義する方法については、ここで説明されている仕様で「The OS 文字列記述子」を参照してください。[Microsoft OS ディスクリプター](microsoft-defined-usb-descriptors.md)します。

**互換性のある ID を設定**

拡張互換性 ID OS 機能のインボックス Winusb.inf を一致し、WinUSB ドライバー モジュールの読み込みに必要な記述子です。

拡張互換性 ID の OS の機能の記述子には、複合または非複合デバイスはかどうかに応じて 1 つまたは複数の関数のセクションの後にヘッダー セクションが含まれています。 ヘッダー セクションには、記述子全体、関数のセクションでは、数、およびバージョン番号の長さを指定します。 非複合デバイスでは、ヘッダー、デバイスの唯一のインターフェイスに関連付けられている 1 つの関数のセクションが続きます。 **CompatibleID**そのセクションのフィールドがフィールドの値として"WINUSB"を指定する必要があります。 複合デバイスの場合は、複数の関数のセクションがあります。 **CompatibleID**関数の各セクションのフィールドが"WINUSB"を指定する必要があります。

**デバイス インターフェイスの GUID を登録します。**

そのデバイス インターフェイスの GUID を登録するために必要な OS の拡張プロパティ機能記述子。 GUID では、アプリケーションまたはサービスからデバイスを検索、デバイスの構成、および I/O 操作を実行する必要があります。

Windows の以前のバージョンでは、GUID 登録デバイスのインターフェイスをカスタム INF を介して行います。 Windows 8 以降、デバイスは OS の拡張プロパティの機能の記述子を使用してインターフェイスの GUID をレポートする必要があります。

OS の拡張プロパティの機能の記述子には、1 つまたは複数のカスタム プロパティ セクションが続くヘッダー セクションが含まれています。 ヘッダー セクションには、その合計の長さ、バージョン番号、およびカスタム プロパティ セクションの数を含む、全体の拡張プロパティの記述子がについて説明します。 デバイス インターフェイスの GUID を登録するには、設定するカスタム プロパティ」セクションを追加、 **bPropertyName** "DeviceInterfaceGUID"フィールドと**wPropertyNameLength** 40 バイトにします。 GUID ジェネレーターを使用して、一意のデバイス インターフェイスの GUID を生成し、設定、 **bPropertyData**フィールド"{0} 8FE6D4D7-49DD-41E7-9486-49AFC6BFE475}"など、その GUID をします。 Unicode 文字列として GUID が指定された文字列の長さが 78 バイトの (null 終端文字を含む) ことに注意してください。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>bPropertyData</strong></td>
<td>78 バイト</td>
<td><p>7B 00 38 00 46 00 45 00 36 00 44 00 34 00 44 00 37 00 00 34 00 39 00 00 44 00 2D 2D 00 34 00 31 00 45 00 37 00 00 39 00 34 00 38 00 36 00 2D 2D 00 34 00 39 00 41 0046 00 43 00 36 00 42 00 46 00 45 00 34 00 37 00 35 00 7 D 00 00 00</p></td>
<td>プロパティの値は、{8FE6D4D7-49DD-41E7-9486-49AFC6BFE475 です}。</td>
</tr>
</tbody>
</table>

 

USB ドライバー スタック、デバイスの列挙中に取得し、 **DeviceInterfaceGUID** OS の拡張プロパティの機能の記述子から値と、デバイスのハードウェア キーでデバイスを登録します。 アプリケーションを使用して値を取得できる**SetupDiXxx** Api (を参照してください[ **SetupDiOpenDevRegKey**](https://msdn.microsoft.com/library/windows/hardware/ff552079))。 詳細については、次を参照してください。 [WinUSB 関数を使用して、USB デバイスへのアクセス方法](using-winusb-api-to-communicate-with-a-usb-device.md)します。

**有効化または WinUSB 電源管理機能を無効にします。**

Windows 8 では、前に、WinUSB の電源管理機能を構成する必要があるでレジストリ エントリの値を書き込む、 **HW。AddReg**のカスタムの INF セクション。

Windows 8 では、デバイスの電源設定を指定できます。 有効または WinUSB そのデバイスの機能を無効に OS の拡張プロパティの機能の記述子からの値を報告できます。 私たちを構成する 2 つの機能があります: 選択的を中断し、システムのスリープを解除します。 セレクティブ サスペンドにより、デバイスをアイドル状態のときに、低電力状態を入力します。 システム スリープ解除は、システムが低電力状態のときにシステムをスリープ解除するデバイスに機能を指します。

WinUSB の電源管理機能については、次を参照してください。 [WinUSB 電源管理](winusb-power-management.md)します。

| プロパティ名            | 説明                                                                                                                                                                                                                                                                                                                               |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| DeviceIdleEnabled        | この値があるデバイスの電源がアイドル状態のときを示す 1 に設定 (選択的な中断)。                                                                                                                                                                                                                                          |
| DefaultIdleState         | この値を示すこと、デバイスを中断できるアイドル時に既定では 1 に設定されます。                                                                                                                                                                                                                                                 |
| DefaultIdleTimeout       | この値は、デバイスがアイドル状態であると判断する前に待機するミリ秒単位の時間数を示す 5000 ミリ秒に設定されます。                                                                                                                                                                                                |
| UserSetDeviceIdleEnabled | この値は、ユーザーがコントロールを有効にまたは USB のセレクティブを無効にするデバイスの機能を中断できるようにする、1 に設定されます。 チェック ボックス**電力を節約するには、このデバイスを無効にするコンピューターを許可する**デバイスで**電源管理**プロパティ ページと、ユーザーことができますを確認または有効にまたは USB のセレクティブを無効にする ボックスの中断をオフにします。 |
| SystemWakeEnabled        | この値は、低電力状態からシステムをスリープ解除するデバイスの機能を制御するアクセス許可を 1 に設定されます。 有効にすると、**スリープを解除するには、このデバイスを許可する**デバイスの電源管理のプロパティ ページでチェック ボックスが表示されます。 ユーザーでは、確認したり、有効にまたは USB システムのスリープ解除を無効にする ボックスをオフにすることができます。         |

 

たとえば、選択的に有効にするため、デバイス上の中断、設定するカスタム プロパティ セクションを追加、 **bPropertyName**に Unicode 文字列では、"DeviceIdleEnabled"フィールドと**wPropertyNameLength** 36 バイトに。 設定、 **bPropertyData**フィールドを"0x00000001"にします。 プロパティの値は、リトル エンディアンの 32 ビット整数として格納されます。

、列挙中には、USB ドライバー スタックは機能の拡張プロパティ記述子を読み取り、このキーの下にレジストリ エントリを作成します。

**HKEY\_ローカル\_マシン**\\**システム**\\**CurrentControlSet**\\**列挙型**\\ **USB**\\***&lt;デバイス識別子&gt;***\\***&lt;インスタンス識別子&gt;***  \\**デバイス パラメーター**

このイメージは、WinUSB デバイスの設定例を示します。

![winusb デバイス用のレジストリ設定](images/winusb-device-reg.png)

その他の例で、仕様を参照してください。 [Microsoft OS ディスクリプター](microsoft-defined-usb-descriptors.md)します。

## <a name="related-topics"></a>関連トピック
[Microsoft による USB ディスクリプター](microsoft-defined-usb-descriptors.md)  



