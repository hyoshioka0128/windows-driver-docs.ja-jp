---
Description: Microsoft から提供されたインボックス ドライバー (Usbser.sys) 通信および CDC 制御デバイスの。
title: USB シリアル ドライバー (Usbser.sys)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fff60502b51bf4e670f5d3e92c6044a6e338611d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385063"
---
# <a name="usb-serial-driver-usbsersys"></a>USB シリアル ドライバー (Usbser.sys)


**最終更新日**

-   2015 年 4 月

* * OS バージョン * *

-   Windows 10
-   Windows 8.1

**適用対象**

-   CDC 制御デバイスのデバイスの製造元

Microsoft から提供されたインボックス ドライバー (Usbser.sys) 通信および CDC 制御デバイスの。

Windows 10 を使用して、ドライバーが書き換えられましたが、[カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)ドライバーの全体的な安定性を向上します。

-   (など、処理の突然の取り外し) ドライバーでの PnP や電源管理を向上します。
-   電源管理機能の追加をなど[USB セレクティブ サスペンド](usb-selective-suspend.md)します。

さらに、UWP アプリケーションには、新しいで提供される Api が使用できますようになりました[ **Windows.Devices.SerialCommunication** ](https://msdn.microsoft.com/library/windows/apps/dn921817)これらのデバイスとの対話にアプリを許可する名前空間。

## <a name="usbsersys-installation"></a>Usbser.sys インストール


Microsoft から提供されたボックスでのドライバーを読み込む (Usbser.sys) 通信および CDC 制御デバイスです。

**注**  を Windows に含まれる USB デバイス クラス ドライバーをインストールしようとする必要はありません、ドライバーをダウンロードする場合。 自動的にインストールされます。 これらは自動的にインストールされていない場合、は、デバイスの製造元に問い合わせてください。 Windows に含まれる USB デバイス クラス ドライバーの一覧で、次を参照してください。 [USB デバイス クラス ドライバーが Windows に含まれる](supported-usb-classes.md)します。

 

**Windows 10**

%Systemroot% に追加された新しい INF、Usbser.inf、Windows 10 で\\Inf Usbser.sys をデバイス スタックの関数デバイス オブジェクト (FDO) として読み込まれる。 デバイスは、通信と、CDC 制御デバイス クラスに属する、Usbser.sys が自動的に読み込まれます。ドライバーを参照する、独自の INF を記述する必要はありません。 ドライバーはのような互換性のある ID 一致に基づいて読み込まれて[Windows に含まれるその他の USB デバイス クラス ドライバー](supported-usb-classes.md)します。

`USB\Class_02`

`USB\Class_02&SubClass_02`

-   Usbser.sys を自動的に読み込む場合は、02 に、クラスのコードに 02 とサブクラス コードを設定、[デバイス記述子](usb-device-descriptors.md)します。 詳細については、USB 通信デバイス クラス (または USB CDC) を参照してくださいで仕様が検出された、 [USB DWG web サイト](https://go.microsoft.com/fwlink/p/?linkid=617741)します。 このアプローチでは、システムは Usbser.inf を使用するために、デバイスの INF ファイルを配布する必要はありません。
-   デバイス クラスのコード 02 02 以外のサブクラス コード値が指定されている場合、Usbser.sys が自動的に読み込まれません。 Pnp マネージャーは、ドライバーを検索しようとします。 適切なドライバーが見つからない場合、デバイスは読み込まれるドライバーがあります。 ここでは、独自のドライバーの読み込みまたは別のインボックス ドライバーを参照する、INF を記述する必要があります。
-   デバイスに 02、クラスとサブクラスのコードを指定します Usbser.sys ではなく別のドライバーをロードする場合は、デバイスとドライバーをインストールするハードウェア ID を指定する、INF を記述する必要があります。 含まれている INF ファイルを検索する例については、[サンプル ドライバー](https://go.microsoft.com/fwlink/p/?LinkId=534087)とデバイスのようなデバイスを探します。 INF セクションについては、次を参照してください。 [INF ファイルの概要](https://msdn.microsoft.com/library/windows/hardware/ff549520)します。

**注**  Microsoft が可能であれば、インボックス ドライバーを使用することをお勧めします。 Windows、Windows 10 Mobile などのモバイルのエディションでは、オペレーティング システムの一部であるドライバーのみが読み込まれます。 デスクトップのエディションとは異なり、外部のドライバー パッケージからドライバーを読み込むことはできません。 新しいインボックス INF で Usbser.sys はモバイル デバイスの USB-シリアル デバイスが検出された場合は自動的に読み込まれます。

 

**Windows 8.1 と以前のバージョン**

Windows 8.1 およびそれ以前のバージョンのオペレーティング システムで Usbser.sys が自動的に読み込まれていない USB-シリアル デバイスがコンピューターに関連付けられている場合。 ドライバーを読み込むを使用して、モデムの INF (mdmcpq.inf) を参照する、INF を書き込む必要があります、 **Include**ディレクティブ。 ディレクティブは、サービスをインスタンス化し、受信トレイのバイナリをコピーして、デバイス インターフェイス、デバイスを見つけてと対話するアプリケーションを必要とする GUID を登録する必要があります。 その INF では、デバイス スタックの下位のフィルター ドライバーとして"Usbser"を指定します。

としてデバイス セットアップ クラスを指定することも必要があります、INF**モデム**mdmcpq.inf を使用します。 [バージョン] セクションで、INF の指定、**モデム**とデバイス クラス GUID です。 詳細については、次を参照してください。 [System-Supplied デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff553419)します。

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

詳細については、次を参照してください。[このサポート技術情報記事](https://support.microsoft.com/kb/837637/)します。

## <a name="configure-selective-suspend-for-usbsersys"></a>選択的構成 Usbser.sys を中断


Windows 10 以降、Usbser.sys サポート[USB セレクティブ サスペンド](usb-selective-suspend.md)します。 これにより、接続している USB-シリアル デバイス、システムの S0 状態のまま使用しない場合は低電力状態にできます。 デバイスとの通信が再開したとき、デバイスは中断状態のままにし、状態の作業を再開できます。 機能は既定で無効および有効になっているおよび構成できるようを設定して、 **IdleUsbSelectiveSuspendPolicy**このレジストリ キーの下のエントリ。

**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\Enum\\USB\\&lt;ハードウェア id&gt; \\ &lt;インスタンス id&gt;\\デバイス パラメーター**

設定することができます Usbser.sys の電源管理機能を構成する**IdleUsbSelectiveSuspendPolicy**に。

-   "0x00000001"

    選択的に入力したときに中断する、またはデバイスからのアクティブなデータ転送がない場合に、アイドルです。

-   "0x00000000"

    選択的入力デバイスを開いているハンドルがない場合にのみを中断します。

2 つの方法のいずれかでは、そのエントリを追加できます。

-   インストール INF を参照する、INF を記述し、レジストリ エントリを追加、 **HW。AddReg**セクション。
-   OS の拡張プロパティの機能記述子でレジストリ エントリをについて説明します。 設定するカスタム プロパティ セクションを追加、 **bPropertyName**に Unicode 文字列では、"IdleUsbSelectiveSuspendPolicy"フィールドと**wPropertyNameLength** 62 バイトにします。 設定、 **bPropertyData**フィールドを"0x00000001"または"0x00000000"。 プロパティの値は、リトル エンディアンの 32 ビット整数として格納されます。

    詳細については、次を参照してください。 [Microsoft OS ディスクリプター](https://go.microsoft.com/fwlink/p/?linkid=224878)します。

## <a name="develop-windows-applications-for-a-usb-cdc-device"></a>CDC の USB デバイス用の Windows アプリケーションを開発します。


CDC の USB デバイスの Usbser.sys をインストールする場合、アプリケーションのプログラミング モデルのオプションを示します。

-   Windows 10 以降、Windows アプリに要求を送信 Usbser.sys を使用して、 [ **Windows.Devices.SerialCommunication** ](https://msdn.microsoft.com/library/windows/apps/dn921817)名前空間。 シリアル ポートまたはシリアル ポートのいくつかの抽象化を使用して CDC の USB デバイスとの通信に使用できる Windows ランタイム クラスを定義します。 クラスは、このようなシリアル デバイスを検出、読み取り、データを書き込むよう機能を提供し、ボー レートの設定など、フロー制御シリアル固有のプロパティをコントロールの状態を通知します。

-   Windows 8.1 以前のバージョンでは、仮想 COM ポートを開き、デバイスと通信する Windows デスクトップ アプリケーションを記述できます。 詳しくは、次のトピックをご覧ください。

    Win32 のプログラミング モデル:

    -   [通信のリソースを構成します。](https://msdn.microsoft.com/library/windows/desktop/aa363201)
    -   [通信の参照](https://msdn.microsoft.com/library/windows/desktop/aa363195)

    .NET framework のプログラミング モデル:

    -   [System.IO.Ports Namespace](https://msdn.microsoft.com/library/System.IO.Ports.aspx)

## <a name="related-topics"></a>関連トピック
[Windows に含まれる USB デバイス クラス ドライバー](supported-usb-classes.md)  
<!-- [How to use or to reference the Usbser.sys driver from universal serial bus (USB) modem .inf files](https://support.microsoft.com/help/837637/how-to-use-or-to-reference-the-usbser.sys-driver-from-universal-serial-bus-usb-modem-.inf-files) -->



