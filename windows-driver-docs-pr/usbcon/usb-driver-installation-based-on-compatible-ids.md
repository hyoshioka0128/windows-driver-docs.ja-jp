---
Description: Microsoft が提供する、お客様のコミュニケーションおよび CDC 制御デバイス用のインボックスドライバー (Usbser)。
title: USB シリアル ドライバー (Usbser.sys)
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: a30e82bfce968f1e3168ed57444b7a79da6ac392
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007575"
---
# <a name="usb-serial-driver-usbsersys"></a>USB シリアル ドライバー (Usbser.sys)


**最終更新日**

-   2015年4月

\* * OS バージョン * *

-   Windows 10
-   Windows 8.1

**適用対象**

-   CDC コントロールデバイスのデバイス製造元

Microsoft が提供する、お客様のコミュニケーションおよび CDC 制御デバイス用のインボックスドライバー (Usbser)。

Windows 10 では、ドライバーは[カーネルモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)を使用して書き換えられ、ドライバーの全体的な安定性が向上しています。

-   ドライバーによる PnP および電源管理の向上 (突然の削除の処理など)。
-   [USB セレクティブサスペンド](usb-selective-suspend.md)などの電源管理機能が追加されました。

また、UWP アプリケーションでは、新しい[**SerialCommunication**](https://docs.microsoft.com/uwp/api/Windows.Devices.SerialCommunication)名前空間によって提供される api を使用して、アプリがこれらのデバイスと通信できるようになりました。

## <a name="usbsersys-installation"></a>Usbser のインストール


通信および CDC 制御デバイス用に、Microsoft が提供するインボックスドライバー (Usbser) を読み込みます。

**注**  Windows に含まれている USB デバイスクラスドライバーをインストールしようとすると、ドライバーをダウンロードする必要はありません。 これらは自動的にインストールされます。 自動的にインストールされない場合は、デバイスの製造元に問い合わせてください。 Windows に含まれる USB デバイスクラスドライバーの一覧については、「 [windows に含まれる usb デバイスクラスドライバー](supported-usb-classes.md)」を参照してください。

 

**Windows 10**

Windows 10 では、新しい INF (Usbser) が% Systemroot%\\Inf に追加されました。この inf は、デバイススタックの関数デバイスオブジェクト (FDO) として Usbser を読み込みます。 デバイスが通信および CDC 制御デバイスクラスに属している場合、Usbser は自動的に読み込まれます。ドライバーを参照するために独自の INF を記述する必要はありません。 ドライバーは、 [Windows に含まれている他の USB デバイスクラスドライバー](supported-usb-classes.md)と同様に、互換性のある ID の一致に基づいて読み込まれます。

`USB\Class_02`

`USB\Class_02&SubClass_02`

-   Usbser を自動的に読み込む場合は、[デバイス記述子](usb-device-descriptors.md)でクラスコードを02、サブクラスコードを02に設定します。 詳細については、usb [DWG web サイト](https://go.microsoft.com/fwlink/p/?linkid=617741)の「usb 通信デバイスクラス (または usb CDC) の仕様」を参照してください。 この方法では、システムで Usbser .inf が使用されるため、デバイスの INF ファイルを配布する必要はありません。
-   デバイスでクラスコード02が指定されていても、サブクラスコード値が02以外の場合、Usbser は自動的に読み込まれません。 Pnp マネージャーがドライバーの検索を試みます。 適切なドライバーが見つからない場合、デバイスにドライバーが読み込まれていない可能性があります。 この場合は、独自のドライバーを読み込むか、または別のインボックスドライバーを参照する INF を作成する必要があります。
-   デバイスでクラスとサブクラスのコードが02に指定されていて、Usbser ではなく別のドライバーを読み込む必要がある場合は、デバイスのハードウェア ID とインストールするドライバーを指定する INF を作成する必要があります。 例として、[サンプルドライバー](https://go.microsoft.com/fwlink/p/?LinkId=534087)に含まれている INF ファイルを調べ、デバイスと同様のデバイスを見つけます。 INF セクションの詳細については、「 [Inf ファイルの概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)」を参照してください。

Microsoft  、可能な限り、インボックスドライバーを使用**することを**お勧めします。 Windows 10 Mobile などの Windows のモバイルエディションでは、オペレーティングシステムの一部であるドライバーのみが読み込まれます。 デスクトップエディションとは異なり、外部ドライバーパッケージを使用してドライバーを読み込むことはできません。 新しいインボックス INF を使用すると、モバイルデバイスで USB-シリアルデバイスが検出された場合に、Usbser が自動的に読み込まれます。

 

**Windows 8.1 以前のバージョン**

Windows 8.1 以前のバージョンのオペレーティングシステムでは、USB-シリアルデバイスがコンピューターに接続されている場合、Usbser は自動的には読み込まれません。 ドライバーを読み込むには、 **Include**ディレクティブを使用して、モデムの inf (mdmcpq) を参照する inf を作成する必要があります。 ディレクティブは、サービスをインスタンス化し、受信トレイバイナリをコピーし、アプリケーションがデバイスを検索して通信するために必要なデバイスインターフェイス GUID を登録するために必要です。 この INF は、デバイススタック内の下位フィルタードライバーとして "Usbser" を指定します。

また、mdmcpq を使用するには、デバイスのセットアップクラスを**Modem**として指定する必要があります。 INF の [Version] セクションで、**モデム**とデバイスクラス GUID を指定します。 詳細については、「[システムによって提供されるデバイスセットアップクラス](https://docs.microsoft.com/previous-versions/ff553419(v=vs.85))」を参照してください。

``` syntax
[DDInstall.NT]
include=mdmcpq.inf
CopyFiles=FakeModemCopyFileSection 

[DDInstall.NT.Services]
include=mdmcpq.inf
AddService=usbser, 0x00000000, LowerFilter_Service_Inst 

[DDInstall.NT.HW]
include=mdmcpq.inf
AddReg=LowerFilterAddReg
```

詳細については、[このサポート技術](https://support.microsoft.com/help/837637/how-to-use-or-to-reference-the-usbser-sys-driver-from-universal-serial/)情報の記事を参照してください。

## <a name="configure-selective-suspend-for-usbsersys"></a>Usbser のセレクティブサスペンドの構成


Windows 10 以降では、Usbser は[USB セレクティブサスペンド](usb-selective-suspend.md)をサポートしています。 この機能を使用すると、接続されている USB-シリアルデバイスは、使用されていないときに低電力状態になることができ、システムは S0 状態のままになります。 デバイスとの通信が再開されると、デバイスは中断状態のままになり、動作状態を再開できます。 この機能は既定で無効になっており、このレジストリキーの下に**IdleUsbSelectiveSuspendPolicy**エントリを設定することによって有効にし、構成することができます。

**HKEY\_ローカル\_マシン\\SYSTEM\\CurrentControlSet\\列挙\\USB\\&lt;ハードウェア id&gt;\\インスタンス id &lt;デバイスパラメーター**&gt;\\

Usbser の電源管理機能を構成するには、 **IdleUsbSelectiveSuspendPolicy**を次のように設定します。

-   0x00000001

    アイドル時のセレクティブサスペンド、つまり、デバイスとの間でアクティブなデータ転送がない場合に選択します。

-   ―

    デバイスに開いているハンドルがない場合にのみ、選択的中断に入ります。

このエントリは、次の2つの方法のいずれかで追加できます。

-   インストール INF を参照する INF を作成し、そのレジストリエントリを HW に追加し**ます。AddReg**セクション。
-   拡張プロパティの OS 機能記述子にレジストリエントリを記述します。 **Bpropertyname**フィールドを Unicode 文字列 "IdleUsbSelectiveSuspendPolicy" に設定し、 **wPropertyNameLength**を62バイトに設定するカスタムプロパティセクションを追加します。 **Bpropertydata**フィールドを "0x00000001" または "0x00000000" に設定します。 プロパティ値は、リトルエンディアン32ビット整数として格納されます。

    詳細については、「 [MICROSOFT OS 記述子](https://go.microsoft.com/fwlink/p/?linkid=224878)」を参照してください。

## <a name="develop-windows-applications-for-a-usb-cdc-device"></a>USB CDC デバイス用の Windows アプリケーションの開発


USB CDC デバイスに対して Usbser をインストールする場合、アプリケーションプログラミングモデルのオプションは次のとおりです。

-   Windows 10 以降では、windows アプリは[**SerialCommunication**](https://docs.microsoft.com/uwp/api/Windows.Devices.SerialCommunication)名前空間を使用して、usbser に要求を送信できます。 シリアルポートまたはシリアルポートの抽象化を介して USB CDC デバイスと通信するために使用できる Windows ランタイムクラスを定義します。 クラスは、このようなシリアルデバイスを検出し、データの読み取りと書き込みを行う機能を提供し、フロー制御のシリアル固有のプロパティ (ボーレートの設定、シグナルの状態など) を制御します。

-   Windows 8.1 以前のバージョンでは、仮想 COM ポートを開き、デバイスと通信する Windows デスクトップアプリケーションを作成できます。 詳しくは、次のトピックをご覧ください。

    Win32 プログラミングモデル:

    -   [通信リソースの構成](https://docs.microsoft.com/windows/desktop/DevIO/configuring-a-communications-resource)
    -   [通信のリファレンス](https://docs.microsoft.com/windows/desktop/DevIO/communications-reference)

    .NET framework プログラミングモデル:

    -   [System.object 名前空間](https://docs.microsoft.com/dotnet/api/system.io.ports?redirectedfrom=MSDN)

## <a name="related-topics"></a>関連トピック
[Windows に含まれる USB デバイスクラスドライバー](supported-usb-classes.md)  
<!-- [How to use or to reference the Usbser.sys driver from universal serial bus (USB) modem .inf files](https://support.microsoft.com/help/837637/how-to-use-or-to-reference-the-usbser-sys-driver-from-universal-serial) -->



