---
Description: 複合 USB デバイスのインターフェイスは、コレクション内にグループ化できます。 USB 汎用親ドライバー (Usbccgp) では、4つの方法でインターフェイスコレクションを列挙できます。
title: USB 複合デバイス上のインターフェイス コレクション列挙の概要
ms.date: 01/07/2019
ms.assetid: aa68a774-d5b2-4fd8-aee9-9b72b1e4ad4f
ms.localizationpriority: medium
ms.openlocfilehash: 8c958afe46039535a870f6c07c37e58b303d9e85
ms.sourcegitcommit: 8084a046ca9d4c29a58b25ffcdea5d8387e9f538
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81625285"
---
# <a name="overview-of-enumeration-of-interface-collections-on-usb-composite-devices"></a>USB 複合デバイス上のインターフェイス コレクション列挙の概要


複合 USB デバイスのインターフェイスは、コレクション内にグループ化できます。 [USB 汎用親ドライバー (Usbccgp)](usb-common-class-generic-parent-driver.md)では、4つの方法でインターフェイスコレクションを列挙できます。

インターフェイスコレクションを列挙するこれらの4つのメソッドは、次のように階層構造になっています。

1.  **ベンダー提供のコールバックルーチン**

    ベンダーが、コールバックルーチンを[USB 汎用親ドライバー (Usbccgp)](usb-common-class-generic-parent-driver.md)に登録している場合は、汎用の親ドライバーがコールバックルーチンに優先され、他のメソッドを使用するのではなく、コールバックルーチンがインターフェイスをグループ化できるようになります。 ベンダー提供のコールバックルーチンを使用したインターフェイスコレクションの列挙の詳細については、「 [USB 複合デバイスでのインターフェイスコレクションの列挙](support-for-interface-collections.md)」を参照してください。

2.  **共用体の機能記述子**

    . ベンダが USB 汎用親ドライバーで CDC および WMCDC 列挙を有効にした場合、汎用の親ドライバーは*共用体の機能記述子*(ufd) を使用して、インターフェイスをコレクションにグループ化します。 このメソッドを有効にすると、ベンダーから提供されたコールバックルーチンを除き、他のすべてのメソッドよりも優先されます。 Ufd を使用したデバイスの列挙の詳細については、「 [Wireless Mobile Communications デバイスクラスのサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)」を参照してください。

3.  **インターフェイスの関連付け記述子**

    *インターフェイス関連付け記述子*(IADs) が存在する場合、USB 汎用の親ドライバーは、レガシメソッドを使用するのではなく、常に IADs を使用してインターフェイスをグループ化します。 ベンダーがインターフェイスコレクションを定義するために IADs を使用することをお勧めします。 IADs を使用したデバイスの列挙の詳細については、「[ワイヤレスモバイル通信デバイスクラスのサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)」を参照してください。

4.  **従来のオーディオメソッド。**

    USB 汎用の親ドライバーは、オーディオ機能用に予約されている従来の手法を使用して、インターフェイスコレクションを列挙できます。 デバイスに IADs がある場合、汎用の親ドライバーはこのメソッドを使用しません。 列挙の従来のオーディオメソッドの詳細については、「 [Wireless Mobile Communication Device クラスのサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)」を参照してください。

##  <a name="customizing-enumeration-of-interface-collections-for-composite-devices"></a>複合デバイスのインターフェイスコレクションの列挙のカスタマイズ


一部の USB デバイスには、USB インターフェイス関連付け記述子 (IAD) が記述できないインターフェイスコレクションがあります。 Windows Vista 以降のオペレーティングシステムでは、ベンダーは、 [USB 汎用親ドライバー (Usbccgp)](usb-common-class-generic-parent-driver.md)がデバイスのインターフェイスコレクションを定義および列挙する方法をカスタマイズできます。 これは、フィルタードライバーの*列挙コールバックルーチン*を使用して行います。 コールバックルーチンは、デバイスのカスタムインターフェイスコレクションを定義するときに、汎用の親ドライバーを支援します。

汎用の親ドライバーでカスタムインターフェイスコレクションを定義するには、複合デバイスのベンダーは次のことを行う必要があります。

1.  列挙コールバックルーチン ([**Usbc\_\_START DEVICE\_callback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbbusif/nc-usbbusif-usbc_start_device_callback)) を実装します。
2.  *USB デバイス構成インターフェイス*( [**usbc\_デバイス\_構成\_インターフェイス\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbbusif/ns-usbbusif-_usbc_device_configuration_interface_v1)の**StartDeviceCallback**メンバー) でコールバックルーチンへのポインターを指定します。
3.  複合デバイスのデバイス ID と一致する INF ファイルを指定し、USB 汎用の親ドライバーとフィルタードライバーの両方を明示的に読み込みます。

### <a name="implementation-considerations"></a>実装に関する注意点


列挙コールバックルーチンを含むフィルタードライバーは、上位または下位のフィルタードライバーのいずれかにすることができます。 USB 汎用親ドライバーが、複合デバイスを起動するための[**\_irp\_\_**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)を開始するデバイスの要求を受信すると、irp [**\_の包括的な\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)要求をドライバースタックの一番上に送信することによって、usb デバイス構成インターフェイスに対してクエリを実行します。

フィルタードライバーは、IRP\_\_\_\_\_ [**\_\_の\_全クエリインターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)要求を受信するときに、要求の**InterfaceType**メンバーの GUID 型を確認して、要求されたインターフェイスの種類が USB バスインターフェイス usbc 構成 GUID であることを確認する必要があります。 そうである場合、フィルタードライバーは、IRP の**インターフェイス**メンバー内のインターフェイスへのポインターを返します。

列挙型コールバックルーチンは、インターフェイスコレクションを記述する*関数記述子*([**usbc\_関数\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbbusif/ns-usbbusif-_usbc_function_descriptor)) の配列へのポインターを返す必要があります。 各関数記述子には、インターフェイスコレクションを記述するインターフェイス記述子 ([**\_USB インターフェイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_interface_descriptor)) の配列が含まれています。 コールバックルーチンは、非ページプールから関数記述子とインターフェイス記述子の両方を割り当てる必要があります。 このメモリは、汎用の親ドライバーによって解放されます。 コールバックルーチンは、各**USB\_インターフェイス\_記述子**の**numberofinterfaces**メンバーがインターフェイスコレクション内のインターフェイスの数を正確に報告する必要があります。

汎用の親ドライバーは、各関数記述子用に物理デバイスオブジェクト (PDO) を作成します。

