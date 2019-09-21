---
Description: "\"UcmTcpciCx\" と呼ばれる USB タイプ C ポートコントローラーインターフェイスクラス拡張の動作と、クライアントドライバーが USB タイプ C ポートコントローラーに対して実行する必要があるタスクについて説明します。"
title: USB Type-C ポート コントローラー ドライバーを記述する
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 54cb8e485e762f8a2d81e4cec5f43de800d64ba9
ms.sourcegitcommit: ee1fc949d1ae5eb14df4530758f767702a886e36
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2019
ms.locfileid: "71164792"
---
# <a name="write-a-usb-type-c-port-controller-driver"></a>USB Type-C ポート コントローラー ドライバーを記述する

Usb タイプ c ハードウェアが usb タイプ c または電力配信 (PD) 物理レイヤーを実装していても、電力配信に必要なステートマシンが実装されていない場合は、USB タイプ c ポートコントローラードライバーを作成する必要があります。 

Windows 10 バージョン1703では、usb タイプ c または電力配信 (PD) 物理レイヤーを実装しているが、対応する PD ポリシーエンジンやプロトコルレイヤーの実装がないハードウェア設計をサポートするように、USB タイプ C アーキテクチャが改善されました。 これらの設計では、Windows 10 バージョン1703では、ソフトウェアベースの PD ポリシーエンジンとデバイスポリシーマネージャーが "USB コネクタマネージャータイプ-C ポートコントローラーインターフェイスクラス拡張" (UcmTcpciCx) という名前の新しいクラス拡張を使用して提供されます。 IHV または OEM/ODM によって記述されたクライアントドライバーは、UcmTcpciCx と通信して、UcmTcpciCx で機能するために必要なハードウェアイベントに関する情報を提供します。 この通信は、このトピックとリファレンスセクションで説明する一連のプログラミングインターフェイスによって有効になります。

![usb コネクタマネージャー](images/tcpci-arch.png)

UcmTcpciCx クラス拡張は、それ自体が UcmCx のクライアントドライバーです。 Power contracts、データロールに関するポリシーの決定は UcmCx で行われ、UcmTcpciCx に転送されます。 UcmTcpciCx は、これらのポリシーを実装し、UcmTcpciCx クライアントドライバーによって提供されるポートコントローラーインターフェイスを使用して、タイプ C と PD のステートマシンを管理します。 


**概要**
- UcmTcpci クラス拡張機能によって提供されるサービス
- クライアントドライバーの予期される動作

