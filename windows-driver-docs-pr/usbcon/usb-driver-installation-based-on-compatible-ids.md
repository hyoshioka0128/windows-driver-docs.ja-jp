---
Description: 通信および CDC 制御デバイス用の Microsoft 提供のインボックス ドライバー (Usbser.sys)。
title: USB シリアル ドライバー (Usbser.sys)
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 2e54bba6c5ba56376f41693ab12050d9932738aa
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "76892195"
---
# <a name="usb-serial-driver-usbsersys"></a>USB シリアル ドライバー (Usbser.sys)


**最終更新日**

-   2015 年 4 月

**OS バージョン**

-   Windows 10
-   Windows 8.1

**適用対象**

-   CDC 制御デバイスのデバイス製造元

通信および CDC 制御デバイス用の Microsoft 提供のインボックス ドライバー (Usbser.sys)。

Windows 10 では、ドライバーが[カーネルモード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)を使用して書き換えられており、ドライバーの全体的な安定性が向上しています。

-   ドライバーによる PnP および電源管理が改善されました (突然の取り外しの処理など)。
-   [USB セレクティブ サスペンド](usb-selective-suspend.md)などの電源管理機能が追加されました。

また、UWP アプリケーションでは、新しい [**Windows.Devices.SerialCommunication**](https://docs.microsoft.com/uwp/api/Windows.Devices.SerialCommunication) 名前空間によって提供される API を使用できるようになりました。これにより、アプリはこれらのデバイスと通信できるようになります。

## <a name="usbsersys-installation"></a>Usbser.sys のインストール


通信および CDC 制御デバイス用の Microsoft 提供のインボックス ドライバー (Usbser.sys) を読み込みます。

**注  **Windows に含まれている USB デバイス クラス ドライバーをインストールしようとしている場合は、ドライバーをダウンロードする必要はありません。 これらは自動的にインストールされます。 自動的にインストールされない場合は、デバイス製造元にお問い合わせください。 Windows に含まれる USB デバイス クラス ドライバーのリストについては、「[Windows に含まれる USB デバイス クラス ドライバー](supported-usb-classes.md)」を参照してください。

 

**Windows 10**

Windows 10 では、新しい INF である Usbser.inf が % Systemroot%\\Inf に追加されました。これにより、デバイス スタックの関数デバイス オブジェクト (FDO) として、Usbser.sys が読み込まれます。 デバイスが通信および CDC 制御デバイス クラスに属している場合、Usbser.sys は自動的に読み込まれます。ドライバーを参照するために独自の INF を作成する必要はありません。 ドライバーは、[Windows に含まれる USB デバイス クラス ドライバー](supported-usb-classes.md)と同様に、互換性のある ID の一致に基づいて読み込まれます。

`USB\Class_02`

`USB\Class_02&SubClass_02`

-   Usbser.sys を自動的に読み込む場合は、[デバイス記述子](usb-device-descriptors.md)でクラス コードを 02 に、サブクラス コードを 02 に設定します。 詳細については、[USB DWG に関する Web サイト](https://go.microsoft.com/fwlink/p/?linkid=617741)にある USB 通信デバイス クラス (つまり、USB CDC) の仕様を参照してください。 この方法では、システムで Usbser.inf が使用されるため、デバイスの INF ファイルを配布する必要はありません。
-   デバイスでクラス コード 02 が指定されていても、サブクラス コード値が 02 以外の場合、Usbser.sys は自動的に読み込まれません。 PnP マネージャーでドライバーの検索が試行されます。 適切なドライバーが見つからない場合、デバイスにドライバーが読み込まれていない可能性があります。 この場合は、独自のドライバーの読み込み、または別のインボックス ドライバーを参照する INF の作成が必要な場合があります。
-   デバイスでクラスとサブクラスのコードが 02 に指定されており、Usbser.sys ではなく別のドライバーを読み込む場合は、デバイスのハードウェア ID とインストールするドライバーを指定する INF を作成する必要があります。 例については、[サンプル ドライバー](https://go.microsoft.com/fwlink/p/?LinkId=534087)に含まれている INF ファイルを参照し、ご利用のデバイスに類似したデバイスを見つけてください。 INF セクションについては、「[INF ファイルの概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)」を参照してください。

**注**  Microsoft では、可能な限りインボックス ドライバーを使用することをお勧めします。 Windows 10 Mobile などの Windows のモバイル エディションでは、オペレーティング システムの一部であるドライバーのみが読み込まれます。 デスクトップ エディションとは異なり、外部ドライバー パッケージを使用してドライバーを読み込むことはできません。 新しいインボックス INF では、モバイル デバイスで USB シリアル デバイスが検出された場合に、Usbser.sys が自動的に読み込まれます。

 

**Windows 8.1 以前のバージョン**

Windows 8.1 以前のバージョンのオペレーティング システムでは、USB シリアル デバイスがコンピューターに接続されている場合、Usbser.sys は自動的には読み込まれません。 ドライバーを読み込むには、**Include** ディレクティブを使用して、モデム INF (mdmcpq.inf) を参照する INF を作成する必要があります。 ディレクティブは、サービスをインスタンス化し、受信トレイ バイナリをコピーし、アプリケーションでデバイスを検索して通信するために必要なデバイス インターフェイス GUID を登録するために必要です。 この INF では、デバイス スタック内の下位フィルター ドライバーとして "Usbser" を指定します。

また、mdmcpq.inf を使用するには、INF で、**Modem** としてデバイス セットアップ クラスを指定する必要があります。 INF の [Version] セクションで、**Modem** とデバイス クラスの GUID を指定します。 詳細については、[システム提供のデバイス セットアップ クラス](https://docs.microsoft.com/previous-versions/ff553419(v=vs.85))に関するページを参照してください。

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

詳細については、[こちらのサポート技術情報の記事](https://support.microsoft.com/help/837637/how-to-use-or-to-reference-the-usbser-sys-driver-from-universal-serial/)を参照してください。

## <a name="configure-selective-suspend-for-usbsersys"></a>Usbser.sys 用にセレクティブ サスペンドを構成する


Windows 10 以降では、Usbser.sys で [USB セレクティブ サスペンド](usb-selective-suspend.md)がサポートされています。 これにより、システムが S0 状態のままになっている間は、接続されている USB シリアル デバイスは、使用されていないときに低電力状態になることができます。 デバイスとの通信が再開されたら、デバイスは中断状態のままにし、動作状態を再開できます。 この機能は、既定では無効になっており、このレジストリ キーの下に **IdleUsbSelectiveSuspendPolicy** エントリを設定することによって有効にし、構成することができます。

**HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Enum\\USB\\&lt;ハードウェア ID&gt;\\&lt;インスタンス ID&gt;\\Device Parameters**

Usbser.sys の電源管理機能を構成する場合は、**IdleUsbSelectiveSuspendPolicy** を次のように設定することができます。

-   "0x00000001"

    アイドル時、つまり、デバイス間でアクティブなデータ転送がない場合は、セレクティブ サスペンドになります。

-   "0x00000000"

    デバイスに対して開いているハンドルがない場合にのみ、セレクティブ サスペンドになります。

このエントリは、次の 2 つの方法のいずれかで追加できます。

-   インストール INF を参照する INF を作成し、**HW.AddReg** セクションにレジストリ エントリを追加します。
-   拡張プロパティの OS 機能記述子にレジストリ エントリを記述します。 **bPropertyName** フィールドを Unicode 文字列 "IdleUsbSelectiveSuspendPolicy" に、**wPropertyNameLength** を 62 バイトに設定するカスタム プロパティ セクションを追加します。 **bPropertyData** フィールドを "0x00000001" または "0x00000000" に設定します。 プロパティ値は、リトルエンディアンの 32 ビット整数として格納されます。

    詳細については、「[Microsoft OS 記述子](https://go.microsoft.com/fwlink/p/?linkid=224878)」を参照してください。

## <a name="develop-windows-applications-for-a-usb-cdc-device"></a>USB CDC デバイス用に Windows アプリケーションを開発する


USB CDC デバイス用の Usbser.sys をインストールする場合、アプリケーション プログラミング モデルのオプションは次のとおりです。

-   Windows 10 以降では、Windows アプリで [**SerialCommunication**](https://docs.microsoft.com/uwp/api/Windows.Devices.SerialCommunication) 名前空間を使用して、Usbser.sys に要求を送信することができます。 シリアル ポート、またはシリアル ポートの何らかの抽象化を介して USB CDC デバイスと通信するために使用できる、Windows ランタイム クラスが定義されます。 クラスでは、このようなシリアル デバイスを検出し、データの読み取りと書き込みを行い、フロー制御のためのシリアル固有のプロパティ (ボー レートの設定、シグナルの状態など) を制御するための機能が提供されます。

-   Windows 8.1 以前のバージョンでは、仮想 COM ポートを開き、デバイスと通信する Windows デスクトップ アプリケーションを作成できます。 詳しくは、次のトピックをご覧ください。

    Win32 プログラミング モデル:

    -   [通信リソースの構成](https://docs.microsoft.com/windows/desktop/DevIO/configuring-a-communications-resource)
    -   [通信のリファレンス](https://docs.microsoft.com/windows/desktop/DevIO/communications-reference)

    .NET Framework プログラミング モデル:

    -   [System.IO.Ports 名前空間](https://docs.microsoft.com/dotnet/api/system.io.ports?redirectedfrom=MSDN)

## <a name="related-topics"></a>関連トピック
[Windows に含まれる USB デバイス クラス ドライバー](supported-usb-classes.md)  
<!-- [How to use or to reference the Usbser.sys driver from universal serial bus (USB) modem .inf files](https://support.microsoft.com/help/837637/how-to-use-or-to-reference-the-usbser-sys-driver-from-universal-serial) -->



