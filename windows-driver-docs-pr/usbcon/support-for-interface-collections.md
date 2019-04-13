---
Description: 複合 USB デバイス上のインターフェイスは、コレクションにグループ化できます。 USB の一般的な親ドライバー (Usbccgp.sys) は、次の 4 つの方法でインターフェイスのコレクションを列挙できます。
title: USB 複合デバイス上のインターフェイス コレクションの列挙
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 912d9a75ae21c48fc47ddf1a8c5d7a46527974b2
ms.sourcegitcommit: 4c67665bf7cd4fd3599ff0751a3b0427d119937c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2019
ms.locfileid: "59554076"
---
# <a name="enumeration-of-interface-collections-on-usb-composite-devices"></a>USB 複合デバイス上のインターフェイス コレクションの列挙


複合 USB デバイス上のインターフェイスは、コレクションにグループ化できます。 [USB 汎用親ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md) 4 つの方法でインターフェイスのコレクションを列挙できます。

これら 4 つのインターフェイスのコレクションの列挙体のメソッドは、次のように階層的に分類されます。

1.  **ベンダーから提供されたコールバック ルーチン**

    仕入先がコールバック ルーチンに登録されている場合、 [USB 汎用親ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)、コールバック ルーチンに優先順位できグループ インターフェイスにコールバック ルーチンことができます、一般的な親ドライバーなく他の方法を使用します。 ベンダーから提供されたコールバック ルーチンを使用してインターフェイスのコレクションの列挙体の詳細については、次を参照してください。[複合デバイスを USB でインターフェイス コレクションの列挙体](support-for-interface-collections.md)します。

2.  **Union 関数型記述子**

    . 一般的な親ドライバーを使用して仕入先がジェネリックの親の USB ドライバーで CDC と WMCDC の列挙を有効な場合*共用体の機能の記述子*(Ufd) コレクションにグループのインターフェイスにします。 有効な場合、このメソッドは、ベンダーから提供されたコールバック ルーチンを除けば、他のすべてのメソッドに優先します。 Ufd デバイスの列挙体の詳細については、次を参照してください。[ワイヤレス モバイル通信デバイス クラスに対するサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)します。

3.  **インターフェイスの関連付けの記述子**

    場合*インターフェイスの関連付け記述子*(Iad) が存在する、一般的な親の USB ドライバーは、従来の方法ではなく、Iad を使用して、常にインターフェイスをグループします。 ベンダーが、インターフェイスのコレクションを定義する Iad を使用することをお勧めします。 Iad でのデバイス列挙の詳細については、次を参照してください。[ワイヤレス モバイル通信デバイス クラスに対するサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)します。

4.  **従来のオーディオ メソッド。**

    一般的な親の USB ドライバーでは、オーディオ機能用に予約されている従来の手法を使用して、インターフェイスのコレクションを列挙できます。 一般的な親ドライバーでは、デバイスで、Iad がある場合、このメソッドは使用しません。 列挙体のオーディオの従来の方法の詳細については、次を参照してください。[ワイヤレス モバイル通信デバイス クラスに対するサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)します。

##  <a name="customizing-enumeration-of-interface-collections-for-composite-devices"></a>複合デバイス用のインターフェイスのコレクションの列挙をカスタマイズします。


一部の USB デバイスでは、USB インターフェイスの関連付け記述子 (IAD) は、説明がインターフェイスのコレクションがあります。 Windows Vista およびそれ以降のオペレーティング システムでは、ベンダーが方法をカスタマイズできます、 [USB 汎用親ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)を定義し、デバイスのインターフェイスのコレクションを列挙します。 これを行う、*列挙コールバック ルーチン*フィルター ドライバー。 コールバック ルーチンは、デバイスのカスタム インターフェイスのコレクションを定義する一般的な親ドライバーを支援します。

カスタム インターフェイスのコレクションを定義する一般的な親ドライバーの場合、複合デバイスのベンダー必要があります。