**公式の仕様**
-   [USB タイプ-C ポートコントローラーインターフェイス仕様]
-   [USB 3.1 および USB タイプ-C 仕様](https://go.microsoft.com/fwlink/p/?LinkId=699515)
-   [USB 電源配布](https://go.microsoft.com/fwlink/p/?LinkID=623310)

適用対象:

- Windows 10

**WDF のバージョン**

-   KMDF バージョン1.15

**最終更新日時:**

-   2017 年 5 月

**重要な API**

[USB タイプ-C ポートコントローラーインターフェイスドライバークラス拡張のリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#type-c-driver-reference)

**UcmTcpciCx クライアントドライバーテンプレート**

[UcmTcpciCx クライアントドライバーテンプレート](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmTcpciCxClientSample)

## <a name="before-you-begin"></a>開始する前に...

-   ハードウェアまたはファームウェアが PD ステートマシンを実装しているかどうかに応じて、書き込む必要があるドライバーの種類を決定します。 詳細については、「 [USB タイプの Windows ドライバーの開発-C コネクタ](developing-windows-drivers-for-usb-type-c-connectors.md)」を参照してください。  

-   Windows 10 for desktop エディション (Home、Pro、Enterprise、および教育) を、USB C コネクタを使用して、対象のコンピューターまたは Windows 10 Mobile にインストールします。
-   開発用コンピューターに最新の Windows Driver Kit (WDK) を[インストール](https://go.microsoft.com/fwlink/p/?LinkID=845980)します。 キットには、クライアントドライバーを記述するために必要なヘッダーファイルとライブラリが用意されています。具体的には、次のものが必要です。

    -   スタブライブラリ (UcmTcpciCxStub .lib)。 ライブラリは、クライアントドライバーによって行われた呼び出しを変換し、クラス拡張に渡します。
    -   ヘッダーファイル UcmTcpciCx .h。

    クライアントドライバーはカーネルモードで実行され、KMDF 1.15 ライブラリにバインドされます。 

    ![ucm の visual studio の構成](images/ucmtcpci-vs.png)

-  クライアントドライバーがアラートをサポートするかどうかを決定します。

- ポートコントローラーは、TCPCI に準拠している必要はありません。 インターフェイスは、すべてのタイプ C ポートコントローラーの機能をキャプチャします。 TCPCI に準拠していないハードウェア用に UcmTcpciCx クライアントドライバーを作成することは、TCPCI 仕様のレジスタとコマンドの意味をハードウェアのものにマップするだけです。 

- ほとんどの TCPCI コントローラーは、I<sup>2</sup>C に接続されています。 クライアントドライバーは、シリアル周辺機器バス (SPB) 接続リソースと割り込み回線を使用して、ハードウェアと通信します。 ドライバーは、SPB フレームワーク拡張 (SpbCx) プログラミングの機能を使用します。 SpbCx について理解するには、次のトピックを参照してください。
    - [シンプルな周辺機器バス (SPB) ドライバー設計ガイド]
    - [SPB ドライバープログラミングリファレンス] 

-   Windows Driver Foundation (WDF) について理解を深めます。 推奨される読み取り:[Windows Driver Foundation でのドライバーの開発]( https://go.microsoft.com/fwlink/p/?LinkId=691676)。これは、少額 Orwick と Guy Smith によって記述されています。

## <a name="behavior-of-the-ucmtcpci-class-extension"></a>UcmTcpci クラス拡張の動作

 -  ステートマシンの実行の一環として、UcmTcpciCx は IOCTL 要求をポートコントローラーに送信します。 たとえば、PD messaging では、送信バッファーを設定する IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_TRANSMIT_BUFFER 要求を送信します。 この要求 (TRANSMIT_BUFFER) は、クライアントドライバーに渡されます。 次に、ドライバーは、クラス拡張によって提供される詳細を使用して、送信バッファーを設定します。 

-   UcmTcpciCx は、電源コントラクト、データロールなどに関するポリシーを実装します。  


## <a name="expected-behavior-of-the-client-driver"></a>クライアントドライバーの予期される動作

UcmTcpciCx へのクライアントドライバーは、次のことを想定しています。

-   電源ポリシーの所有者である。 UcmTcpciCx は、ポートコントローラーの電源管理に参加していません。 

-   UcmTcpciCx から受信した要求を、ハードウェアの読み取りコマンドまたは書き込みコマンドに変換します。 DPM はハードウェア転送の完了を待つことができないため、コマンドを非同期にする必要があります。  

-   フレームワークの要求オブジェクトを格納するフレームワークキューオブジェクトを指定します。 UcmTcpci クラス拡張がクライアントドライバーに送信する要求ごとに、拡張機能によって、要求オブジェクトがドライバーの queue オブジェクトに追加されます。 ドライバーが要求の処理を完了すると、WdfRequestComplete が呼び出されます。 要求を適切なタイミングで完了するのは、クライアントドライバーの役割です。 

-   ポートコントローラーの機能を検出して報告します。 これらの機能には、ポートコントローラーが動作できるロール (ソースのみ、シンク専用、DRP など) などの情報が含まれます。 ただし、コネクタには、USB タイプ C および PD ポリシーを適切に実装するために必要な機能があります (機能ストアに関するメモを参照してください)。また、システム全体についても説明します。 たとえば、DPM は、ポートパートナーに提供するために、システム/コネクタのソース機能を認識している必要があります。 

    **メモ機能ストア** 
        
    クライアントドライバーに関連する機能に加えて、追加情報は、_機能ストア_と呼ばれるシステムグローバルな場所から取得されます。 このシステムグローバル機能ストアは、ACPI に格納されています。 これは、システムの機能の静的な説明であり、DPM が実装するポリシーを決定するために使用するそれぞれの USB タイプ C コネクタです。 
      
    システム機能の説明をポートコントローラーのクライアントドライバーから分離することにより、さまざまな機能を持つさまざまなシステムでドライバーを使用できるようになります。 UcmTcpciCx ではなく UcmCx は、機能ストアとのインターフェイスを備えています。 UcmTcpciCx (またはそのクライアントドライバー) は、機能ストアと対話しません。 
      
    該当する場合、機能ストアの情報は、ポートコントローラークライアントドライバーから直接取得された情報を上書きします。 たとえば、ポートコントローラーはシンクのみの操作が可能であり、クライアントドライバーはその情報を報告します。 ただし、システムの残りの部分は、シンクのみの操作に対して正しく構成されていない可能性があります。 この場合、システムの製造元は、コネクタが機能ストアでソースのみの操作に対応していることを報告できます。 機能ストアの設定は、ドライバーによって報告された情報よりも優先されます。 

-   アラートに関連するすべての関連データを使用して、UcmTcpciCx に通知します。 
 
-   任意。 別のモードを入力または終了した後で、追加の処理を実行します。 ドライバーは、IOCTL 要求によって、クラス拡張によってこれらの状態について通知されます。 


## <a name="1-register-the-client-driver-with-ucmtcpcicx"></a>1. クライアントドライバーを UcmTcpciCx に登録する

サンプルリファレンス:「 `EvtPrepareHardware` 」 `Device.cpp`の「」を参照してください。

1.  EVT_WDF_DRIVER_DEVICE_ADD 実装で、UcmTcpciDeviceInitInitialize を呼び出して、WDFDEVICE_INIT 不透明構造体を初期化します。 この呼び出しにより、クライアントドライバーがフレームワークに関連付けられます。

2.  フレームワークデバイスオブジェクト (WDFDEVICE) を作成した後、UcmTcpciDeviceInitialize を呼び出してクライアントのダイバーを Ucmtcpcideviceinitialize に登録します。

## <a name="2-initialize-the-i2c-communications-channel-to-the-port-controller-hardware"></a>2. I2C 通信チャネルをポートコントローラーハードウェアに初期化します。

サンプルリファレンス:「 `EvtCreateDevice` 」 `Device.cpp`の「」を参照してください。

EVT_WDF_DEVICE_PREPARE_HARDWARE 実装では、ハードウェアリソースを読み、通信チャネルを開きます。 これは、PD 機能を取得し、アラートに関する通知を受け取るために必要です。 

ほとんどの TCPCI コントローラーは、I<sup>2</sup>C に接続されています。 参照サンプルでは、クライアントドライバーは、SPB フレームワーク拡張 (SpbCx) プログラミングの機能を使用して I<sup>2</sup>チャネルを開きます。 

クライアントドライバーは、WdfCmResourceListGetDescriptor を呼び出すことによって、ハードウェアリソースを列挙します。 

アラートは割り込みとして受信されます。 このため、ドライバーはフレームワークの interrupt オブジェクトを作成し、アラートを処理する ISR を登録します。  ISR は、ハードウェアへのアクセスが完了するまでブロックするハードウェアの読み取りおよび書き込み操作を実行します。 待機は DIRQL では許容されないため、ドライバーは PASSIVE_LEVEL で ISR を実行します。 


## <a name="3-initialize-the-port-controllers-type-c-and-pd-capabilities"></a>3.ポートコントローラーのタイプ C と PD の機能を初期化します。
    
サンプルリファレンス:「 `EvtDeviceD0Entry` 」 `Device.cpp`の「」を参照してください。


 EVT_WDF_DEVICE_D0_EXIT 実装では、 
 
 1. さまざまなレジスタを読み取って、ポートコントローラーハードウェアと通信し、デバイスの識別子と機能を取得します。 
 
 2. 取得した情報を使用して、UCMTCPCI_PORT_CONTROLLER_IDENTIFICATION と UCMTCPCI_PORT_CONTROLLER_CAPABILITIES を初期化します。 

 3. 初期化された構造体を UCMTCPCI_PORT_CONTROLLER_CONFIG_INIT に渡すことによって、前の情報で UCMTCPCI_PORT_CONTROLLER_CONFIG 構造体を初期化します。

 4. Ucmtcpciportcontroller Create を呼び出して、ポートコントローラーオブジェクトを作成し、UCMTCPCIPORTCONTROLLER ハンドルを取得します。

## <a name="4-set-up-a-framework-queue-object-for-receiving-requests-from-ucmtcpcicx"></a>4。UcmTcpciCx からの要求を受信するためのフレームワークキューオブジェクトを設定する

サンプルリファレンス:「」 `EvtDeviceD0Entry` および`HardwareRequestQueueInitialize`「 」の`Queue.cpp`「」を参照してください。 `Device.cpp`

 1. EVT_WDF_DEVICE_D0_EXIT 実装で、WdfIoQueueCreate を呼び出してフレームワークキューオブジェクトを作成します。 この呼び出しでは、UcmTpciCx によって送信された IOCTL 要求を処理するために、コールバックの実装を登録する必要があります。 クライアントドライバーは、電源管理キューを使用する場合があります。 

    タイプ C と PD のステートマシンの実行中に、UcmTpciCx はコマンドをクライアントドライバーに送信して実行します。 UcmTcpciCx では、特定の時点で未解決のポートコントローラー要求が1つしかないことが保証されます。  
 
 2. UcmTcpciPortControllerSetHardwareRequestQueue を呼び出して、UcmTpciCx に新しいフレームワークキューオブジェクトを登録します。 この呼び出しが成功すると、UcmTcpciCx は、ドライバーからのアクションが必要なときに、このキューにフレームワークキューオブジェクト (WDFREQUEST) を配置します。 

 3. これらの Ioctl を処理するには、EvtIoDeviceControl callback 関数を実装します。 

|  制御コード |  説明 | 
|---            |           ---|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_GET_STATUS|   すべてのステータスレジスタの値を取得します。これは、ユニバーサルシリアルバスタイプ C ポートコントローラーインターフェイス仕様に従います。 クライアントドライバーは、CC_STATUS、POWER_STATUS、および FAULT_STATUS の各レジスタの値を取得する必要があります。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_GET_CONTROL|ユニバーサルシリアルバスタイプ C ポートコントローラーインターフェイス仕様に従って定義されたすべてのコントロールレジスタの値を取得します。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_CONTROL|ユニバーサルシリアルバスタイプ C ポートコントローラーインターフェイスの仕様に従って定義されたコントロールレジスタの値を設定します。| 
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_TRANSMIT|ユニバーサルシリアルバスタイプ C ポートコントローラーの仕様に従って定義された送信レジスタを設定します。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_TRANSMIT_BUFFER|ユニバーサルシリアルバスタイプ C ポートコントローラーの仕様に従って定義された TRANSMIT_BUFER レジスタを設定します。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_RECEIVE_DETECT|ユニバーサルシリアルバスタイプ C ポートコントローラーの仕様に従って定義された RECEIVE_DETECT レジスタを設定します。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_CONFIG_STANDARD_OUTPUT|ユニバーサルシリアルバスタイプ C ポートコントローラーの仕様に従って定義された CONFIG_STANDARD_OUTPUT レジスタを設定します。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_COMMAND|ユニバーサルシリアルバスタイプ-C ポートコントローラーのインターフェイス仕様に従って定義されたコマンドレジスタの値を設定します。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_MESSAGE_HEADER_INFO|ユニバーサルシリアルバスタイプ C ポートコントローラーの仕様に従って定義された MESSAGE_HEADER_INFO Register の値を設定します。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_ALTERNATE_MODE_ENTERED|ドライバーが追加のタスクを実行できるように、代替モードが入力されたことをクライアントドライバーに通知します。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_ALTERNATE_MODE_EXITED|ドライバーが追加のタスクを実行できるように、代替モードが終了したことをクライアントドライバーに通知します。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_CONFIGURED|パートナーデバイスの DisplayPort 代替モードが pin 割り当てで構成されていることをクライアントドライバーに通知します。これにより、ドライバーは追加のタスクを実行できます。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_HPD_STATUS_CHANGED|ドライバーが追加のタスクを実行できるように、DisplayPort 接続のホットプラグ検出状態が変更されたことをクライアントドライバーに通知します。|

4. Ucmtcpciportcontroller Start を呼び出して、UcmTcpciCx にポートコントローラーを開始するように指示します。 UcmTcpciCx は、USB タイプ C と電力配信の制御を想定しています。 ポートコントローラーが開始されると、UcmTcpciCx が要求をハードウェア要求キューに挿入し始めます。 

 
## <a name="5-handlle-alerts-from-the-port-controller-hardware"></a>5。ポートコントローラーのハードウェアによるアラートのアラート

サンプルリファレンス:「 `ProcessAndSendAlerts` 」 `Alert.cpp`の「」を参照してください。

クライアントドライバーは、ポートコントローラーハードウェアから受信したアラート (またはイベント) を処理し、イベントに関連するデータを UcmTcpciCx に送信する必要があります。 

ハードウェアのアラートが発生すると、ポートコントローラーのハードウェアは、アラートの pin を高くします。 これにより、クライアントドライバーの ISR (手順2で登録) が呼び出されます。 このルーチンは、PASSIVE_LEVEL でのハードウェアの割り込みを行います。 このルーチンは、割り込みがポートコントローラーハードウェアからのアラートであるかどうかを判断します。その場合は、アラートの処理を完了し、Ucmtcpcicx のアラートを呼び出して UcmTcpciCx に通知します。 

Ucmtcpciportコントローラーのアラートを呼び出す前に、クライアントは、アラートに関連するすべての関連データを UCMTCPCI_PORT_CONTROLLER_ALERT_DATA 構造体に含める必要があります。 クライアントは、ハードウェアが複数のアラートを同時にアサートする可能性があるため、アクティブなすべてのアラートの配列を提供します。 

CC ステータスの変更を報告するタスクのフローの例を次に示します。 

1. クライアントはハードウェアアラートを受け取ります。 

2. クライアントは、アラートの登録を読み取り、アクティブなアラートの種類を特定します。 

3. クライアントは CC ステータスレジスタを読み取り、UCMTCPCI_PORT_CONTROLLER_ALERT_DATA の CC 状態レジスタの内容を説明します。 ドライバーは、AlertType メンバーを register の UcmTcpciPortControllerAlertCCStatus および CCStatus メンバーに設定します。

4. クライアントは Ucmportコントローラーアラートを呼び出して、配列ハードウェアのアラートを UcmTcpciCx に送信します。 

5. クライアントはアラートをクリアします (これは、クライアントがアラート情報を取得した後、いつでも発生する可能性があります)。 

## <a name="6-process-requests-received-from-ucmtcpcicx"></a>6。UcmTcpciCx から受信したプロセス要求

サンプルリファレンス:「`PortControllerInterface.cpp`」を参照してください。

状態マシンの実行の一環として、UcmTcpciCx はポートコントローラーに要求を送信する必要があります。 たとえば、TRANSMIT_BUFFER を設定する必要があります。 この要求は、クライアントドライバーに渡されます。 このドライバーは、UcmTcpciCx によって提供される詳細を使用して、送信バッファーを設定します。 ほとんどの要求は、クライアントドライバーによって読み取りまたは書き込みがハードウェアに変換されます。 DPM はハードウェア転送の完了の待機をブロックできないため、コマンドは非同期である必要があります。

UcmTcpciCx は、クライアントドライバーで必要な取得/設定操作を記述する i/o 制御コードとしてコマンドを送信します。 クライアントドライバーのキューセットアップで、ドライバーは UcmTcpciCx を使用してキューを登録しました。  UcmTcpciCx は、ドライバーからの操作が必要なフレームワーク要求オブジェクトをキューに配置し始めます。 I/o 制御コードは、手順 4. の表に一覧表示されています。

要求を適切なタイミングで完了するのは、クライアントドライバーの役割です。

クライアントドライバーは、要求された操作を完了したときに完了ステータスを使用して、フレームワーク要求オブジェクトで WdfRequestComplete を呼び出します。 

クライアントドライバーは、ハードウェア操作を実行するために、別のドライバーに i/o 要求を送信することが必要になる場合があります。 たとえば、サンプルでは、ドライバーは SPB 要求を I<sup>2</sup>C 接続ポートコントローラーに送信します。 この場合、要求オブジェクトには、WDM IRP 内の正しいスタック位置の数が含まれていない可能性があるため、このドライバーは UcmTcpciCx から受け取ったフレームワーク要求オブジェクトを転送できません。 クライアントドライバーは、別のフレームワーク要求オブジェクトを作成し、別のドライバーに転送する必要があります。 クライアントドライバーは、UcmTcpciCx から要求を取得するたびに作成するのではなく、初期化中に必要な要求オブジェクトを事前に割り当てることができます。 UcmTcpciCx では、特定の時点で未解決の要求が1つだけであることが保証されるため、これが可能です。 

## <a name="see-also"></a>関連項目
[USB タイプ-C ポートコントローラーインターフェイスドライバークラス拡張のリファレンス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt805826(v=vs.85))