USB デバイス構成インターフェイスと列挙型コールバックルーチンは、[汎用の親ドライバールーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#usbccgp)にまとめられています。

### <a name="usb-generic-parent-driver-loading-mechanism"></a>USB 汎用親ドライバーの読み込みメカニズム


複合デバイスが、「 [USB 複合デバイスの列挙](enumeration-of-the-composite-parent-device.md)」で説明されている要件を満たしている場合`USB\COMPOSITE` 、オペレーティングシステムは、デバイスが複合であることを示すために、互換性のある ID を生成します。 互換性のある ID によって、Usb .inf での一致が生成され、オペレーティングシステムは、ベンダーが提供する INF ファイルを使用せずに、自動的に USB 汎用の親ドライバーを読み込みます。

ただし、この既定の機構は、インターフェイスコレクションのカスタム列挙を必要とする複合デバイスでは機能しません。これは、既定のメカニズムでは、必要なベンダーから提供されたフィルタードライバーが読み込まれないためです。 列挙コールバックルーチン機構を機能させるには、usb 汎用親が複合デバイスのインターフェイスコレクションを列挙するときに、USB デバイス構成インターフェイスを公開するフィルタードライバーが既に読み込まれている必要があります。 複合デバイスのベンダーは、複合デバイスのデバイス ID と一致する INF ファイルをインストールし、USB 汎用の親ドライバーとフィルタードライバーの両方を明示的に読み込む必要があります。


## <a name="support-for-the-wireless-mobile-communication-device-class"></a>ワイヤレス モバイル コミュニケーション デバイス クラスのサポート


Windows Vista では、 [Usb 汎用親ドライバー (Usbccgp)](usb-common-class-generic-parent-driver.md)は、ユニバーサルシリアルバス (Usb) 通信デバイスクラス (cdc) と Usb ワイヤレスモバイル通信デバイスクラス (wmcdc) に含まれるデバイスをサポートしています。

USB ワイヤレスモバイル通信デバイスクラス (WMCDC) 仕様は、デバイスが USB ポートに接続されている場合に、ホストとワイヤレスモバイルデバイス (携帯電話など) との間の接続、制御、およびコンテンツ交換のための標準を確立します。 WMCDC は、通信デバイスクラス (CDC) の拡張機能であり、幅広い通信とネットワークデバイスが含まれています。 このセクションでは、Windows オペレーティングシステムで CDC および WMCDC デバイスをサポートするアーキテクチャについて説明します。

WMCDC デバイスは、*論理ハンドセット*にグループ化された複数の関数で構成されます。 ほとんどの WMCDC デバイスは1つの論理ハンドハンドを持っていますが、デバイスには複数の論理ハンドセットが存在する場合があります。 通常、Logical ハンドセットには、データ/fax モデム、オブジェクトストア、および呼び出し制御機能などの機能が含まれています。 論理受話器には、USB オーディオクラス仕様、USB ヒューマン入力デバイス (HID) クラス仕様、USB ビデオクラス仕様など、他の USB 仕様で定義されているサポート機能も含まれている場合があります。

Windows WMCDC アーキテクチャは、windows のネイティブドライバーを使用して、WMCDC デバイスの機能を管理します。 たとえば、Windows テレフォニーアプリケーションプログラムインターフェイス (TAPI) サブシステムを使用して、デバイスの音声およびデータ/fax モデム機能を管理したり、デバイスのイーサネット LAN 機能を管理するための Windows network driver interface specification (NDIS) サブシステムを管理したりできます。 さらに、 [winusb](winusb.md) (winusb .sys) を使用して、オブジェクト交換プロトコル (OBEX) 関数などの一部の機能をユーザーモードソフトウェアで管理することもできます。

次の図は、WMCDC デバイスのドライバースタックの例を示しています。

![デバイス構成とドライバースタックのサンプル](images/wmcdc-architecture.png)

上の図で、WMCDC デバイスには、OBEX 関数とモデム機能という1つの論理ハンドセットが含まれています。 ベンダーが提供する INF ファイルは、モデムを管理するためにネイティブ Windows ドライバーを読み込みます。 OBEX 関数は、[ユーザーモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/user-mode-driver-framework-design-guide)(UMDF) で実行されるベンダー提供のユーザーモードドライバーによって管理されます。 ユーザーモードドライバーは、Windows ポータブルデバイス (WPD) プロトコルを使用して、ユーザーアプリケーションと、 [Winusb](winusb.md)が usb スタックと通信するためにエクスポートするインターフェイスと通信します。 一般に、ベンダが提供する INF ファイルでは、Winusb .sys を使用するインターフェイスコレクションごとに Winusb の個別のインスタンスが読み込まれます。

### <a name="registry-settings"></a>レジストリの設定

USB スタックは、WMCDC を自動的にサポートしません。 Usbccgp のインスタンスを読み込む INF ファイルを指定する必要があります。 INF ファイルには**AddReg**セクションが含まれている必要があります。このセクションでは、Usbccgp に関連付けられているソフトウェア\_キーの**列挙**型のレジストリ値を、0x02、0x00、0x 00 の3つの数値から構成される REG バイナリ値に設定します。 次の例の INF ファイルからのコード例では、**列挙**値を適切な値に設定する方法を示しています。

```INF
[CCGPDriverInstall.NT]
Include=usb.inf
Needs=Composite.Dev.NT
AddReg=CCGPDriverInstall.AddReg

[CCGPDriverInstall.NT.Services]
Include=usb.inf
Needs=Composite.Dev.NT.Services

[CCGPDriverInstall.AddReg]
HKR,,EnumeratorClass, 0x00000001,02,00,00
```

**列挙型クラス**に割り当てる必要がある値は、3つの1バイトのバイナリ値から構成されます。これは、INF ファイルでは、02、00、および00のペアによって表されます。 これら3つの数値は、USB 実装者フォーラムが CDC デバイスクラス、CDC デバイスサブクラス、および CDC デバイスプロトコルに割り当てた値にそれぞれ対応しています。

WMCDC デバイスを正しく列挙するようにレジストリを構成する方法の詳細については、「[ワイヤレスモバイル通信デバイスクラスのサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)」を参照してください。

次のトピックでは、WMCDC の詳細について説明します。

### <a name="enumerating-interface-collections-on-wmcdc"></a>WMCDC でのインターフェイスコレクションの列挙


USB ワイヤレスモバイル通信デバイスクラス (WMCDC) は、USB 通信デバイスクラス (CDC) のサブクラスです。 WMCDC 仕様はを拡張しますが、インターフェイスコレクションを定義するための CDC ガイドラインを大幅に変更することはありません。 特に、WMCDC デバイスは、インターフェイスコレクションを定義するための CDC ガイドラインに準拠している必要があります。

CDC インターフェイスコレクションには、通信インターフェイスクラス (`bInterfaceClass = 0x02`) またはデータインターフェイスクラス (`bInterfaceClass = 0x0A`) に属するマスターインターフェイス ([**USB\_インターフェイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_interface_descriptor)) が含まれています。 マスターインターフェイスが通信インターフェイスクラス (一般的な状況) に属している場合、マスターインターフェイス (**bInterfaceSubClass**) のサブクラスは CDC*制御モデル*を指定します。 コントロールモデルは、インターフェイスコレクションに含まれるインターフェイスの種類を示します。 USB 実装者フォーラムで定義されているコントロールモデルの説明については、「CDC 仕様」と「WMCDC 仕様」を参照してください。

インターフェイスコレクションのマスターインターフェイスの後に、一連の必須クラス固有の機能記述子 (union 機能記述子 (UFD) を含む) が続きます。 UFD には、コレクションに属するインターフェイスの数が一覧表示されます。 UFD の**Bmasterinterface**フィールドには、マスターインターフェイスの番号が含まれています。 0個以上の**bSubordinateInterface**フィールドには、コレクション内の他の (下位の) インターフェイスの番号が含まれます。

ほとんどの種類の制御モデルでは、 [USB 汎用親ドライバー (Usbccgp)](usb-common-class-generic-parent-driver.md)によって、各 UFD 用に1つの物理デバイスオブジェクト (PDO) が作成されます。 ただし、一部のコントロールモデルには、汎用の親ドライバーが、オーディオインターフェイスが属しているインターフェイスコレクションとは別に列挙するオーディオインターフェイスが含まれています。 インターフェイスコレクションの UFD 内の下位インターフェイス (**bSubordinateInterface**) の一覧にオーディオインターフェイスが表示されますが、汎用の親ドライバーは、オーディオインターフェイス用に個別の PDO を作成します。 オーディオインターフェイスの PDO と、オーディオインターフェイスが属するインターフェイスコレクションの PDO は、どちらも、デバイスオブジェクトツリー内の親複合デバイスの機能デバイスオブジェクト (FDO) のすぐ上にあります。 オーディオインターフェイスの PDO は、インターフェイスコレクションの子ではありません。 オーディオインターフェイスの列挙につい[ては、「ワイヤレスモバイル通信デバイスクラスのサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)」で説明されています。

列挙特性がレジストリで構成可能なコントロールモデルは2つあります。ワイヤレス受話器制御モデル (WHCM) は、論理ハンドハンドを定義し、オブジェクト交換プロトコル (OBEX) コントロールモデルを定義します。 これら2つのコントロールモデルの列挙特性を構成するには、Usbccgp のインスタンスを読み込む INF ファイルを指定し、Usbccgp のインスタンスのソフトウェアキーに**CdcFlags**の値を設定する必要があります。 次の表では、 **CdcFlags**の構成オプションについて説明します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>CdcFlags ビット</th>
<th>ビットを0に設定します。</th>
<th>ビットを1に設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0 (マスク = 0x00000001)</p></td>
<td><p>USB 汎用親ドライバーは、各 OBEX インターフェイスに対して個別の PDO を作成します。</p></td>
<td><p>USB 汎用親ドライバーは、すべての OBEX インターフェイスに対して1つの PDO を作成します。</p></td>
</tr>
<tr class="even">
<td><p>1 (mask = 0x00000010)</p></td>
<td><p>USB 汎用親ドライバーは、WHCM インターフェイス (logical ハンドセット) 用の PDOs を作成しません。 これらのインターフェイスは、デバイスオブジェクトツリーの観点からは見えません。</p></td>
<td><p>USB 汎用親ドライバーは、各 WHCM インターフェイス用に PDO を作成します。</p></td>
</tr>
</tbody>
</table>

 

たとえば、両方のビットをクリアする (0 に設定する) には、INF ファイルの**AddReg**セクションに次の行が含まれている必要があります。

```INF
HKR, , CdcFlags, 0x00010001, 0x00000000
```

両方のビットを1に設定するには、INF ファイルに次の行が含まれている必要があります。

```INF
HKR, , CdcFlags, 0x00010001, 0x00000011
```

ビット0を1に、ビット1を0に設定するには、INF ファイルに次の行が含まれている必要があります。

```INF
HKR, , CdcFlags, 0x00010001, 0x00000001
```

どちらのビットも、もう一方のビットとは別に設定またはリセットできます。

次の図は、異なるレジストリ構成が同じデバイスに対して異なるデバイスツリーを作成する方法を示しています。

次の図は、 **CdcFlags**のビット0とビット1の両方が0の場合の PDO 構成を示しています。

![cdcflags = 0x00000000 のデバイスオブジェクトマッピングへのインターフェイスコレクションを示す図](images/cdcflags.png)

前の図のワイヤレス受話器制御モデル (WHCM) インターフェイスコレクションには、3つの下位インターフェイスコレクション (**bSubordinateInterface**) が含まれています。2つの OBEX コレクションとモデムコレクションです。 **CdcFlags**のビット0は0であるため、USB 汎用親ドライバーは whcm インターフェイスコレクション用の PDO を作成しません。 **CdcFlags**のビット1は0であるため、USB 汎用親ドライバーは、各 OBEX インターフェイスコレクションに対して個別の PDO を生成します。

次の図は、 **CdcFlags**のビット0とビット1の両方が設定されている場合の PDO 構成を示しています。

![cdcflags = 0x00010001 のデバイスオブジェクトマッピングへのインターフェイスコレクションを示す図](images/cdcflags-wpd.png)

ビット0の**CdcFlags**は1に設定されているため、USB 汎用親ドライバーは whcm インターフェイスコレクション用の PDO を作成します。 **CdcFlags**のビット1が1に設定されているため、USB 汎用親ドライバーは2つの obex コレクションをグループ化し、両方の obex コレクションに対して1つの PDO を生成します。

1つの PDO でカーネルレベルで OBEX コレクションを表現し、ユーザーモードドライバー内で個々の OBEX コレクションを区別することができます。 Windows ポータブルデバイス (WPD) プロトコルは、すべての OBEX 関数がカーネルレベルで1つの PDO にグループ化されている場合に、ユーザーレベルで異なる OBEX 関数間のデータストリームを多重化するのに役立ちます。

次の INF ファイルの例では、WMCDC デバイスを管理するために USB 汎用の親ドライバーを読み込み、論理ハンドセットの PDOs を作成するように USB 汎用親に指示し、論理受話器内のすべての OBEX コレクションに対して単一の PDO を作成します。

```INF
[Version]
signature="$Windows NT$"
Class=USB
ClassGUID={36FC9E60-C465-11CF-8056-444553540000}
Provider=%MSFT%
DriverVer=07/01/2001,5.1.2600.0

[ControlFlags]
ExcludeFromSelect=*

[Manufacturer]
CompanyName=CompanyName

[CompanyName]
%COMPANYNAME.DeviceDesc%=CCGPDriverInstall,USB\Vid_????&Pid_????

[CCGPDriverInstall.NT]
Include=usb.inf
Needs=Composite.Dev.NT
AddReg=CCGPDriverInstall.AddReg

[CCGPDriverInstall.NT.Services]
Include=usb.inf
Needs=Composite.Dev.NT.Services

[CCGPDriverInstall.AddReg]
HKR,,EnumeratorClass,0x00000001,02,00,00
HKR,,CdcFlags,0x00010001,0x00010001

[Strings]
MSFT="Microsoft"
COMPANYNAME.DeviceDesc="USB Phone Parent"
```
### <a name="handling-cdc-and-wmcdc-interface-collections"></a>CDC および WMCDC インターフェイスコレクションの処理


USB 汎用親ドライバーは、ワイヤレス[モバイル通信デバイスクラスのサポートに関する](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)ページで説明されているように、ワイヤレス受話器制御モデル (whcm) インターフェイスを特別な方法で処理します。

次の一覧は、CDC および WMCDC インターフェイスコレクションの処理と他のインターフェイスコレクションとの違いが最も重要な方法をまとめたものです。

-   ワイヤレスモバイル通信デバイスクラスは、限られた数のインターフェイスコレクションの入れ子を許可します。 特に、論理ハンドハンドインターフェイスコレクション (WHCM インターフェイスコレクション) には、他の下位インターフェイスコレクションを含めることができます。 たとえば、WMCDC 準拠の電話には、WHCM インターフェイスコレクションを含めることができます。このコレクションには、抽象コントロールモデルコレクションと OBEX コレクションが含まれています。
-   USB 汎用の親ドライバーで WHCM インターフェイスコレクションが列挙されないように構成することができます。 列挙されていない WHCM インターフェイスコレクションは非表示のままですが、汎用の親ドライバーは、WHCM インターフェイスコレクションに属する共用体関数記述子 (Ufd) の情報を使用して、下位インターフェイスコレクションをグループ化および列挙します。
-   OBEX コントロールモデルインターフェイスコレクション用に個別の物理デバイスオブジェクト (PDOs) を作成するか、すべての OBEX コントロールモデルインターフェイスコレクション用に1つの PDO を作成するように、USB 汎用親ドライバーを構成できます。
-   UFD 内のインターフェイス番号の一覧には、ギャップがある場合があります。 つまり、UFD のインターフェイス番号は、連続していないインターフェイスを参照できます。 この種類の番号付けは、たとえば、 [USB インターフェイスの関連付け記述子 (IAD)](usb-interface-association-descriptor.md)では有効ではなく、連続した番号を持つ必要があるインターフェイスを持つことができます。
-   Ufd には、関連するオーディオインターフェイスコレクションを含めることができます。
-   CDC および WMCDC インターフェイスコレクションのハードウェア識別子 (IDs) には、interface サブクラスが含まれている必要があります。 その他の USB インターフェイスには、インターフェイス番号\_を指定する MI% 02x suffix が含まれていますが、インターフェイスサブクラスに関する情報は含まれていません。 サブクラス情報は、ベンダーが特定のインターフェイスコレクションに対してハードウェア ID 一致を持つ INF ファイルを提供できるようにするために、ハードウェア ID に含まれています。これにより、記述子レイアウト内のインターフェイスの位置に依存せずに、コレクション用に読み込むドライバーを決定することができます。 ハードウェア ID のサブクラス情報を使用すると、ユーザーモードドライバーなどの代替手段に対して、WMCDC インターフェイスコレクションを管理する、現在のベンダー提供のドライバーからの段階的な移行パスを使用することもできます。 CDC および WMCDC ハードウェア Id の例については、「[ワイヤレスモバイル通信デバイスクラスのサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)」を参照してください。 USB インターフェイスのハードウェア Id の形式については、「 [Usb デバイスの識別子](https://docs.microsoft.com/windows-hardware/drivers/install/identifiers-for-usb-devices)」を参照してください。

### <a name="cdc-and-wmcdc-control-models"></a>CDC および WMCDC 制御モデル


CDC および WMCDC 制御モデルセクションでは、Microsoft Windows オペレーティングシステムでサポートされているインターフェイスコレクションのプロパティについて説明します。 各説明には、特に、USB 汎用親ドライバーがインターフェイスコレクションに対して生成するハードウェア id とデバイス識別子 (IDs) の一覧が含まれています。

Windows がサポートするインターフェイスコレクションのほとんどは、通信デバイスクラス (CDC) とワイヤレスモバイル通信デバイスクラス (WMCDC) に属しているコントロールモデルに対応していますが、オペレーティングシステムでは、従来のオーディオおよびビデオインターフェイスコレクションと、モバイルコンピューティング昇格コンソーシアム (MCPC) で定義されているインターフェイスコレクションもサポートしています。

このセクションで説明するインターフェイスコレクションは次のとおりです。

#### <a name="audio-class-interfaces"></a>オーディオクラスのインターフェイス


CDC デバイスと WMCDC デバイスで実行される USB オーディオデバイスクラスインターフェイスコレクションには、次のプロパティがあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>リファレンス</p></td>
<td><p><em>オーディオデバイスのユニバーサルシリアルバスデバイスクラス定義</em>、バージョン1.0。</p></td>
</tr>
<tr class="even">
<td><p>クラス</p></td>
<td><p>インターフェイスコレクション内のすべてのインターフェイスは、オーディオデバイスクラス (0x01) に属している必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>サブクラス</p></td>
<td><p>インターフェイスコレクション内の各インターフェイスには、コレクション内の最初のインターフェイスとは異なるサブクラスが必要です。</p></td>
</tr>
<tr class="even">
<td><p>Protocol</p></td>
<td><p>None (0x00)。</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>はい。</p></td>
</tr>
<tr class="even">
<td><p>関連インターフェイス</p></td>
<td><p>Streaming サブクラス (0x02) に属する0個以上の連続するインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&MI_%02x
USB\Vid_%04x&Pid_%04x&MI_%02x</code></pre>
<p>オーディオインターフェイスコレクションのハードウェア Id には、インターフェイスクラス固有の情報は含まれていません。 オーディオインターフェイスコレクションに関連付けられているハードウェア Id の書式設定の詳細については、「<a href="support-for-the-wireless-mobile-communication-device-class--wmcdc-.md" data-raw-source="[Support for the Wireless Mobile Communication Device Class](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)">ワイヤレスモバイル通信デバイスクラスのサポート</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_01&SubClass_01&Prot_00
USB\Class_01&SubClass_01
USB\Class_01</code></pre>
<p>オーディオインターフェイスコレクションの互換性のある Id の形式には、インターフェイスクラス、インターフェイスサブクラス、およびプロトコルに関する埋め込み情報が含まれています。 CDC デバイスまたは WMCDC デバイスでのオーディオインターフェイスコレクションの場合、インターフェイスクラスは01、サブクラスは01、プロトコルは00です。</p></td>
</tr>
</tbody>
</table>

#### <a name="cdc-abstract-control-model"></a>CDC 抽象制御モデル


抽象コントロールモデル (ACM) には2つのバージョンがあります。 元のバージョンは、 *USB 通信デバイスクラス*(CDC) 仕様で定義されています。 *USB ワイヤレスモバイル通信デバイスクラス*(wmcdc) 仕様には、ACM の拡張定義が含まれています。

WMCDC 仕様に準拠するインターフェイスコレクションについては[、「ワイヤレスモバイル通信デバイスクラスのサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)」で説明されています。

CDC 仕様に準拠するインターフェイスコレクションには、次のプロパティがあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>リファレンス</p></td>
<td><p>通信デバイス、バージョン1.1、セクション 3.6.2<em>のユニバーサルシリアルバスクラス定義</em>。</p></td>
</tr>
<tr class="even">
<td><p>マスターインターフェイスのクラス</p></td>
<td><p>通信インターフェイスクラス (0x02)。</p></td>
</tr>
<tr class="odd">
<td><p>Master インターフェイスのサブクラス</p></td>
<td><p>ACM (0x02)。</p></td>
</tr>
<tr class="even">
<td><p>Protocol</p></td>
<td><p>いつ.</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>はい。</p></td>
</tr>
<tr class="even">
<td><p>関連インターフェイス</p></td>
<td><p>1つのデータクラスインターフェイスと、共用体機能記述子 (UFD) で参照されるオプションのオーディオクラスインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_02&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_02
USB\Vid_%04x&Pid_%04x&Cdc_02&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_02</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_02&Prot_%02X
USB\Class_02&SubClass_02
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>UFD は、ACM インターフェイスコレクションとは別に列挙されるオーディオインターフェイスコレクションを参照できます。</p></td>
</tr>
</tbody>
</table>

#### <a name="cdc-atm-networking-control-model"></a>CDC ATM ネットワーク制御モデル


USB CDC ATM ネットワーク制御モデル (arm m) インターフェイスコレクションには、次のプロパティがあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>リファレンス</p></td>
<td><p>通信デバイス、バージョン1.1、セクション 3.8.3<em>のユニバーサルシリアルバスクラス定義</em></p></td>
</tr>
<tr class="even">
<td><p>マスターインターフェイスのクラス</p></td>
<td><p>Communication Interface クラス (0x02)</p></td>
</tr>
<tr class="odd">
<td><p>Master インターフェイスのサブクラス</p></td>
<td><p>0x07</p></td>
</tr>
<tr class="even">
<td><p>Protocol</p></td>
<td><p>なし (0x00)</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>関連インターフェイス</p></td>
<td><p>共用体機能記述子 (UFD) によって参照される1つのデータクラスインターフェイス</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_07&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_07
USB\Vid_%04x&Pid_%04x&Cdc_07&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_07</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_07&Prot_00
USB\Class_02&SubClass_07
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>


#### <a name="cdc-capi-control-model"></a>CDC CAPI 制御モデル


USB CDC Common ISDN API (CAPI) コントロールモデルインターフェイスコレクションには、次のプロパティがあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>リファレンス</p></td>
<td><p><em></em></p>
<p>通信デバイス、バージョン1.1、セクション 3.7.2<em>のユニバーサルシリアルバスクラス定義</em></p></td>
</tr>
<tr class="even">
<td><p>マスターインターフェイスのクラス</p></td>
<td><p>Communication Interface クラス (0x02)</p></td>
</tr>
<tr class="odd">
<td><p>Master インターフェイスのサブクラス</p></td>
<td><p>CAPI (0x05)</p></td>
</tr>
<tr class="even">
<td><p>Protocol</p></td>
<td><p>なし (0x00)</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>関連インターフェイス</p></td>
<td><p>共用体機能記述子 (UFD) が参照する1つのデータクラスインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_05&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_05</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_05&Prot_00
USB\Class_02&SubClass_05</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>

#### <a name="cdc-direct-line-control-model"></a>CDC の直接直線制御モデル


USB CDC Direct Line Control Model (DLCM) インターフェイスコレクションには、次のプロパティがあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>リファレンス</p></td>
<td><p>通信デバイス、バージョン1.1、セクション 3.6.1<em>のユニバーサルシリアルバスクラス定義</em>。</p></td>
</tr>
<tr class="even">
<td><p>マスターインターフェイスのクラス</p></td>
<td><p>通信インターフェイスクラス (0x02)。</p></td>
</tr>
<tr class="odd">
<td><p>Master インターフェイスのサブクラス</p></td>
<td><p>DLCM (0x01)。</p></td>
</tr>
<tr class="even">
<td><p>Protocol</p></td>
<td><p>None (0x00)。</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>はい。</p></td>
</tr>
<tr class="even">
<td><p>関連インターフェイス</p></td>
<td><p>共用体機能記述子 (UFD) が参照するオーディオクラスまたはベンダー定義のインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_01&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_01
USB\Vid_%04x&Pid_%04x&Cdc_01&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_01</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_01&Prot_00
USB\Class_02&SubClass_01
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>UFD は、DLCM インターフェイスコレクションとは別に列挙されるオーディオクラスインターフェイスコレクションを参照します。</p></td>
</tr>
</tbody>
</table>

#### <a name="cdc-ethernet-networking-control-model"></a>CDC イーサネットネットワーク制御モデル


USB CDC イーサネットネットワーク制御モデル (ENCM) インターフェイスコレクションには、次のプロパティがあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>リファレンス</p></td>
<td><p>通信デバイス、バージョン1.1、セクション 3.8.2<em>のユニバーサルシリアルバスクラス定義</em>。</p></td>
</tr>
<tr class="even">
<td><p>マスターインターフェイスのクラス</p></td>
<td><p>通信インターフェイスクラス (0x02)。</p></td>
</tr>
<tr class="odd">
<td><p>Master インターフェイスのサブクラス</p></td>
<td><p>ENCM (0x06)。</p></td>
</tr>
<tr class="even">
<td><p>Protocol</p></td>
<td><p>None (0x00)。</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>はい。</p></td>
</tr>
<tr class="even">
<td><p>関連インターフェイス</p></td>
<td><p>共用体機能記述子 (UFD) が参照する1つのデータクラスインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_06&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_06
USB\Vid_%04x&Pid_%04x&Cdc_06&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_06</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_06&Prot_00
USB\Class_02&SubClass_06
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>このコントロールモデルの互換性のある Id は、Microsoft が提供する INF ファイルと一致しています。 製造元から提供されている INF ファイルでハードウェア Id の1つに一致するものが見つからない場合、システムはネイティブ NDIS ミニポートドライバーを自動的に読み込み、インターフェイスコレクションを管理します。</p></td>
</tr>
</tbody>
</table>

#### <a name="cdc-multi-channel-isdn-control-model"></a>CDC マルチチャネルの ISDN 制御モデル


USB CDC マルチチャネル ISDN 制御モデル (MCCM) インターフェイスコレクションには、次のプロパティがあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>リファレンス</p></td>
<td><p>通信デバイス、バージョン1.1、セクション 3.7.1<em>のユニバーサルシリアルバスクラス定義</em></p></td>
</tr>
<tr class="even">
<td><p>マスターインターフェイスのクラス</p></td>
<td><p>Communication Interface クラス (0x02)</p></td>
</tr>
<tr class="odd">
<td><p>Master インターフェイスのサブクラス</p></td>
<td><p>MCCM (0x04)</p></td>
</tr>
<tr class="even">
<td><p>Protocol</p></td>
<td><p>なし (0x00)</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>関連インターフェイス</p></td>
<td><p>共用体機能記述子 (UFD) が参照する複数のデータクラスインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_04&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_04
USB\Vid_%04x&Pid_%04x&Cdc_04&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_04</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_04&Prot_00
USB\Class_02&SubClass_04
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>

 
#### <a name="cdc-telephone-control-model"></a>CDC の電話制御モデル


USB CDC の電話制御モデル (TCM) インターフェイスコレクションには、次のプロパティがあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>リファレンス</p></td>
<td><p>通信デバイス、バージョン1.1、セクション 3.6.3<em>のユニバーサルシリアルバスクラス定義</em>。</p></td>
</tr>
<tr class="even">
<td><p>マスターインターフェイスのクラス</p></td>
<td><p>通信インターフェイスクラス (0x02)。</p></td>
</tr>
<tr class="odd">
<td><p>Master インターフェイスのサブクラス</p></td>
<td><p>TCM (0x03)。</p></td>
</tr>
<tr class="even">
<td><p>Protocol</p></td>
<td><p>いつ.</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>はい。</p></td>
</tr>
<tr class="even">
<td><p>関連インターフェイス</p></td>
<td><p>共用体機能記述子 (UFD) が参照するオーディオクラスインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>Hardware ID (ハードウェア ID)</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_03&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_03
USB\Vid_%04x&Pid_%04x&Cdc_03&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_03</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 ID</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_03&Prot_%02X
USB\Class_02&SubClass_03
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>UFD は、TCM インターフェイスコレクションとは別に列挙されるオーディオクラスインターフェイスコレクションを参照できます。</p></td>
</tr>
</tbody>
</table>

#### <a name="mcpc-vendor-unique-interfaces"></a>MCPC ベンダー-固有のインターフェイス


モバイルコンピューティングプロモーションコンソーシアム (MCPC) は、ワイヤレスモバイル通信デバイスクラス (WMCDC) 仕様がベンダー固有の CDC デバイスの形式を提供する前に、インターフェイスコレクションの形式を定義しました。 そのため、MCPC インターフェイスコレクションは WMCDC 標準に準拠していません。

ただし、WMCDC が有効になっている場合は、USB 汎用親ドライバーが MCPC インターフェイスコレクションを列挙できます。 MCPC インターフェイスコレクションには、次のプロパティがあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>リファレンス</p></td>
<td><p>モバイルコンピューティングプロモーションコンソーシアム (MCPC) 004 仕様</p></td>
</tr>
<tr class="even">
<td><p>クラス</p></td>
<td><p>CDC (0x02)</p></td>
</tr>
<tr class="odd">
<td><p>サブクラス</p></td>
<td><p>0x88</p></td>
</tr>
<tr class="even">
<td><p>Protocol</p></td>
<td><p>なし (0x00)</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>関連インターフェイス</p></td>
<td><p>共用体機能記述子 (UFD) で参照される0個以上のデータクラスインターフェイス</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_88&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_88
USB\Vid_%04x&Pid_%04x&Cdc_88&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_88</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_88&Prot_00
USB\Class_02&SubClass_88
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>

#### <a name="video-class-interfaces"></a>ビデオクラスインターフェイス


CDC デバイスと WMCDC デバイスで実行される USB ビデオデバイスクラスインターフェイスコレクションには、次のプロパティがあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>リファレンス</p></td>
<td><p><em>ビデオデバイスのユニバーサルシリアルバスデバイスクラスの定義</em>バージョン1.0。</p></td>
</tr>
<tr class="even">
<td><p>クラス</p></td>
<td><p>ビデオ (0x0E)。</p></td>
</tr>
<tr class="odd">
<td><p>サブクラス</p></td>
<td><p>ビデオコントロール (0x01)。</p></td>
</tr>
<tr class="even">
<td><p>Protocol</p></td>
<td><p>None (0x00)。</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>はい。</p></td>
</tr>
<tr class="even">
<td><p>関連インターフェイス</p></td>
<td><p>Streaming サブクラス (0x02) に属する0個以上の連続するインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&MI_%02x
USB\Vid_%04x&Pid_%04x&MI_%02x</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_0E&SubClass_01&Prot_00
USB\Class_0E&SubClass_01
USB\Class_0E</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>Video クラスのインターフェイスコレクションは、CDC デバイスで特別な処理を受けます。 非 CDC デバイスでは、ビデオクラスインターフェイスコレクションはインターフェイスの関連付け記述子 (IADs) によって定義されます。 CDC デバイスでは、ビデオクラスのインターフェイスコレクションは、共用体の機能記述子 (Ufd) によって定義されます。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-abstract-control-model"></a>WMCDC 抽象コントロールモデル


抽象コントロールモデル (ACM) には2つのバージョンがあります。 元のバージョンは、USB 通信デバイスクラス (CDC) 仕様で定義されています。 USB ワイヤレスモバイル通信デバイスクラス (WMCDC) 仕様には、ACM の拡張定義が含まれています。 Fax/モデム関数を含む ACM コレクションでは、元の CDC ACM 定義ではなく、ACM の WMCDC 定義を使用する必要があります。

CDC 仕様に準拠するインターフェイスコレクションについては[、「ワイヤレスモバイル通信デバイスクラスのサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)」で説明されています。

WMCDC 仕様に準拠するインターフェイスコレクションには、次のプロパティがあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>リファレンス</p></td>
<td><p><em>ワイヤレスモバイル通信デバイスの場合は、ユニバーサルシリアルバス CDC サブクラス仕様</em>、バージョン1.0、セクション6.2。</p></td>
</tr>
<tr class="even">
<td><p>マスターインターフェイスのクラス</p></td>
<td><p>通信インターフェイスクラス (0x02)。</p></td>
</tr>
<tr class="odd">
<td><p>Master インターフェイスのサブクラス</p></td>
<td><p>ACM (0x02)。</p></td>
</tr>
<tr class="even">
<td><p>Protocol</p></td>
<td><p>コレクションで AT コマンドセットプロトコルが使用されている場合、互換性 Id に埋め込まれているプロトコル値は0x01 になります。 コレクションが、WMCDC 仕様に記述されているプロトコルのいずれかを使用している場合、互換性のある Id に埋め込まれているプロトコル値は 0x2 ~ 0x06 (0xFE) になります。</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>はい。</p></td>
</tr>
<tr class="even">
<td><p>関連インターフェイス</p></td>
<td><p>共用体機能記述子 (UFD) が参照する1つのデータクラスインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_Modem&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_Modem
USB\Vid_%04x&Pid_%04x&Cdc_Modem&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_Modem</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_Modem&Prot_%02X
USB\Class_02&SubClass_Modem
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>UFD は、ACM インターフェイスコレクションとは別に列挙されるオーディオインターフェイスコレクションを参照する場合があります。</p>
<p>インターフェイスコレクションは、WMCDC 仕様のセクション6.2 で指定されている特殊な記述子およびエンドポイントの要件に従っている必要があります。 インターフェイスコレクションが WMCDC 要件に準拠していないが、インターフェイスが CDC 要件に準拠している場合、USB 汎用親ドライバーは、「<a href="support-for-the-wireless-mobile-communication-device-class--wmcdc-.md" data-raw-source="[Support for the Wireless Mobile Communication Device Class](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)">ワイヤレスモバイル通信デバイスクラスのサポート</a>」で説明されているように、cdc 形式でインターフェイスコレクションと汎用ハードウェア id を列挙します。</p>
<p>このコントロールモデルの互換性のある Id は、Microsoft が提供する INF ファイルと一致しています。 製造元から提供されている INF ファイルでハードウェア Id の1つに一致するものが見つからない場合、システムはネイティブテレフォニーアプリケーションプログラミングインターフェイス (TAPI) モデムフィルタードライバーを自動的に読み込み、モデムの機能を管理し、プロトコルコードが0xFE でない限り、適切な TAPI レジストリ設定を設定します。 プロトコルコードが0xFE の場合、ベンダーは、TAPI レジストリ設定を正しく設定するために、デバイスまたはクラスの共同インストーラーを提供する必要があります。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-device-management-model"></a>WMCDC デバイス管理モデル


USB WMCDC デバイス管理モデル (DMM) インターフェイスコレクションには、次のプロパティがあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>リファレンス</p></td>
<td><p><em>ワイヤレスモバイル通信デバイスの場合は、ユニバーサルシリアルバス CDC サブクラス仕様</em>、バージョン1.0、セクション6.6。</p></td>
</tr>
<tr class="even">
<td><p>マスターインターフェイスのクラス</p></td>
<td><p>通信インターフェイスクラス (0x02)。</p></td>
</tr>
<tr class="odd">
<td><p>Master インターフェイスのサブクラス</p></td>
<td><p>DMM (0x09)。</p></td>
</tr>
<tr class="even">
<td><p>Protocol</p></td>
<td><p>いつ.</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>はい。</p></td>
</tr>
<tr class="even">
<td><p>関連インターフェイス</p></td>
<td><p>[なし] :</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_09&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_09
USB\Vid_%04x&Pid_%04x&Cdc_09&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_09</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_09&Prot_%02X
USB\Class_02&SubClass_09
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>この制御モデルは、共用体の機能記述子 (UFD) を使用しません。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-mobile-direct-line-model"></a>WMCDC モバイルダイレクトラインモデル


USB WMCDC モバイル Direct Line Model (MDLM) インターフェイスコレクションには、次のプロパティがあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>リファレンス</p></td>
<td><p><em>ワイヤレスモバイル通信デバイスのユニバーサルシリアルバス CDC サブクラス仕様</em>(バージョン1.0、セクション 6.7)</p></td>
</tr>
<tr class="even">
<td><p>マスターインターフェイスのクラス</p></td>
<td><p>Communication Interface クラス (0x02)</p></td>
</tr>
<tr class="odd">
<td><p>Master インターフェイスのサブクラス</p></td>
<td><p>MDLM (0x0A)</p></td>
</tr>
<tr class="even">
<td><p>Protocol</p></td>
<td><p>Any</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>関連インターフェイス</p></td>
<td><p>共用体機能記述子 (UFD) で参照される1つ以上のデータクラスインターフェイス</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_0A&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_0A
USB\Vid_%04x&Pid_%04x&Cdc_0A&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_0A</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_0A&Prot_%02X
USB\Class_02&SubClass_0A
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>[なし] :</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-obex-control-model-multiple-pdos"></a>WMCDC OBEX 制御モデル (複数の PDOs)


オブジェクト交換プロトコル (OBEX) コントロールモデルのコレクションを列挙するには、2つの方法があります。 USB 汎用親ドライバーは、すべての OBEX インターフェイスをグループ化し、すべての OBEX インターフェイスに対して1つの物理デバイスオブジェクト (PDO) を作成できます。また、親ドライバーは、各 OBEX インターフェイスに個別の PDO を作成できます。 グループにまとめられている OBEX インターフェイスに対して USB 汎用親ドライバーが生成するハードウェア Id の説明については、「[ワイヤレスモバイル通信デバイスクラスのサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)」を参照してください。

USB 汎用親ドライバーによって各 OBEX インターフェイスに個別の PDOs が割り当てられると、PDOs には次のプロパティがあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>リファレンス</p></td>
<td><p><em>ワイヤレスモバイル通信デバイスの場合は、ユニバーサルシリアルバス CDC サブクラス仕様</em>、バージョン1.0、セクション6.5。</p></td>
</tr>
<tr class="even">
<td><p>マスターインターフェイスのクラス</p></td>
<td><p>通信インターフェイスクラス (0x02)。</p></td>
</tr>
<tr class="odd">
<td><p>Master インターフェイスのサブクラス</p></td>
<td><p>OBEX (0x0B)。</p></td>
</tr>
<tr class="even">
<td><p>Protocol</p></td>
<td><p>None (0x00)。</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>はい。</p></td>
</tr>
<tr class="even">
<td><p>関連インターフェイス</p></td>
<td><p>共用体機能記述子 (UFD) が参照する1つのデータクラスインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_0B&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_0B
USB\Vid_%04x&Pid_%04x&Cdc_0B&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_0B</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_0B&Prot_00
USB\Class_02&SubClass_0B
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>複合デバイスを管理する USB 汎用親ドライバーのインスタンスに関連付けられているレジストリ設定により、OBEX インターフェイスを1つの PDO または複数の PDOs で管理するかどうかが決まります。 USB 汎用親ドライバーが OBEX インターフェイスを列挙する方法を指定するレジストリ設定の詳細については、「<a href="support-for-the-wireless-mobile-communication-device-class--wmcdc-.md" data-raw-source="[Support for the Wireless Mobile Communication Device Class](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)">ワイヤレスモバイル通信デバイスクラスのサポート</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-obex-control-model-single-pdo"></a>WMCDC OBEX 制御モデル (単一 PDO)


オブジェクト交換プロトコル (OBEX) コントロールモデルのコレクションを列挙するには、2つの方法があります。 USB 汎用親ドライバーは、すべての OBEX インターフェイスをグループ化し、すべての OBEX インターフェイスに対して1つの物理デバイスオブジェクト (PDO) を作成できます。また、親ドライバーは、各 OBEX インターフェイスに個別の PDO を作成できます。 個別に列挙される OBEX インターフェイスに対して USB 汎用親ドライバーが生成するハードウェア Id の説明については、「[ワイヤレスモバイル通信デバイスクラスのサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)」を参照してください。

USB 汎用親ドライバーが1つの PDO をすべての OBEX インターフェイスに割り当てると、PDO には次のプロパティがあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>リファレンス</p></td>
<td><p><em>ワイヤレスモバイル通信デバイスの場合は、ユニバーサルシリアルバス CDC サブクラス仕様</em>、バージョン1.0、セクション6.5。</p></td>
</tr>
<tr class="even">
<td><p>マスターインターフェイスのクラス</p></td>
<td><p>通信インターフェイスクラス (0x02)。</p></td>
</tr>
<tr class="odd">
<td><p>Master インターフェイスのサブクラス</p></td>
<td><p>OBEX (0x0B)。</p></td>
</tr>
<tr class="even">
<td><p>Protocol</p></td>
<td><p>None (0x00)。</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>はい。</p></td>
</tr>
<tr class="even">
<td><p>関連インターフェイス</p></td>
<td><p>共用体機能記述子 (UFD) が参照する1つのデータクラスインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&WPD_OBEX&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&WPD_OBEX
USB\Vid_%04x&Pid_%04x&WPD_OBEX&MI_%02x
USB\Vid_%04x&Pid_%04x&WPD_OBEX</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&WPD_OBEX
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>複合デバイスを管理する USB 汎用親ドライバーのインスタンスに関連付けられているレジストリ設定により、OBEX インターフェイスを1つの PDO または複数の PDOs で管理するかどうかが決まります。 USB 汎用親ドライバーが OBEX インターフェイスを列挙する方法を指定するレジストリ設定の詳細については、「 <a href="support-for-interface-collections.md" data-raw-source="[Enumeration of Interface Collections on USB Composite Devices](support-for-interface-collections.md)">Usb 複合デバイスでのインターフェイスコレクションの列挙</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-wireless-handset-control-model"></a>WMCDC ワイヤレスハンドハンド制御モデル


USB 汎用の親ドライバーは、常にワイヤレス受話器制御モデル (WHCM) インターフェイスコレクションを列挙するわけではありません。 WHCM インターフェイスコレクションを管理する USB 汎用親ドライバーのインスタンスに関連付けられているレジストリ設定によって、USB 汎用親ドライバーがインターフェイスコレクション用に物理デバイスオブジェクト (PDO) を作成するかどうかが決定されます。 USB 汎用親ドライバーが WHCM インターフェイスを列挙する方法を指定するレジストリ設定の詳細については、「 [Usb 複合デバイスでのインターフェイスコレクションの列挙](support-for-interface-collections.md)」を参照してください。

列挙型 WHCM インターフェイスコレクションには、次のプロパティがあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>リファレンス</p></td>
<td><p><em>ワイヤレスモバイル通信デバイスの場合は、ユニバーサルシリアルバス CDC サブクラス仕様</em>、バージョン1.0、セクション6.1。</p></td>
</tr>
<tr class="even">
<td><p>マスターインターフェイスのクラス</p></td>
<td><p>通信インターフェイスクラス (0x02)。</p></td>
</tr>
<tr class="odd">
<td><p>Master インターフェイスのサブクラス</p></td>
<td><p>WHCM (0x08)。</p></td>
</tr>
<tr class="even">
<td><p>Protocol</p></td>
<td><p>None (0x00)。</p></td>
</tr>
<tr class="odd">
<td><p>Enumerated</p></td>
<td><p>はい。</p></td>
</tr>
<tr class="even">
<td><p>関連インターフェイス</p></td>
<td><p>[なし] :</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_08&MI_%02x
USB\Vid_%04x&Pid_%04x&Rev_%04x&Cdc_08
USB\Vid_%04x&Pid_%04x&Cdc_08&MI_%02x
USB\Vid_%04x&Pid_%04x&Cdc_08</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&SubClass_08&Prot_00
USB\Class_02&SubClass_08
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>共用体機能記述子 (UFD) は、論理ハンドセットに関連付けられているインターフェイスを識別します。</p></td>
</tr>
</tbody>
</table>

前のトピックで説明したハードウェア ID 形式では、次の規則を使用します。

- C 言語の**printf**形式は、整数を表します。 たとえば、"% 04x" は4桁の16進整数を意味し、"% 02x" は2桁の16進数整数を意味します。

- 文字列 "Vid\_" の後の整数は、USB 委員会 (www.usb.org) が仕入先に割り当てるベンダーコードの4桁の16進数表現です。

- 文字列 "Pid\_" の後の整数は、ベンダーからデバイスに割り当てられた製品コードの4桁の16進数表現です。

- 文字列 "Rev\_" の後の整数は、デバイスのリビジョン番号を表す4桁の16進数表記です。

- 文字列 "Cdc\_" の後の整数は、interface サブクラスです。

- 文字列 "Prot.13\_" の後の整数は、プロトコル番号です。

- 文字列 "MI\_" の後の整数は、インターフェイスの記述子の**bInterfaceNumber**フィールドから抽出された、インターフェイス番号の2桁の16進数表現です。


### <a name="enumeration-of-interface-collections-on-usb-devices-with-iads"></a>IADs を使用した USB デバイスでのインターフェイスコレクションの列挙


USB 複合デバイスのファームウェアにインターフェイスの関連付け記述子 (IAD) がある場合、Windows は、各コレクションが1つのデバイスであるかのようにインターフェイスコレクションを列挙し、各インターフェイスコレクションに1つの物理デバイスオブジェクト (PDO) を割り当て、ハードウェアと互換性のある識別子 (IDs) を PDO に関連付けます。 IADs の詳細については、「 [USB インターフェイスの関連付け記述子](usb-interface-association-descriptor.md)」を参照してください。 ここでは、IAD に関連付けられているインターフェイスコレクションに割り当てられたハードウェア Id と互換性のある識別子 (IDs) について説明します。

##  <a name="hardware-ids"></a>ハードウェア Id


`USB\VID_v(4)&PID_p(4)&Rev_r(4)&MI_z(2)`

`USB\VID_v(4)&PID_p(4)&MI_z(2)`

これらのハードウェア Id では、

-   *v (4)* は、USB 委員会によってベンダーに割り当てられ、デバイス記述子の**idvendor**フィールドから抽出される4桁のベンダーコードです。
-   *p (4)* は、ベンダーによってデバイスに割り当てられ、デバイス記述子の**idproduct**フィールドから抽出される4桁の製品コードです。
-   *r (4)* は、ベンダーによってデバイスに割り当てられ、デバイス記述子の**bcddevice**フィールドから抽出された、4桁のデバイスのリリース番号です (バイナリでコード化された10進リビジョン)。
-   *z (2)* は、iad の**bfirstinterface**フィールドから抽出された2桁のインターフェイス番号です。

#### <a name="compatible-ids"></a>互換性 Id


`USB\Class_c(2)&SubClass_s(2)&Prot_p(2)`

`USB\Class_c(2)&SubClass_s(2)`

`USB\Class_c(2)`

これらの互換性のある Id では、c (2)、s (2)、および p (2) は、IAD の**Bfunctionclass**、 **bfunctionclass クラス**、および**bfunctionclass**の各フィールドからそれぞれ取得される値を格納します。

IADs を再帰的に使用して関数の関数をバインドすることはできません。 特に、デバイスのファームウェアに IAD 記述子がある場合、汎用の親ドライバーは、「 [USB 複合デバイスでのインターフェイスコレクションの列挙](support-for-interface-collections.md)」で説明されているように、オーディオデバイスクラスによってインターフェイスをグループ化しません。

### <a name="enumeration-of-interface-collections-on-audio-devices-without-iads"></a>IADs を使用しないオーディオデバイスでのインターフェイスコレクションの列挙


オーディオデバイスの場合、Windows オペレーティングシステムは、関数に関連付けられたインターフェイスのグループ (インターフェイスコレクション) を列挙し、デバイスにインターフェイス関連付け記述子 (IAD) がない場合でも、各グループに1つの物理デバイスオブジェクト (PDO) を割り当てることができます。

インターフェイスが次の条件を満たしている場合、オペレーティングシステムは複合オーディオデバイスのインターフェイスをインターフェイスコレクションにグループ化します。

-   インターフェイスコレクション内のすべてのインターフェイスは、連続している必要があります。 つまり、ファームウェアメモリ内でインターフェイスが相互に隣接している必要があります。
-   インターフェイスコレクション内のすべてのインターフェイスは、オーディオデバイスクラスに属している必要があります。 デバイスの製造元は、インターフェイス記述子の**bInterfaceClass**フィールドに0x01 の値を割り当てることによって、インターフェイスがオーディオデバイスクラスに属していることを指定します。
-   インターフェイスコレクション内の各インターフェイスには、コレクション内の最初のインターフェイスとは異なるサブクラスが必要です。インターフェイス記述子の**bInterfaceSubClass**フィールドは、インターフェイスの device サブクラスを指定します。

インターフェイスがこれら3つの条件のすべてを満たしていない場合、Windows は他のオーディオクラスインターフェイスを使用してグループ化するのではなく、個別に列挙しようとします。

インターフェイスの関連付け記述子 (IAD) がデバイスのファームウェアに存在する場合、オペレーティングシステムはオーディオクラスインターフェイスを特別な方法でグループ化しません。 IAD メソッドは、常に、USB インターフェイスをグループ化するための推奨される方法です。

このセクションでは、オーディオデバイスクラスに属するインターフェイスを持つインターフェイスコレクション用にオペレーティングシステムによって作成される PDO に関連付けられている、ハードウェアおよび互換性のある識別子 (IDs) について説明します。

#### <a name="hardware-ids"></a>ハードウェア Id


`USB\VID_v(4)&PID_p(4)&Rev_r(4)&MI_z(2)`

`USB\VID_v(4)&PID_p(4)&MI_z(2)`

これらのハードウェア Id では、

-   *v (4)* は、USB 標準委員会がベンダーに割り当て、デバイス記述子の**idvendor**フィールドから抽出された4桁のベンダーコードです。
-   *p (4)* は、ベンダーによってデバイスに割り当てられ、デバイス記述子の**idproduct**フィールドから抽出される4桁の製品コードです。
-   *r (4)* は、ベンダーによってデバイスに割り当てられ、デバイス記述子の**bcddevice**フィールドから抽出された、4桁のデバイスのリリース番号です (バイナリでコード化された10進リビジョン)。
-   *z (2)* は、インターフェイス記述子の**bInterfaceNumber**フィールドから抽出された2桁のインターフェイス番号です。

##### <a name="compatible-ids"></a>互換性 Id

`USB\Class_c(2)&SubClass_s(2)&Prot_p(2)`

`USB\Class_c(2)&SubClass_s(2)`

`USB\Class_c(2)`

これらの互換性のある Id では、c (2)、s (2)、および p (2) には、各インターフェイスコレクション内の最初の USB インターフェイス記述子の bInterfaceClass、bInterfaceSubClass、および bInterfaceProtocol の各フィールドからそれぞれ取得される値が含まれます。

## <a name="related-topics"></a>関連トピック
[USB 汎用親ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)  
[Microsoft が提供する USB ドライバー](system-supplied-usb-drivers.md)  