1.  列挙体のコールバック ルーチンを実装 ([**USBC\_開始\_デバイス\_コールバック**](https://msdn.microsoft.com/library/windows/hardware/ff539007))。
2.  コールバック ルーチンへのポインターを指定、 *USB デバイスの構成インターフェイス*(**StartDeviceCallback**のメンバー [ **USBC\_デバイス\_構成\_インターフェイス\_V1**](https://msdn.microsoft.com/library/windows/hardware/ff538990))。
3.  複合デバイスと明示的には、デバイス ID と一致する INF ファイルを読み込みます一般的な親の USB ドライバーと、フィルター ドライバーの両方を提供します。

### <a name="implementation-considerations"></a>実装に関する注意点


列挙体のコールバック ルーチンを含むフィルター ドライバーには、上限または下限フィルター ドライバーのいずれかを指定できます。 一般的な親の USB ドライバーを受信すると、 [ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749)複合デバイスを開始するには、USB デバイスの照会送信することによって構成インターフェイス、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff551687)ドライバー スタックの一番上に要求します。

受信時、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff551687)要求、フィルター ドライバーする必要がありますチェックイン GUID 型、 **InterfaceType**メンバーが要求されているインターフェイス型 USB のことを確認する要求の\_BUS\_インターフェイス\_USBC\_構成\_GUID。 場合は、フィルター ドライバーのインターフェイス ポインターを返します、**インターフェイス**IRP のメンバー。

列挙体のコールバック ルーチンは、配列へのポインターを返す必要があります*関数記述子*([**USBC\_関数\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff539001))インターフェイスのコレクションを記述するとします。 各関数の記述子には、インターフェイスの記述子の配列が含まれています ([**USB\_インターフェイス\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff540065)) インターフェイスのコレクションを記述します。 コールバック ルーチンでは、非ページ プールから関数記述子とインターフェイスの記述子の両方を割り当てる必要があります。 一般的な親ドライバーでは、このメモリを解放します。 コールバック ルーチンを確認する必要があります、 **NumberOfInterfaces**のそれぞれに所属**USB\_インターフェイス\_記述子**でインターフェイスの数が正確に報告しますインターフェイスのコレクション。

一般的な親ドライバーは、各関数の記述子の物理デバイス オブジェクト (PDO) を作成します。

USB デバイスの構成インターフェイスと列挙型のコールバック ルーチンにまとめられています[汎用親ドライバー ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#usbccgp)します。

### <a name="usb-generic-parent-driver-loading-mechanism"></a>USB 一般的な親ドライバーの読み込みメカニズム


複合デバイスが記載された要件を満たしている場合[USB の複合デバイスの列挙体](enumeration-of-the-composite-parent-device.md)、オペレーティング システムの互換性のある ID を生成する`USB\COMPOSITE`デバイスが複合であることを示します。 Usb.inf で互換性のある ID が一致し、オペレーティング システムを読み込みます、USB の一般的な親ドライバー自動的には、ベンダーから提供された INF ファイルのヘルプを表示しません。

ただし、この既定のメカニズムは使えませんインターフェイスのコレクションのカスタム列挙を必要とする複合デバイスの既定のメカニズム、システム読み込まれないため、必要なベンダーから提供されたフィルター ドライバー。 列挙コールバック ルーチン メカニズムの動作をフィルター ドライバー、USB デバイスの構成インターフェイスを公開する必要があります既に読み込まれている USB の一般的な親複合デバイスのインターフェイスのコレクションを列挙する場合。 これには、複合デバイスのベンダーを複合デバイスのデバイス ID と一致して、一般的な親の USB ドライバーと、フィルター ドライバーの両方を明示的に読み込みます INF ファイルをインストールする必要があります。


## <a name="support-for-the-wireless-mobile-communication-device-class"></a>ワイヤレス モバイル コミュニケーション デバイス クラスのサポート


Windows Vista では、 [USB 汎用親ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)ユニバーサル シリアル バス (USB) 通信デバイス クラス (CDC) USB ワイヤレス モバイル通信デバイス クラス (に含まれているデバイスのサポートを提供します。WMCDC)。

USB ワイヤレス モバイル通信デバイス クラス (WMCDC) 仕様の接続、制御、およびホストとワイヤレス モバイル デバイス (携帯電話など) の間のコンテンツの交換のための標準の確立、デバイスが USB ポートに接続されています。 WMCDC は、さまざまな通信とネットワーク デバイスが含まれています、通信デバイス クラス (CDC) の拡張です。 このセクションでは、Windows オペレーティング システムで CDC と WMCDC のデバイスをサポートするアーキテクチャについて説明します。

WMCDC デバイスに分類される複数の関数から成る*論理ハンドセット*します。 ほとんどの WMCDC デバイスは 1 つの論理ハンドセットが、デバイスは、複数の論理電話機を必要があります。 通常、論理電話機には、データ、fax モデムやオブジェクト ストアでは、呼び出しの制御機能などの関数が含まれます。 論理ハンドセットは、USB オーディオ クラス仕様、USB ヒューマン入力デバイス (HID) クラスの指定、および USB ビデオ クラス仕様などの他の USB 仕様で定義されている関数をサポートしているにもあります。

Windows WMCDC アーキテクチャでは、ネイティブの Windows ドライバーを使用して、WMCDC デバイスの機能を管理します。 たとえば、Windows テレフォニー アプリケーション プログラム インターフェイス (TAPI) サブシステムを使用して、デバイスとデバイスのイーサネットを管理する Windows ネットワーク ドライバー インターフェイス specification (NDIS) サブシステムの音声およびデータ、fax モデムの機能を管理することができます。LAN 関数。 さらに、オブジェクト交換プロトコル (OBEX) 関数、ユーザー モードのソフトウェアの支援など、一部の関数を管理できる、 [WinUSB](winusb.md) (Winusb.sys)。

このイメージは、WMCDC デバイスのドライバー スタックの例を示します。

![デバイスの構成とドライバー スタックのサンプル](images/wmcdc-architecture.png)

WMCDC デバイスには上の図には 1 つの論理ハンドセットが含まれています。 OBEX 関数およびモデム関数。 ベンダーから提供された INF ファイルでは、モデムを管理するネイティブの Windows ドライバーを読み込みます。 OBEX 関数がマネージ関数で実行されているベンダーから提供されたユーザー モード ドライバーによって、[ユーザー モード ドライバー フレームワーク](https://msdn.microsoft.com/library/windows/hardware/ff561365)(UMDF)。 ユーザー モード ドライバーでは、Windows ポータブル デバイス (WPD) プロトコルを使用してユーザーのアプリケーションとのインターフェイスと通信する、 [WinUSB](winusb.md) USB スタックとの通信にエクスポートします。 一般に、ベンダーから提供された INF ファイル Winusb.sys の Winusb.sys を使用するインターフェイスのコレクションごとに個別のインスタンスが読み込まれます。

### <a name="registry-settings"></a>レジストリの設定

USB スタックは、WMCDC を自動的にサポートしていません。 Usbccgp.sys のインスタンスをロードする INF ファイルを提供する必要があります。 INF ファイルを含める必要があります、 **AddReg**設定セクション、 **EnumeratorClass**に 21 で、Usbccgp.sys に関連付けられているソフトウェア キーのレジストリ値\_はバイナリ値3 つの数値から構築します。0x02, 0x00, 0x00 とします。 サンプル INF ファイルから次のコード例は、設定する方法を示しています。 **EnumeratorClass**適切な値。

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

値を割り当てる必要がある**EnumeratorClass** INF ファイルで 16 進数の組によって表される 3 つの 1 バイトのバイナリ値から構成されます。02、00 および 00 です。 これら 3 つの数値は、USB Implementers Forum がそれぞれの CDC デバイス クラス、CDC デバイス サブクラスおよび CDC デバイス プロトコルに割り当てられている値に対応します。

正しく WMCDC デバイスを列挙するためにレジストリを構成する方法の詳細については、次を参照してください。[ワイヤレス モバイル通信デバイス クラスに対するサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)します。

さらに、次のトピックには、WMCDC について説明します。

### <a name="enumerating-interface-collections-on-wmcdc"></a>WMCDC 上のインターフェイスのコレクションを列挙します。


USB ワイヤレス モバイル通信デバイス クラス (WMCDC) は、USB 通信デバイス クラス (CDC) のサブクラスです。 WMCDC 仕様では、拡張は、インターフェイスのコレクションを定義するための CDC ガイドラインを大幅に変更されません。 具体的には、WMCDC デバイスは、インターフェイスのコレクションを定義するための CDC ガイドラインに準拠する必要があります。

CDC インターフェイスのコレクションには、マスターのインターフェイスが含まれます ([**USB\_インターフェイス\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff540065)) 通信インターフェイスのクラスに属している (`bInterfaceClass = 0x02`) またはデータインターフェイス クラス (`bInterfaceClass = 0x0A`)。 マスターのインターフェイスで (つまり、通常の状況) の通信インターフェイス クラスに、マスターのインターフェイスのサブクラスが属している場合 (**bInterfaceSubClass**) な CDC の指定*コントロール モデル*します。 コントロール モデルでは、インターフェイスのコレクションに含まれるインターフェイスの種類を示します。 USB Implementers Forum を定義するコントロール モデルの説明は、CDC 仕様と WMCDC 仕様を参照してください。

インターフェイスのコレクションのマスター インターフェイスには、共用体機能記述子 (UFD) を含むクラス固有機能記述子、必須のセットが続きます。 UFD は、コレクションに属しているインターフェイスの数を示します。 **BMasterInterface** UFD のフィールドにマスター インターフェイスの数が含まれています。 0 個以上**bSubordinateInterface**フィールドには、コレクション内の他の (下位) インターフェイスの数字です。

ほとんどの種類のコントロールのモデル、 [USB 汎用親ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)各 UFD の 1 つの物理デバイス オブジェクト (PDO) を作成します。 いくつかのコントロール モデルには、一般的な親ドライバーは、オーディオのインターフェイスが属しているインターフェイスのコレクションから個別を列挙するオーディオのインターフェイスが含まれます。 オーディオのインターフェイスが下位インターフェイスの一覧に表示されます (**bSubordinateInterface**) インターフェイスのコレクションがジェネリックの親の UFD のドライバーは、オーディオのインターフェイスの別の PDO を作成します。 オーディオのインターフェイスの PDO とオーディオのインターフェイスが属しているインターフェイスのコレクションの PDO の両方は、デバイスのオブジェクト ツリーの親複合デバイスの機能のデバイス オブジェクト (FDO) の上に直接が。 オーディオのインターフェイスの PDO は、インターフェイスのコレクションの子ではありません。 オーディオのインターフェイスの列挙体については、「[ワイヤレス モバイル通信デバイス クラスに対するサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)します。

レジストリの特性を持つ列挙型は構成可能な 2 つのコントロール モデルがあります。 ワイヤレス ハンドセット コントロール モデル (WHCM)、論理の携帯電話端末と、オブジェクト交換プロトコル (OBEX) コントロール モデルを定義します。 でこれらの 2 つの制御モデルの列挙型の特性を構成するには、で、Usbccgp.sys のインスタンスをロードし、値を設定する INF ファイルを提供する必要があります**CdcFlags**のインスタンスで、Usbccgp.sys をソフトウェア キー。 次の表に、構成オプションの**CdcFlags**します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>CdcFlags ビット</th>
<th>ビットを 0 に設定</th>
<th>ビットが 1 に設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0 (マスク = 0x00000001)</p></td>
<td><p>一般的な親の USB ドライバーは、OBEX インターフェイスごとに個別の PDO を作成します。</p></td>
<td><p>一般的な親の USB ドライバーは、すべての OBEX インターフェイスの 1 つの PDO を作成します。</p></td>
</tr>
<tr class="even">
<td><p>1 (マスク 0x00000010 =)</p></td>
<td><p>一般的な親の USB ドライバーでは、WHCM インターフェイス (論理ハンドセット) Pdo は作成されません。 これらのインターフェイスは、デバイス オブジェクト ツリーの観点から非表示のままです。</p></td>
<td><p>一般的な親の USB ドライバーは、各 WHCM インターフェイスの PDO を作成します。</p></td>
</tr>
</tbody>
</table>

 

たとえば、両方のビットをオフにする (に 0 に設定)、INF ファイルに、次の行があります、 **DDInstall.AddReg**セクション。

```INF
HKR, , CdcFlags, 0x00010001, 0x00000000
```

両方のビットを 1 に設定するには、次の行が、INF ファイルにあります。

```INF
HKR, , CdcFlags, 0x00010001, 0x00000011
```

ビット 0 ~ 1 と 1 を 0 ビットの両方を設定するには、次の行が、INF ファイルにあります。

```INF
HKR, , CdcFlags, 0x00010001, 0x00000001
```

いずれかのビットを設定またはその他のビットとは無関係に、リセットできます。

次の図は、レジストリ構成の別の方法を示しています。 同じデバイスに対して別のデバイスのツリーを作成できます。

ビット 0 ビット 1 の両方と、次の図は、PDO 構成を示しています。 **CdcFlags**は 0。

![cdcflags のデバイス オブジェクトのマッピングをインターフェイスのコレクションを示す図 = 0x00000000](images/cdcflags.png)

上記の図でワイヤレス ハンドセット コントロール モデル (WHCM) インターフェイスのコレクションには、次の 3 つの下位インターフェイス コレクションが含まれています (**bSubordinateInterface**): 2 つの OBEX コレクションとモデムのコレクション。 ビット 0、 **CdcFlags** 0 の場合は、一般的な親の USB ドライバーが WHCM インターフェイスのコレクションの PDO を作成しないようにします。 ビット 1、 **CdcFlags**は 0 のため、一般的な親の USB ドライバーが OBEX インターフェイスのコレクションごとに個別の PDO を生成します。

ビット 0 ビット 1 の両方と、次の図は、PDO 構成を示しています。 **CdcFlags**設定されます。

![cdcflags のデバイス オブジェクトのマッピングをインターフェイスのコレクションを示す図 0x00010001 を =](images/cdcflags-wpd.png)

ため、ビット 0 の**CdcFlags**設定されている WHCM インターフェイスのコレクションの PDO を作成している一般的な親の USB ドライバーを 1 にします。 ため、ビット 1 **CdcFlags** 1 に設定されて、一般的な親の USB ドライバー OBEX コレクションの 2 つのグループ化し、両方の OBEX コレクションの 1 つの PDO を生成します。

カーネル レベルで 1 つの PDO を OBEX コレクションを表すと、ユーザー モード ドライバー内で個々 の OBEX コレクションごとの間で区別することができます。 Windows ポータブル デバイス (WPD) プロトコルは、カーネル レベルで 1 つの PDO をグループ化しているすべての OBEX 関数、ユーザー レベルで別の OBEX 関数の間でデータ ストリームを多重化するのに役立ちます。

次のサンプルの INF ファイルでは、WMCDC デバイスを管理する USB の一般的な親ドライバーがロードし、USB の一般的な親論理ハンドセットの Pdo を作成して、論理のハンドセットですべての OBEX コレクションの 1 つの PDO を作成するように指示します。

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
### <a name="handling-cdc-and-wmcdc-interface-collections"></a>CDC と WMCDC インターフェイスのコレクションの処理


」の説明に従って、汎用的な親の USB ドライバーが特別な方法でワイヤレス ハンドセット コントロール モデル (WHCM) インターフェイスを処理[ワイヤレス モバイル通信デバイス クラスに対するサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)します。

次の一覧は、その他のインターフェイスのコレクションから CDC と WMCDC インターフェイスのコレクションの処理とは異なる、最も重要な方法をまとめたものです。

-   ワイヤレス モバイル通信デバイス クラスでは、限られた量のインターフェイスのコレクションの入れ子を許可します。 具体的には、論理ハンドセット インターフェイス コレクション (つまり、WHCM インターフェイス コレクション) は、その他の下位のインターフェイスのコレクションを含めることができます。 たとえば、WMCDC 準拠の電話、さらに、コントロールの抽象モデルのコレクションと、OBEX コレクションが含まれています、WHCM インターフェイス コレクションことができます。
-   USB の一般的な親ドライバー WHCM インターフェイスのコレクションを列挙できませんを構成できます。 列挙されない WHCM インターフェイスのコレクションは非が、一般的な親ドライバーがグループ化し、下位のインターフェイスのコレクションを列挙する WHCM インターフェイス コレクションに属している統合機能ディスクリプター (Ufd) からの情報を使用します。
-   OBEX コントロール モデル インターフェイスのコレクション、またはすべての OBEX コントロール モデル インターフェイス コレクションの 1 つの PDO を作成するには、別の物理デバイス オブジェクト (Pdo) を作成する USB 一般的な親ドライバーを構成することができます。
-   UFD のインターフェイスの番号の一覧には、ギャップを持つことができます。 つまり、UFD のインターフェイスの番号は連続していないインターフェイスを参照できます。 この種類の番号が無効です、たとえば、 [USB インターフェイスの関連付け記述子 (IAD)](usb-interface-association-descriptor.md)シーケンシャル番号を持つ、インターフェイスが連続する必要があります。
-   Ufd はオーディオ関連のインターフェイスのコレクションを含めることができます。
-   CDC と WMCDC インターフェイスのコレクションのハードウェア識別子 (Id) は、インターフェイス サブクラスを含める必要があります。 ハードウェア Id 持つには、MI が含まれて、他の USB インターフェイス\_%02 X サフィックス インターフェイスの番号を指定するインターフェイス サブクラスをに関する情報は含まれません。 ベンダーとのインターフェイスをロードするドライバーを確認する記述子レイアウト内の位置ではなく、特定のインターフェイスのコレクションに一致するハードウェア ID の INF ファイルを提供できるようにするハードウェア ID に含まれるサブクラス情報コレクションです。 ハードウェア ID のサブクラスの情報は、ユーザー モード ドライバーなどの代替手段を WMCDC インターフェイスのコレクションを管理する現在のベンダーから提供されたドライバーから段階的な移行パスができます。 CDC と WMCDC ハードウェア Id の例については、次を参照してください。[ワイヤレス モバイル通信デバイス クラスに対するサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)します。 USB インターフェイスのハードウェアの概要については、Id が書式設定は、「 [USB デバイスの識別子](https://msdn.microsoft.com/library/windows/hardware/ff546284)します。

### <a name="cdc-and-wmcdc-control-models"></a>CDC と WMCDC コントロール モデル


CDC と WMCDC コントロール モデルのセクションでは、Microsoft Windows オペレーティング システムでサポートされているインターフェイスのコレクションのプロパティについて説明します。 それぞれの説明には、インターフェイスのコレクションの一般的な親の USB ドライバーが生成されます。 ハードウェアとデバイスの識別子 (Id) の一覧が、特に含まれます。

Windows をサポートするインターフェイスのコレクションのほとんどが、通信デバイス クラス (CDC) およびワイヤレス モバイル通信デバイス クラス (WMCDC) に属するコントロール モデルに対応していますが、オペレーティング システムは、従来のオーディオとビデオにもサポートインターフェイスのコレクションと、モバイル コンピューティング プロモーション Consortium (MCPC) を定義するインターフェイスのコレクション。

このセクションに記載されているインターフェイスのコレクション以下のとおりです。

#### <a name="audio-class-interfaces"></a>オーディオのクラス インターフェイス


CDC と WMCDC デバイスで発生する USB オーディオ デバイス クラス インターフェイス コレクションでは、次のプロパティがあります。

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
<td><p><em>ユニバーサル シリアル バス デバイス クラス定義のオーディオ デバイス</em>、バージョン 1.0。</p></td>
</tr>
<tr class="even">
<td><p>クラス</p></td>
<td><p>インターフェイスのコレクション内のすべてのインターフェイスは、オーディオ デバイス クラス (0x01) に属している必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>サブクラス</p></td>
<td><p>インターフェイスのコレクション内の各インターフェイスでは、コレクション内の最初のインターフェイスから別のサブクラスが必要です。</p></td>
</tr>
<tr class="even">
<td><p>プロトコル</p></td>
<td><p>None (0x00) です。</p></td>
</tr>
<tr class="odd">
<td><p>列挙</p></td>
<td><p>[はい]。</p></td>
</tr>
<tr class="even">
<td><p>関連するインターフェイス</p></td>
<td><p>ストリーミングのサブクラス (0x02) に属している 0 個以上の連続するインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;MI_%02x</code></pre>
<p>オーディオのインターフェイスのコレクションのハードウェア Id では、インターフェイス クラスに固有の情報は含まれません。 ハードウェア オーディオ インターフェイスのコレクションに関連付けられている Id の書式設定の詳細については、次を参照してください。<a href="support-for-the-wireless-mobile-communication-device-class--wmcdc-.md" data-raw-source="[Support for the Wireless Mobile Communication Device Class](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)">ワイヤレス モバイル通信デバイス クラスに対するサポート</a>します。</p></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_01&amp;SubClass_01&amp;Prot_00
USB\Class_01&amp;SubClass_01
USB\Class_01</code></pre>
<p>互換性のあるオーディオ インターフェイスのコレクション Id の形式は、インターフェイス クラス、インターフェイス サブクラスをおよびプロトコルの埋め込みについてを説明します。 CDC または WMCDC デバイスでは、オーディオ インターフェイスのコレクションのインターフェイス クラスは 01 01 は、サブクラスは、プロトコルは 00。</p></td>
</tr>
</tbody>
</table>

#### <a name="cdc-abstract-control-model"></a>CDC 抽象コントロール モデル


抽象コントロール モデル (ACM) の 2 つのバージョンがあります。 定義された元のバージョン、 *USB 通信デバイス クラス*(CDC) の仕様。 *USB ワイヤレス モバイル通信デバイス クラス*(WMCDC) 仕様には、ACM の拡張の定義が含まれています。

WMCDC 仕様に準拠しているインターフェイスのコレクションに記載されて[ワイヤレス モバイル通信デバイス クラスに対するサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)します。

CDC 仕様に準拠しているインターフェイスのコレクションには、次のプロパティがあります。

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
<td><p><em>ユニバーサル シリアル バス クラスの定義の通信デバイス</em>、バージョン 1.1 では、セクション 3.6.2 します。</p></td>
</tr>
<tr class="even">
<td><p>マスターのインターフェイスのクラス</p></td>
<td><p>通信インターフェイス クラス (0x02) です。</p></td>
</tr>
<tr class="odd">
<td><p>マスターのインターフェイスのサブクラス</p></td>
<td><p>ACM (0X02)。</p></td>
</tr>
<tr class="even">
<td><p>プロトコル</p></td>
<td><p>任意です。</p></td>
</tr>
<tr class="odd">
<td><p>列挙</p></td>
<td><p>[はい]。</p></td>
</tr>
<tr class="even">
<td><p>関連するインターフェイス</p></td>
<td><p>1 つのデータ クラス インターフェイスと共用体機能記述子 (UFD) を参照する省略可能なオーディオ クラスのインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_02&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_02
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_02&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_02</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_02&amp;Prot_%02X
USB\Class_02&amp;SubClass_02
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>UFD は ACM インターフェイスのコレクションとは無関係に列挙されているオーディオ インターフェイス コレクションを参照できます。</p></td>
</tr>
</tbody>
</table>

#### <a name="cdc-atm-networking-control-model"></a>CDC ATM ネットワーク コントロール モデル


USB CDC ATM ネットワーク コントロール モデル (ANCM) インターフェイスのコレクションには、次のプロパティがあります。

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
<td><p><em>ユニバーサル シリアル バス クラスの定義の通信デバイス</em>、バージョン 1.1 では、セクション 3.8.3</p></td>
</tr>
<tr class="even">
<td><p>マスターのインターフェイスのクラス</p></td>
<td><p>通信インターフェイス クラス (0x02)</p></td>
</tr>
<tr class="odd">
<td><p>マスターのインターフェイスのサブクラス</p></td>
<td><p>ANCM (0x07)</p></td>
</tr>
<tr class="even">
<td><p>プロトコル</p></td>
<td><p>None (0x00)</p></td>
</tr>
<tr class="odd">
<td><p>列挙</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p>関連するインターフェイス</p></td>
<td><p>Union 関数型記述子 (UFD) によって参照される 1 つのデータ クラス インターフェイス</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_07&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_07
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_07&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_07</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_07&amp;Prot_00
USB\Class_02&amp;SubClass_07
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>


#### <a name="cdc-capi-control-model"></a>CDC CAPI コントロール モデル


USB CDC 共通 ISDN API (CAPI) コントロール モデル インターフェイスのコレクションの次のプロパティがあります。

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
<p><em>ユニバーサル シリアル バス クラスの定義の通信デバイス</em>、バージョン 1.1 では、セクション 3.7.2</p></td>
</tr>
<tr class="even">
<td><p>マスターのインターフェイスのクラス</p></td>
<td><p>通信インターフェイス クラス (0x02)</p></td>
</tr>
<tr class="odd">
<td><p>マスターのインターフェイスのサブクラス</p></td>
<td><p>CAPI (0X05)</p></td>
</tr>
<tr class="even">
<td><p>プロトコル</p></td>
<td><p>None (0x00)</p></td>
</tr>
<tr class="odd">
<td><p>列挙</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p>関連するインターフェイス</p></td>
<td><p>Union 関数型記述子 (UFD) を参照する 1 つのデータ クラス インターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_05&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_05</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_05&amp;Prot_00
USB\Class_02&amp;SubClass_05</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>

#### <a name="cdc-direct-line-control-model"></a>CDC ダイレクト行コントロール モデル


USB CDC 直接行コントロール モデル (DLCM) インターフェイスのコレクションには、次のプロパティがあります。

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
<td><p><em>ユニバーサル シリアル バス クラスの定義の通信デバイス</em>、バージョン 1.1 では、セクション 3.6.1 します。</p></td>
</tr>
<tr class="even">
<td><p>マスターのインターフェイスのクラス</p></td>
<td><p>通信インターフェイス クラス (0x02) です。</p></td>
</tr>
<tr class="odd">
<td><p>マスターのインターフェイスのサブクラス</p></td>
<td><p>DLCM (0x01).</p></td>
</tr>
<tr class="even">
<td><p>プロトコル</p></td>
<td><p>None (0x00) です。</p></td>
</tr>
<tr class="odd">
<td><p>列挙</p></td>
<td><p>[はい]。</p></td>
</tr>
<tr class="even">
<td><p>関連するインターフェイス</p></td>
<td><p>Union 関数型記述子 (UFD) を参照するオーディオ クラスまたはベンダー定義のインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_01&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_01
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_01&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_01</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_01&amp;Prot_00
USB\Class_02&amp;SubClass_01
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>UFD は、DLCM インターフェイスのコレクションとは無関係に列挙されているオーディオ クラス インターフェイスのコレクションを参照します。</p></td>
</tr>
</tbody>
</table>

#### <a name="cdc-ethernet-networking-control-model"></a>CDC のイーサネット ネットワーク コントロール モデル


USB CDC イーサネット ネットワーク コントロール モデル (ENCM) インターフェイスのコレクションには、次のプロパティがあります。

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
<td><p><em>ユニバーサル シリアル バス クラスの定義の通信デバイス</em>、バージョン 1.1 では、セクション 3.8.2 します。</p></td>
</tr>
<tr class="even">
<td><p>マスターのインターフェイスのクラス</p></td>
<td><p>通信インターフェイス クラス (0x02) です。</p></td>
</tr>
<tr class="odd">
<td><p>マスターのインターフェイスのサブクラス</p></td>
<td><p>ENCM (0X06)。</p></td>
</tr>
<tr class="even">
<td><p>プロトコル</p></td>
<td><p>None (0x00) です。</p></td>
</tr>
<tr class="odd">
<td><p>列挙</p></td>
<td><p>[はい]。</p></td>
</tr>
<tr class="even">
<td><p>関連するインターフェイス</p></td>
<td><p>Union 関数型記述子 (UFD) を参照する 1 つのデータ クラス インターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_06&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_06
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_06&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_06</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_06&amp;Prot_00
USB\Class_02&amp;SubClass_06
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>このコントロール モデルの互換性 Id いて、Microsoft 提供の INF ファイルに一致します。 オペレーティング システムがベンダーから提供された INF ファイルでのハードウェア Id のいずれかと一致するを見つけられない場合、システムでインターフェイスのコレクションを管理するネイティブの NDIS ミニポート ドライバーが自動的に読み込まれます。</p></td>
</tr>
</tbody>
</table>

#### <a name="cdc-multi-channel-isdn-control-model"></a>マルチ チャネルの CDC ISDN コントロール モデル


USB CDC マルチ チャンネル ISDN コントロール モデル (MCCM) インターフェイスのコレクションには、次のプロパティがあります。

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
<td><p><em>ユニバーサル シリアル バス クラスの定義の通信デバイス</em>、バージョン 1.1 では、3.7.1</p></td>
</tr>
<tr class="even">
<td><p>マスターのインターフェイスのクラス</p></td>
<td><p>通信インターフェイス クラス (0x02)</p></td>
</tr>
<tr class="odd">
<td><p>マスターのインターフェイスのサブクラス</p></td>
<td><p>MCCM (0X04)</p></td>
</tr>
<tr class="even">
<td><p>プロトコル</p></td>
<td><p>None (0x00)</p></td>
</tr>
<tr class="odd">
<td><p>列挙</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p>関連するインターフェイス</p></td>
<td><p>Union 関数型記述子 (UFD) を参照する複数のデータ クラス インターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_04&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_04
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_04&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_04</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_04&amp;Prot_00
USB\Class_02&amp;SubClass_04
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>

 
#### <a name="cdc-telephone-control-model"></a>CDC 電話コントロール モデル


USB CDC 電話コントロール モデル (TCM) インターフェイスのコレクションには、次のプロパティがあります。

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
<td><p><em>ユニバーサル シリアル バス クラスの定義の通信デバイス</em>、バージョン 1.1 では、セクション 3.6.3 します。</p></td>
</tr>
<tr class="even">
<td><p>マスターのインターフェイスのクラス</p></td>
<td><p>通信インターフェイス クラス (0x02) です。</p></td>
</tr>
<tr class="odd">
<td><p>マスターのインターフェイスのサブクラス</p></td>
<td><p>TCM (0X03)。</p></td>
</tr>
<tr class="even">
<td><p>プロトコル</p></td>
<td><p>任意です。</p></td>
</tr>
<tr class="odd">
<td><p>列挙</p></td>
<td><p>[はい]。</p></td>
</tr>
<tr class="even">
<td><p>関連するインターフェイス</p></td>
<td><p>Union 関数型記述子 (UFD) を参照するオーディオ クラスのインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>Hardware ID (ハードウェア ID)</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_03&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_03
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_03&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_03</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 ID</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_03&amp;Prot_%02X
USB\Class_02&amp;SubClass_03
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>UFD は、TCM インターフェイスのコレクションとは無関係に列挙されているオーディオ クラス インターフェイスのコレクションを参照できます。</p></td>
</tr>
</tbody>
</table>

#### <a name="mcpc-vendor-unique-interfaces"></a>MCPC ベンダー固有のインターフェイス


モバイル コンピューティング プロモーション Consortium (MCPC) では、ワイヤレス モバイル通信デバイス クラス (WMCDC) 仕様を CDC デバイスのベンダー固有の書式を提供する前にインターフェイスのコレクションの形式が定義されています。 そのため、MCPC インターフェイスのコレクションでは、WMCDC 標準に準拠していません。

ただし、WMCDC が有効になっている場合は、一般的な親の USB ドライバーは MCPC インターフェイスのコレクションを列挙できます。 MCPC インターフェイスのコレクションには、次のプロパティがあります。

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
<td><p>モバイル コンピューティング プロモーション Consortium (MCPC) GL 004 仕様</p></td>
</tr>
<tr class="even">
<td><p>クラス</p></td>
<td><p>CDC (0X02)</p></td>
</tr>
<tr class="odd">
<td><p>サブクラス</p></td>
<td><p>0x88</p></td>
</tr>
<tr class="even">
<td><p>プロトコル</p></td>
<td><p>None (0x00)</p></td>
</tr>
<tr class="odd">
<td><p>列挙</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p>関連するインターフェイス</p></td>
<td><p>Union 関数型記述子 (UFD) を参照する 0 個以上のデータ クラス インターフェイス</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_88&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_88
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_88&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_88</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_88&amp;Prot_00
USB\Class_02&amp;SubClass_88
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>

#### <a name="video-class-interfaces"></a>ビデオのクラス インターフェイス


CDC と WMCDC デバイスで発生する USB ビデオ デバイスのクラス インターフェイスのコレクションでは、次のプロパティがあります。

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
<td><p><em>ユニバーサル シリアル バス デバイスのクラス定義のビデオ デバイス</em>、バージョン 1.0。</p></td>
</tr>
<tr class="even">
<td><p>クラス</p></td>
<td><p>ビデオ (0x0E)。</p></td>
</tr>
<tr class="odd">
<td><p>サブクラス</p></td>
<td><p>ビデオ コントロール (0x01)。</p></td>
</tr>
<tr class="even">
<td><p>プロトコル</p></td>
<td><p>None (0x00) です。</p></td>
</tr>
<tr class="odd">
<td><p>列挙</p></td>
<td><p>[はい]。</p></td>
</tr>
<tr class="even">
<td><p>関連するインターフェイス</p></td>
<td><p>ストリーミングのサブクラス (0x02) に属している 0 個以上の連続するインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;MI_%02x</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_0E&amp;SubClass_01&amp;Prot_00
USB\Class_0E&amp;SubClass_01
USB\Class_0E</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>ビデオ クラス インターフェイスのコレクションでは、CDC のデバイスで特別な処理を受信します。 CDC 以外のデバイスでビデオ クラス インターフェイスのコレクションは、インターフェイスの関連付け記述子 (Iad) によって定義されます。 CDC のデバイスでビデオ クラス インターフェイスのコレクションは、共用体機能記述子 (Ufd) によって定義されます。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-abstract-control-model"></a>WMCDC 抽象コントロール モデル


抽象コントロール モデル (ACM) の 2 つのバージョンがあります。 元のバージョンは、USB 通信デバイス クラス (CDC) 仕様で定義されます。 USB ワイヤレス モバイル通信デバイス クラス (WMCDC) 仕様には、ACM の拡張の定義が含まれています。 Fax モデム/関数を含む ACM コレクションには、ACM の WMCDC 定義ではなく、元の CDC ACM 定義を使用する必要があります。

CDC の仕様に準拠しているインターフェイスのコレクションに記載されて[ワイヤレス モバイル通信デバイス クラスに対するサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)します。

WMCDC 仕様に準拠しているインターフェイスのコレクションには、次のプロパティがあります。

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
<td><p><em>ユニバーサル シリアル バス CDC サブクラス仕様のワイヤレス モバイル通信デバイス</em>、バージョン 1.0、6.2 を参照します。</p></td>
</tr>
<tr class="even">
<td><p>マスターのインターフェイスのクラス</p></td>
<td><p>通信インターフェイス クラス (0x02) です。</p></td>
</tr>
<tr class="odd">
<td><p>マスターのインターフェイスのサブクラス</p></td>
<td><p>ACM (0X02)。</p></td>
</tr>
<tr class="even">
<td><p>プロトコル</p></td>
<td><p>コレクションでコマンド セットのプロトコルを使用する場合、互換性 Id に埋め込まれているプロトコル値は 0x01 です。 互換性 Id に埋め込まれているプロトコルの値が 0x2 には、コレクションは、WMCDC 仕様を示すプロトコルのいずれかを使用している場合、0x06 または 0 xfe でします。</p></td>
</tr>
<tr class="odd">
<td><p>列挙</p></td>
<td><p>[はい]。</p></td>
</tr>
<tr class="even">
<td><p>関連するインターフェイス</p></td>
<td><p>Union 関数型記述子 (UFD) を参照する 1 つのデータ クラス インターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_Modem&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_Modem
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_Modem&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_Modem</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_Modem&amp;Prot_%02X
USB\Class_02&amp;SubClass_Modem
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>UFD は ACM インターフェイスのコレクションとは無関係に列挙されているオーディオ インターフェイス コレクションを参照場合があります。</p>
<p>インターフェイスのコレクションは、WMCDC 仕様のセクション 6.2 で指定されている特殊な記述子とエンドポイントの要件に準拠する必要があります。 インターフェイスのコレクションが WMCDC 要件に準拠していない場合は、インターフェイスは、CDC の要件に準拠して、一般的な親の USB ドライバー列挙、インターフェイスのコレクションと、CDC の書式を持つ汎用ハードウェア Id 」の説明に従って<a href="support-for-the-wireless-mobile-communication-device-class--wmcdc-.md" data-raw-source="[Support for the Wireless Mobile Communication Device Class](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)">ワイヤレス モバイル通信のデバイス クラスに対するサポート</a>します。</p>
<p>このコントロール モデルの互換性 Id いて、Microsoft 提供の INF ファイルに一致します。 システムが、ネイティブのテレフォニー アプリケーション プログラミング インターフェイス (TAPI) モデム フィルター ドライバーにモデム関数とセットの管理を自動的に読み込まれますオペレーティング システムがベンダーから提供された INF ファイルでのハードウェア Id のいずれかと一致するを見つけられない場合、TAPI のレジストリ設定を適切なプロトコル コードが 0 xfe である場合。 プロトコルのコードは、0 xfe は、仕入先は、TAPI のレジストリ設定を正しく設定するデバイスまたはクラスの共同インストーラーを指定する必要があります。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-device-management-model"></a>WMCDC デバイスの管理モデル


USB WMCDC デバイスの管理モデル (DMM) インターフェイスのコレクションには、次のプロパティがあります。

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
<td><p><em>ユニバーサル シリアル バス CDC サブクラス仕様のワイヤレス モバイル通信デバイス</em>、バージョン 1.0 では、セクション 6.6 します。</p></td>
</tr>
<tr class="even">
<td><p>マスターのインターフェイスのクラス</p></td>
<td><p>通信インターフェイス クラス (0x02) です。</p></td>
</tr>
<tr class="odd">
<td><p>マスターのインターフェイスのサブクラス</p></td>
<td><p>DMM (0X09)。</p></td>
</tr>
<tr class="even">
<td><p>プロトコル</p></td>
<td><p>任意です。</p></td>
</tr>
<tr class="odd">
<td><p>列挙</p></td>
<td><p>[はい]。</p></td>
</tr>
<tr class="even">
<td><p>関連するインターフェイス</p></td>
<td><p>なし。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_09&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_09
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_09&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_09</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_09&amp;Prot_%02X
USB\Class_02&amp;SubClass_09
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>このコントロール モデルでは、共用体機能記述子 (UFD) は使用しません。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-mobile-direct-line-model"></a>WMCDC モバイル Direct Line モデル


USB WMCDC Mobile 直接行モデル (MDLM) インターフェイスのコレクションには、次のプロパティがあります。

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
<td><p><em>ユニバーサル シリアル バス CDC サブクラス仕様のワイヤレス モバイル通信デバイス</em>、バージョン 1.0 では、セクション 6.7</p></td>
</tr>
<tr class="even">
<td><p>マスターのインターフェイスのクラス</p></td>
<td><p>通信インターフェイス クラス (0x02)</p></td>
</tr>
<tr class="odd">
<td><p>マスターのインターフェイスのサブクラス</p></td>
<td><p>MDLM (0X0A)</p></td>
</tr>
<tr class="even">
<td><p>プロトコル</p></td>
<td><p>任意</p></td>
</tr>
<tr class="odd">
<td><p>列挙</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p>関連するインターフェイス</p></td>
<td><p>1 つまたは複数のデータ クラス インターフェイス共用体機能記述子 (UFD) を参照します。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_0A&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_0A
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_0A&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_0A</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_0A&amp;Prot_%02X
USB\Class_02&amp;SubClass_0A
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>なし。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-obex-control-model-multiple-pdos"></a>WMCDC OBEX コントロール モデル (複数 Pdo)


オブジェクト交換プロトコル (OBEX) コントロール モデル インターフェイスのコレクションを列挙するために 2 つの方法があります一般的な親の USB ドライバーがすべての OBEX インターフェイスをまとめてグループ化とすべての OBEX インターフェイスの 1 つの物理デバイス オブジェクト (PDO) を作成、または。親のドライバーでは、OBEX インターフェイスごとに個別の PDO を作成できます。 ハードウェアのグループ化された OBEX インターフェイスの一般的な親の USB ドライバーを生成する Id については、次を参照してください。[ワイヤレス モバイル通信デバイス クラスに対するサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)します。

一般的な親の USB ドライバーは、OBEX インターフェイスごとに個別の Pdo を割り当てます、ときに、Pdo の次のプロパティがあります。

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
<td><p><em>ユニバーサル シリアル バス CDC サブクラス仕様のワイヤレス モバイル通信デバイス</em>、バージョン 1.0 では、セクション 6.5 します。</p></td>
</tr>
<tr class="even">
<td><p>マスターのインターフェイスのクラス</p></td>
<td><p>通信インターフェイス クラス (0x02) です。</p></td>
</tr>
<tr class="odd">
<td><p>マスターのインターフェイスのサブクラス</p></td>
<td><p>OBEX (0X0B)。</p></td>
</tr>
<tr class="even">
<td><p>プロトコル</p></td>
<td><p>None (0x00) です。</p></td>
</tr>
<tr class="odd">
<td><p>列挙</p></td>
<td><p>[はい]。</p></td>
</tr>
<tr class="even">
<td><p>関連するインターフェイス</p></td>
<td><p>Union 関数型記述子 (UFD) を参照する 1 つのデータ クラス インターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_0B&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_0B
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_0B&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_0B</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_0B&amp;Prot_00
USB\Class_02&amp;SubClass_0B
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>複合デバイスを管理する USB 一般的な親ドライバーのインスタンスに関連付けられているレジストリ設定は、PDO を 1 つまたは複数の Pdo OBEX インターフェイスを管理するかどうかを決定します。 一般的な親の USB ドライバーが OBEX インターフェイスを列挙する方法を指定するレジストリ設定の詳細については、次を参照してください。<a href="support-for-the-wireless-mobile-communication-device-class--wmcdc-.md" data-raw-source="[Support for the Wireless Mobile Communication Device Class](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)">ワイヤレス モバイル通信デバイス クラスに対するサポート</a>します。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-obex-control-model-single-pdo"></a>WMCDC OBEX コントロール モデル (単一 PDO)


オブジェクト交換プロトコル (OBEX) コントロール モデル インターフェイスのコレクションを列挙するために 2 つの方法があります一般的な親の USB ドライバーがすべての OBEX インターフェイスをまとめてグループ化とすべての OBEX インターフェイスの 1 つの物理デバイス オブジェクト (PDO) を作成、または。親のドライバーでは、OBEX インターフェイスごとに個別の PDO を作成できます。 ハードウェアとは別に列挙されている OBEX インターフェイスの一般的な親の USB ドライバーを生成する Id については、次を参照してください。[ワイヤレス モバイル通信デバイス クラスに対するサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)します。

一般的な親の USB ドライバーが 1 つの PDO をすべての OBEX インターフェイスに割り当てると、ときに PDO は次のプロパティがあります。

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
<td><p><em>ユニバーサル シリアル バス CDC サブクラス仕様のワイヤレス モバイル通信デバイス</em>、バージョン 1.0 では、セクション 6.5 します。</p></td>
</tr>
<tr class="even">
<td><p>マスターのインターフェイスのクラス</p></td>
<td><p>通信インターフェイス クラス (0x02) です。</p></td>
</tr>
<tr class="odd">
<td><p>マスターのインターフェイスのサブクラス</p></td>
<td><p>OBEX (0X0B)。</p></td>
</tr>
<tr class="even">
<td><p>プロトコル</p></td>
<td><p>None (0x00) です。</p></td>
</tr>
<tr class="odd">
<td><p>列挙</p></td>
<td><p>[はい]。</p></td>
</tr>
<tr class="even">
<td><p>関連するインターフェイス</p></td>
<td><p>Union 関数型記述子 (UFD) を参照する 1 つのデータ クラス インターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;WPD_OBEX&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;WPD_OBEX
USB\Vid_%04x&amp;Pid_%04x&amp;WPD_OBEX&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;WPD_OBEX</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;WPD_OBEX
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>複合デバイスを管理する USB 一般的な親ドライバーのインスタンスに関連付けられているレジストリ設定は、PDO を 1 つまたは複数の Pdo OBEX インターフェイスを管理するかどうかを決定します。 一般的な親の USB ドライバーが OBEX インターフェイスを列挙する方法を指定するレジストリ設定の詳細については、次を参照してください。<a href="support-for-interface-collections.md" data-raw-source="[Enumeration of Interface Collections on USB Composite Devices](support-for-interface-collections.md)">複合デバイスを USB でインターフェイス コレクションの列挙体</a>します。</p></td>
</tr>
</tbody>
</table>

#### <a name="wmcdc-wireless-handset-control-model"></a>WMCDC ワイヤレス ハンドセット コントロール モデル


一般的な親の USB ドライバーがワイヤレス ハンドセット コントロール モデル (WHCM) インターフェイスのコレクションを常に列挙することはできません。 USB の一般的な親ドライバー WHCM インターフェイスのコレクションを管理するのインスタンスに関連付けられているレジストリ設定は、かどうかに、一般的な親の USB ドライバーがインターフェイスのコレクションの物理デバイス オブジェクト (PDO) を作成するかどうかを決定します。 一般的な親の USB ドライバーが WHCM インターフェイスを列挙する方法を指定するレジストリ設定の詳細については、次を参照してください。[複合デバイスを USB でインターフェイス コレクションの列挙体](support-for-interface-collections.md)します。

WHCM インターフェイスの列挙のコレクションの次のプロパティがあります。

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
<td><p><em>ユニバーサル シリアル バス CDC サブクラス仕様のワイヤレス モバイル通信デバイス</em>、version 1.0, 6.1 を参照します。</p></td>
</tr>
<tr class="even">
<td><p>マスターのインターフェイスのクラス</p></td>
<td><p>通信インターフェイス クラス (0x02) です。</p></td>
</tr>
<tr class="odd">
<td><p>マスターのインターフェイスのサブクラス</p></td>
<td><p>WHCM (0X08)。</p></td>
</tr>
<tr class="even">
<td><p>プロトコル</p></td>
<td><p>None (0x00) です。</p></td>
</tr>
<tr class="odd">
<td><p>列挙</p></td>
<td><p>[はい]。</p></td>
</tr>
<tr class="even">
<td><p>関連するインターフェイス</p></td>
<td><p>なし。</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェア Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_08&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Rev_%04x&amp;Cdc_08
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_08&amp;MI_%02x
USB\Vid_%04x&amp;Pid_%04x&amp;Cdc_08</code></pre></td>
</tr>
<tr class="even">
<td><p>互換性 Id</p></td>
<td><pre space="preserve"><code class="language-syntax">USB\Class_02&amp;SubClass_08&amp;Prot_00
USB\Class_02&amp;SubClass_08
USB\Class_02</code></pre></td>
</tr>
<tr class="odd">
<td><p>特別な処理</p></td>
<td><p>Union 関数型記述子 (UFD) は、論理ハンドセットに関連付けられているインターフェイスを識別します。</p></td>
</tr>
</tbody>
</table>

前のトピックで、ハードウェア ID の形式が使用について説明します、次の規則。

- C 言語**printf**形式の整数を表します。 たとえば、"%04 x"を 4 桁の 16 進整数を意味します。"% 02 x"と 2 桁の 16 進整数を意味します。

- 整数、文字列に続く"Vid\_"は、ベンダーに、USB 委員会 (www.usb.org) を代入する仕入先のコードの 4 桁の 16 進数表現。

- 整数、文字列に続く"Pid\_"は、ベンダーがデバイスに割り当てる製品コードの 4 桁の 16 進数表現。

- 整数、文字列に続く"Rev\_"は、デバイスのリビジョン番号の 4 桁の 16 進数表現。

- 整数、文字列に続く"Cdc\_"はインターフェイス サブクラスです。

- 整数、文字列に続く"ポート\_"プロトコル番号です。

- 整数、文字列に続く"MI\_"から抽出されたインターフェイス数の 2 桁の 16 進数表現では、 **bInterfaceNumber**インターフェイス記述子フィールド。


### <a name="enumeration-of-interface-collections-on-usb-devices-with-iads"></a>Iad で USB デバイスのインターフェイスのコレクションの列挙


場合複合 USB デバイスが、そのファームウェア インターフェイスの関連付け記述子 (IAD)、Windows を列挙しますインターフェイス コレクションものとして、各コレクションが 1 つのデバイスと、1 つの物理デバイス オブジェクト (PDO) を割り当てますインターフェイス コレクションごとに、PDO をハードウェアと互換性のある識別子 (Id) を関連付けます。 Iad の詳細については、次を参照してください。 [USB インターフェイスの関連付けの記述子](usb-interface-association-descriptor.md)します。 このセクションでは、ハードウェア Id および互換性のある識別子 (Id)、IAD に関連付けられているインターフェイスのコレクションに割り当てられているについて説明します。

##  <a name="hardware-ids"></a>ハードウェア Id


`USB\VID_v(4)&PID_p(4)&Rev_r(4)&MI_z(2)`

`USB\VID_v(4)&PID_p(4)&MI_z(2)`

これらのハードウェア id

-   *v(4)* 仕入先に、USB 委員会を代入する 4 桁の仕入先のコードから抽出する、 **idVendor**デバイス記述子フィールド。
-   *p(4)* 4 桁の製品コード ベンダーがデバイスに割り当てるから抽出する、 **idProduct**デバイス記述子フィールド。
-   *r(4)* 4 桁のデバイスのリリース番号、バイナリのコード化された 10 進数のリビジョン、仕入先が、デバイスに割り当てるから抽出する、 **bcdDevice**デバイス記述子フィールド。
-   *z(2)* から抽出されたインターフェイスの 2 桁の番号、 **bFirstInterface** IAD のフィールド。

#### <a name="compatible-ids"></a>互換性 Id


`USB\Class_c(2)&SubClass_s(2)&Prot_p(2)`

`USB\Class_c(2)&SubClass_s(2)`

`USB\Class_c(2)`

これらの互換性のある Id で c(2)、s(2)、および p(2) 値が含まれますが取得され、それぞれから、 **bFunctionClass**、 **bFunctionSubClass**と**bFunctionProtocol**IAD のフィールドです。

関数の関数をバインドするのに Iad を再帰的には使用できません。 具体的には、デバイスでは、そのファームウェアに IAD 記述子が含まれる場合、一般的な親ドライバーはグループではないインターフェイス、オーディオ デバイス クラスによって」の説明に従って[複合デバイスを USB でインターフェイス コレクションの列挙体](support-for-interface-collections.md)します。

### <a name="enumeration-of-interface-collections-on-audio-devices-without-iads"></a>Iad なしオーディオ デバイスのインターフェイスのコレクションの列挙


オーディオ デバイスの場合、Windows オペレーティング システムは、関数に関連付けられているインターフェイス (インターフェイスのコレクション) のグループを列挙し、デバイスにインターフェイスがあるない場合でも、各グループに 1 つの物理デバイス オブジェクト (PDO) を割り当てるアソシエーションの記述子 (IAD)。

オペレーティング システムでは、インターフェイスは、次の条件を満たしている場合に、複合のオーディオ デバイスのインターフェイスがインターフェイスのコレクションにグループ化します。

-   インターフェイスのコレクション内のすべてのインターフェイスは、連続している必要があります。 つまり、インターフェイスは、ファームウェアのメモリ内で互いに隣接するである必要があります。
-   インターフェイスのコレクション内のすべてのインターフェイスは、オーディオ デバイス クラスに属している必要があります。 デバイスの製造元を指定する 0x01 の値を割り当てることでインターフェイスがオーディオ デバイス クラスに属している、 **bInterfaceClass**インターフェイス記述子フィールド。
-   インターフェイスのコレクション内の各インターフェイスでは、コレクション内の最初のインターフェイスから別のサブクラスが必要です。**BInterfaceSubClass**インターフェイス記述子のフィールドをインターフェイスのデバイスのサブクラスを指定します。

インターフェイスは、これら 3 つの条件のすべてにも満たしていない、Windows は、他のオーディオ クラス インターフェイスを持つグループ化することではなく、それを個別に列挙しようとします。

インターフェイスの関連付け記述子 (IAD) がデバイスのファームウェアに存在する場合、オペレーティング システムは特別な方法でオーディオ クラス インターフェイスをグループされません。 IAD メソッドは、USB インターフェイスをグループ化の推奨される方法では常にします。

このセクションでは、ハードウェアと互換性のある識別子 (Id) に関連付けられたオーディオ デバイス クラスに属しているインターフェイスが、インターフェイスのコレクション用のオペレーティング システムによって作成される PDO について説明します。

#### <a name="hardware-ids"></a>ハードウェア Id


`USB\VID_v(4)&PID_p(4)&Rev_r(4)&MI_z(2)`

`USB\VID_v(4)&PID_p(4)&MI_z(2)`

これらのハードウェア id

-   *v(4)* USB 標準委員会が仕入先に代入する 4 桁の仕入先のコードから抽出する、 **idVendor**デバイス記述子フィールド。
-   *p(4)* 4 桁の製品コード ベンダーがデバイスに割り当てるから抽出する、 **idProduct**デバイス記述子フィールド。
-   *r(4)* 4 桁のデバイスのリリース番号、バイナリのコード化された 10 進数のリビジョン、仕入先が、デバイスに割り当てるから抽出する、 **bcdDevice**デバイス記述子フィールド。
-   *z(2)* から抽出されたインターフェイスの 2 桁の番号、 **bInterfaceNumber**インターフェイス記述子フィールド。

##### <a name="compatible-ids"></a>互換性 Id

`USB\Class_c(2)&SubClass_s(2)&Prot_p(2)`

`USB\Class_c(2)&SubClass_s(2)`

`USB\Class_c(2)`

これらの互換性のある Id で c(2)、s(2)、および p(2) 実行される、それぞれ、bInterfaceClass、bInterfaceSubClass、および各インターフェイスのコレクション内の最初の USB インターフェイス記述子の bInterfaceProtocol フィールドから値が含まれます。

## <a name="related-topics"></a>関連トピック
[一般的な親の USB ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)  
[Microsoft 提供の USB ドライバー](system-supplied-usb-drivers.md)  



