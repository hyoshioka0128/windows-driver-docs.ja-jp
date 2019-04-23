---
Description: USB タイプ C ポート コント ローラー インターフェイス クラス拡張機能の UcmTcpciCx およびクライアント ドライバーは、型-C# の USB ポート コント ローラーに対して実行する必要がありますタスクと呼ばれる動作について説明します。
title: USB Type-C ポート コントローラー ドライバーを記述する
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: b0a35e31f3640f788b69e7bee08d8a9137b96e37
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902432"
---
# <a name="write-a-usb-type-c-port-controller-driver"></a>USB Type-C ポート コントローラー ドライバーを記述する

USB タイプ-c ハードウェア USB 型-c または電源配信 (PD) 物理レイヤーの実装が電源の配信に必要なステート マシンを実装していません型-C# の USB ポート コント ローラーのドライバーを記述する必要があります。 

Windows 10 バージョン 1703、USB 型-C# のアーキテクチャは USB 型-c または電源配信 (PD) 物理レイヤーの実装が、対応する PD ポリシー エンジンまたはプロトコル レイヤーの実装がないハードウェア設計をサポートするために強化されました。 これらの設計では、Windows 10 バージョン 1703 は、ソフトウェア ベース PD ポリシー エンジンとデバイス ポリシー マネージャーを拡張と呼ばれる"USB コネクタ マネージャー型 C ポート コント ローラー インターフェイス クラス"(UcmTcpciCx)、新しいクラス拡張機能を使用を提供します。 IHV または OEM または ODM によって記述されたクライアント ドライバーと通信 UcmTcpciCx PD ポリシー エンジンとデバイス ポリシー マネージャー UcmTcpciCx で関数に必要なハードウェア イベントに関する情報を提供します。 通信は、一連のプログラミングとリファレンス セクションのこのトピックで説明されているインターフェイスを有効になっています。

![usb コネクタ マネージャー](images/tcpci-arch.png)

UcmTcpciCx クラスの拡張機能自体は、UcmCx のクライアント ドライバーです。 電源のコントラクト、データのロールに関するポリシーの決定は UcmCx で行われ、UcmTcpciCx に転送します。 UcmTcpciCx では、これらのポリシーを実装し、UcmTcpciCx クライアント ドライバーによって提供されるポート コント ローラーのインターフェイスを使用して、型 C と PD ステート マシンを管理します。 


**要約**
- UcmTcpci クラスの拡張機能によって提供されるサービス
- クライアント ドライバーの想定される動作

**公式の仕様**
-   [種類 C の USB ポート コント ローラー インターフェイス仕様]
-   [USB 3.1 と USB 型-C# の仕様](https://go.microsoft.com/fwlink/p/?LinkId=699515)
-   [USB 電源配信](https://go.microsoft.com/fwlink/p/?LinkID=623310)

適用対象:

- Windows 10

**WDF のバージョン**

-   KMDF バージョン 1.15

**最終更新日。**

-   2017 年 5 月

**重要な API**

[USB タイプ C ポート コント ローラー インターフェイス ドライバー クラスの拡張機能のリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#type-c-driver-reference)

**UcmTcpciCx クライアント ドライバー テンプレート**

[UcmTcpciCx クライアント ドライバー テンプレート](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmTcpciCxClientSample)

## <a name="before-you-begin"></a>開始する前にしています.

-   によって、ハードウェアまたはファームウェアの PD ステート マシンを実装するかどうかを記述する必要があるドライバーの種類を決定します。 詳細については、次を参照してください。[種類 C の USB コネクタ用の Windows の開発ドライバー](developing-windows-drivers-for-usb-type-c-connectors.md)します。  

-   ターゲット コンピューターまたは Windows 10 Mobile にデスクトップのエディション (Home、Pro、Enterprise、および Education) が型-C# の USB コネクタの使用には、Windows 10 をインストールします。
-   [インストール](https://go.microsoft.com/fwlink/p/?LinkID=845980)開発用コンピューターに最新 Windows Driver Kit (WDK)。 このキットが必要なヘッダー ファイルとライブラリを具体的には、クライアント ドライバーを記述するため、必要があります。

    -   スタブ ライブラリは、(UcmTcpciCxStub.lib)。 ライブラリでは、クライアント ドライバーによって行われた呼び出しを変換し、クラスの拡張機能に渡します。
    -   ヘッダー ファイルでは、UcmTcpciCx.h します。

    クライアント ドライバーでは、カーネル モードで実行され、KMDF 1.15 ライブラリにバインドします。 

    ![ucm の visual studio の構成](images/ucmtcpci-vs.png)

-  クライアント ドライバーがアラートをサポートするかどうかを決定します。

- ポートのコント ローラーを TCPCI に準拠する必要はありません。 インターフェイスは、型 C の任意のポート コント ローラーの機能をキャプチャします。 ハードウェアのレジスタと TCPCI 仕様内のコマンドの意味をマッピングでは単が TCPCI 準拠していないハードウェアの UcmTcpciCx クライアント ドライバーを記述します。 

- ほとんどの TCPCI コント ローラーは<sup>2</sup>C に接続されています。 クライアント ドライバーでは、シリアル ペリフェラル バス (SPB) 接続のリソースおよび、割り込みの行をハードウェアとの通信に使用されます。 ドライバーでは、インターフェイスをプログラミング SPB フレームワーク拡張機能 (SpbCx) を使用します。 について理解を深める SpbCx によってこれらのトピックを参照します。
    - [ドライバーの設計ガイドのシンプルな周辺機器バス (SPB)]
    - [SPB ドライバーのプログラミング リファレンス] 

-   Windows Driver Foundation (WDF) を理解します。 参考資料。[Windows Driver Foundation でのドライバーの開発]( https://go.microsoft.com/fwlink/p/?LinkId=691676)少額 Orwick と Guy Smith によって書き込まれた、します。

## <a name="behavior-of-the-ucmtcpci-class-extension"></a>UcmTcpci クラスの拡張機能の動作

 -  状態のマシンの実行の一環として、UcmTcpciCx は IOCTL 要求をポート コント ローラーに送信します。 たとえば、PD がメッセージングの送信バッファーを設定する IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_TRANSMIT_BUFFER 要求を送信します。 その要求 (TRANSMIT_BUFFER) クライアント ドライバーに渡されます。 ドライバーは、クラスの拡張機能によって提供される詳細情報を送信バッファーを設定します。 

-   UcmTcpciCx は、power コントラクトとデータ ロールに関するポリシーを実装します。  


## <a name="expected-behavior-of-the-client-driver"></a>クライアント ドライバーの想定される動作

UcmTcpciCx クライアント ドライバーが必要です。

-   電源ポリシーの所有者であります。 UcmTcpciCx は、ポート コント ローラーの電源管理に関与しません。 

-   UcmTcpciCx から受信した要求を変換、ハードウェアに読み取りまたは書き込みコマンド。 コマンドは、DPM は、ハードウェア転送が完了するを待つをブロックできないため、非同期である必要があります。  

-   Framework 要求オブジェクトを含むフレームワークのキュー オブジェクトを提供します。 UcmTcpci クラスの拡張機能は、クライアント ドライバーに送信する必要がある各要求に対しては、拡張機能は、ドライバーのキュー オブジェクトの要求オブジェクトを追加します。 ドライバーが完了すると要求の処理、WdfRequestComplete を呼び出します。 適切なタイミングで要求を完了する、クライアント ドライバーの役目です。 

-   検出し、ポート コント ローラーの機能を報告します。 これらの機能で、ポートのコント ローラーが運用する役割などの情報を含める (など、ソースのみ、シンク専用、DRP)。 ただし、コネクタの他の機能があります (機能ストアに関する注意事項を参照してください) と、システム全体を DPM は USB 型-c および PD ポリシーを正しく実装するために知っておく必要があるのです。 たとえば、DPM では、ポート パートナーにそれを提供するシステム/コネクタのソースの機能を把握する必要があります。 

    **機能ストアの注** 
        
    クライアント ドライバーに関連する機能に加え、追加情報と呼ばれるシステム グローバルの場所からは、_機能ストア_します。 このシステム グローバルの機能ストアは、ACPI に格納されます。 システムの機能と、DPM を使用して実装するためにポリシーを決定する、USB 型-c コネクタのそれぞれの静的な記述することをお勧めします。 
      
    ポートのコント ローラーのクライアント ドライバーからシステムの機能の説明を分離するでは、設計は、さまざまな機能のさまざまなシステムで使用するドライバーを許可します。 機能ストアと UcmCx、いないの UcmTcpciCx インターフェイス。 UcmTcpciCx (またはそのクライアント ドライバー) は、機能ストアと対話しません。 
      
    可能な機能ストアからの情報は、ポート コント ローラーのクライアント ドライバーから直接送信される情報をオーバーライドします。 たとえば、ポートのコント ローラーがシンク専用の操作に対応し、クライアント ドライバーは、その情報を報告します。 ただし、システムの残りの部分が正しく構成されていないシンク専用の操作。 その場合は、システムの製造元は、コネクタは機能ストア内のソース専用の操作の機能をレポートできます。 ドライバーには、機能ストアの優先設定は、情報を報告します。 

-   アラートに関連するすべての関連データで UcmTcpciCx を通知します。 
 
-   (省略可能)。 別のモードが入力された終了後に余分な処理を実行します。 ドライバーは、IOCTL 要求を通じてクラスの拡張機能によって、それらの状態について通知されます。 


## <a name="1-register-the-client-driver-with-ucmtcpcicx"></a>1. クライアント ドライバーに UcmTcpciCx 登録します。

サンプルの参照。参照してください`EvtPrepareHardware`で`Device.cpp`します。

1.  EVT_WDF_DRIVER_DEVICE_ADD 実装 UcmTcpciDeviceInitInitialize WDFDEVICE_INIT 非透過構造体を初期化するために呼び出します。 呼び出しは、クライアント ドライバーをフレームワークに関連付けます。

2.  Framework デバイス オブジェクト (WDFDEVICE) を作成したら、UcmTcpciCx クライアント ドライバーに登録する UcmTcpciDeviceInitialize を呼び出します。

## <a name="2-initialize-the-i2c-communications-channel-to-the-port-controller-hardware"></a>2. ポートのコント ローラーのハードウェア、I2C 通信チャネルを初期化します。

サンプルの参照。参照してください`EvtCreateDevice`で`Device.cpp`します。

EVT_WDF_DEVICE_PREPARE_HARDWARE 実装、通信チャネルを開くためのハードウェア リソースを読み取ります。 これは、PD 機能を取得し、アラートに関する通知を受け取るに必要です。 

ほとんどの TCPCI コント ローラーは<sup>2</sup>C に接続されています。 参照サンプルでは、クライアント ドライバーを開きは<sup>2</sup> SPB フレームワーク拡張 (SpbCx) のプログラミング インターフェイスを使用してチャネル。 

クライアント ドライバーでは、WdfCmResourceListGetDescriptor を呼び出すことによって、ハードウェア リソースを列挙します。 

アラートは、割り込みとして受信されます。 そのため、ドライバーは framework 割り込みオブジェクトを作成し、アラートを処理する ISR を登録します。  ISR 読み取りハードウェアとハードウェアへのアクセスが完了するまでブロックする書き込み操作を実行します。 待機が DIRQL で受け入れられないため、ドライバーは PASSIVE_LEVEL の ISR を実行します。 


## <a name="3-initialize-the-port-controllers-type-c-and-pd-capabilities"></a>3.ポートのコント ローラーの種類 C および PD 機能を初期化します。
    
サンプルの参照。参照してください`EvtDeviceD0Entry`で`Device.cpp`します。


 で、EVT_WDF_DEVICE_D0_EXIT の実装 
 
 1. ポートのコント ローラー ハードウェアと通信し、さまざまなレジスタを読み取ることによって、デバイス identificaton と機能を取得します。 
 
 2. 取得した情報を UCMTCPCI_PORT_CONTROLLER_IDENTIFICATION と UCMTCPCI_PORT_CONTROLLER_CAPABILITIES を初期化します。 

 3. UCMTCPCI_PORT_CONTROLLER_CONFIG_INIT に初期化された構造体を渡すことによって、上記の情報を使用した UCMTCPCI_PORT_CONTROLLER_CONFIG 構造を初期化します。

 4. ポートのコント ローラー オブジェクトを作成および UCMTCPCIPORTCONTROLLER ハンドルを取得する UcmTcpciPortControllerCreate を呼び出します。

## <a name="4-set-up-a-framework-queue-object-for-receiving-requests-from-ucmtcpcicx"></a>4。UcmTcpciCx から要求を受信するためのフレームワーク キュー オブジェクトを設定します。

サンプルの参照。参照してください`EvtDeviceD0Entry`で`Device.cpp`と`HardwareRequestQueueInitialize`で`Queue.cpp`します。

 1. EVT_WDF_DEVICE_D0_EXIT 実装では、WdfIoQueueCreate を呼び出すことによって、framework のキュー オブジェクトを作成します。 その呼び出しでは、UcmTpciCx から送信された IOCTL 要求を処理するために、コールバックの実装を登録する必要があります。 クライアント ドライバーでは、電源管理対象のキューを使用できます。 

    、型 C と PD ステート マシンの実行中には、UcmTpciCx はコマンドを実行するクライアント ドライバーに送信されます。 UcmTcpciCx があることで最も未処理ポート コント ローラーの 1 つの要求で、特定の時点を保証します。  
 
 2. UcmTpciCx を新しいフレームワークのキュー オブジェクトを登録する UcmTcpciPortControllerSetHardwareRequestQueue を呼び出します。 その呼び出しが成功すると、UcmTcpciCx は、ドライバーからアクションを必要とする場合、このキューに framework キュー オブジェクト (WDFREQUEST) を配置します。 

 3. これらの Ioctl を処理するために EvtIoDeviceControl コールバック関数を実装します。 

|  制御コード |  説明 | 
|---            |           ---|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_GET_STATUS|   ユニバーサル シリアル バスの種類 C ポート コント ローラー インターフェイス仕様に従ってすべてのステータス レジスタの値を取得します。 クライアント ドライバーでは、CC_STATUS、POWER_STATUS、および FAULT_STATUS レジスタの値を取得する必要があります。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_GET_CONTROL|ユニバーサル シリアル バスの種類 C ポート コント ローラー インターフェイス仕様に従って定義されているすべてのコントロール レジスタの値を取得します。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_CONTROL|ユニバーサル シリアル バスの種類 C ポート コント ローラー インターフェイス仕様に従って定義されているコントロール レジスタの値を設定します。| 
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_TRANSMIT|セットの送信の登録、ユニバーサル シリアル バス型 C ポート コント ローラー インターフェイス仕様に従って定義されています。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_TRANSMIT_BUFFER|セット TRANSMIT_BUFER 登録、ユニバーサル シリアル バス型 C ポート コント ローラー インターフェイス仕様に従って定義されています。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_RECEIVE_DETECT|セット RECEIVE_DETECT 登録、ユニバーサル シリアル バス型 C ポート コント ローラー インターフェイス仕様に従って定義されています。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_CONFIG_STANDARD_OUTPUT|セット CONFIG_STANDARD_OUTPUT 登録、ユニバーサル シリアル バス型 C ポート コント ローラー インターフェイス仕様に従って定義されています。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_COMMAND|ユニバーサル シリアル バスの種類 C ポート コント ローラー インターフェイス仕様に従って定義されているコマンドのレジスタの値を設定します。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_MESSAGE_HEADER_INFO|セット、ユニバーサル シリアル バス型 C ポート コント ローラー インターフェイス仕様に従って MESSAGE_HEADER_INFO 登録の値が定義されています。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_ALTERNATE_MODE_ENTERED|ドライバーは、その他のタスクを実行できるように、別のモードが入力されているクライアント ドライバーに通知します。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_ALTERNATE_MODE_EXITED|ドライバーは、その他のタスクを実行できるように、別のモードが終了していることをクライアント ドライバーに通知します。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_CONFIGURED|ドライバーは、その他のタスクを実行できるように、パートナー デバイスのディスプレイ ポート等代替モードが暗証番号 (pin) が割り当てられた構成されているクライアント ドライバーに通知します。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_HPD_STATUS_CHANGED|ホット プラグは、ディスプレイ ドライバーは、その他のタスクを実行できるように、接続が変更されたポートの状態を検出するクライアント ドライバーに通知します。|

4. UcmTcpciCx ポート コント ローラーを起動するように指示する UcmTcpciPortControllerStart を呼び出します。 UcmTcpciCx には、USB 型-C# と電源の配信の制御が想定しています。 ポートのコント ローラーを開始すると、UcmTcpciCx がハードウェアの要求キューに要求を配置することを開始することがあります。 

 
## <a name="5-handlle-alerts-from-the-port-controller-hardware"></a>5。ポートのコント ローラー ハードウェアから Handlle アラート

サンプルの参照。参照してください`ProcessAndSendAlerts`で`Alert.cpp`します。

クライアント ドライバーは、ポートのコント ローラー ハードウェアから受信したアラート (またはイベント) を処理し、イベントに関連するデータを UcmTcpciCx に送信する必要があります。 

ハードウェアのアラートが発生したときに、ポートのコント ローラー ハードウェア ドライブ アラートが高にピン留めします。 これは、場合、クライアント (手順 2. で登録) ドライバーの ISR 呼び出されます。 ルーチンは PASSIVE_LEVEL のハードウェア割り込みをサービスします。 ルーチンの場合、割り込みがポートのコント ローラー ハードウェア; からのアラートであるかどうかそうである場合、アラートの処理が完了し、UcmTcpciPortControllerAlert を呼び出すことによって UcmTcpciCx を通知します。 

UcmTcpciPortControllerAlert を呼び出す前に、クライアントは UCMTCPCI_PORT_CONTROLLER_ALERT_DATA 構造内のアラートに関連するすべての関連するデータを含む責任を負います。 クライアントは、ハードウェアのアサートで複数のアラートが同時に処理でした可能性があるため、アクティブになっているすべてのアラートの配列を提供します。 

[Cc] 状態の変化にレポート タスクのフローの例を次に示します。 

1. クライアントは、ハードウェアのアラートを受信します。 

2. クライアントは、アラートの登録を読み取るし、アクティブになっている種類のアラートを決定します。 

3. クライアントは、[cc] ステータス レジスタを読み取って、UCMTCPCI_PORT_CONTROLLER_ALERT_DATA で CC ステータス レジスタの内容について説明します。 ドライバーは、UcmTcpciPortControllerAlertCCStatus AlertType メンバーとレジスタの CCStatus メンバーを設定します。

4. クライアントが呼び出す UcmPortControllerAlert UcmTcpciCx にアレイ ハードウェアのアラートを送信します。 

5. クライアントは、(クライアントは、アラートの情報を取得した後、いつでも発生する可能性があります)、アラートをクリアします。 

## <a name="6-process-requests-received-from-ucmtcpcicx"></a>6。UcmTcpciCx から受信した要求の処理

サンプルの参照。「`PortControllerInterface.cpp`」を参照してください。

状態のマシンの実行の一環として、UcmTcpciCx はポート コント ローラーに要求を送信する必要があります。 たとえば、TRANSMIT_BUFFER を設定する必要があります。 この要求のクライアント ドライバーに渡されます。 ドライバーは、UcmTcpciCx によって提供される詳細情報の送信バッファーを設定します。 それらの要求のほとんどは、ハードウェアの読み取りに変換またはクライアント ドライバーによって記述します。 コマンドは、DPM は、ハードウェアの転送が完了するを待つをブロックできませんので、非同期である必要があります。

UcmTcpciCx は、クライアント ドライバーから必要な取得/設定操作を記述する場合の I/O 制御コードとしてのコマンドを送信します。 クライアント ドライバーのキューのセットアップは、ドライバーは、そのキューを UcmTcpciCx に登録します。  Framework 要求オブジェクトをキューに配置する UcmTcpciCx 開始ドライバーからの操作が必要です。 I/O 制御コードは、手順 4. でテーブルに表示されます。

適切なタイミングで要求を完了する、クライアント ドライバーの役目です。

クライアント ドライバーは、要求された操作が完了したら、framework 要求オブジェクトを表す完了状態で WdfRequestComplete を呼び出します。 

クライアント ドライバーは、ハードウェアの操作を実行する別のドライバーに、I/O 要求を送信する必要があります。 たとえば、サンプルでは、ドライバー、要求を送信します SPB に<sup>2</sup>C に接続されているポートのコント ローラー。 その場合は、ドライバーは、要求オブジェクト WDM IRP スタックの場所の正しい番号があるないため、UcmTcpciCx から受け取った framework 要求オブジェクトを転送できません。 クライアント ドライバーは、別のフレームワーク要求オブジェクトを作成し、別のドライバーに転送する必要があります。 クライアント ドライバー UcmTcpciCx から要求を取得するたびに作成する代わりに、初期化中に必要な要求オブジェクトを事前に割り当てることができます。 UcmTcpciCx 保証がある 1 つだけ要求未処理任意の時点であるために、可能です。 

## <a name="see-also"></a>参照
[USB タイプ C ポート コント ローラー インターフェイス ドライバー クラスの拡張機能のリファレンス](https://msdn.microsoft.com/library/windows/hardware/mt805826)
