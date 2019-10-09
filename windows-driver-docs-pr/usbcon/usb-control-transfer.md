---
Description: このトピックでは、制御転送の構造と、クライアントドライバーがデバイスにコントロール要求を送信する方法について説明します。
title: USB コントロール転送の送信方法
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 6b36ef04e75ced0c51a1c145024ee67db01ddfee
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007592"
---
# <a name="how-to-send-a-usb-control-transfer"></a>USB コントロール転送の送信方法


このトピックでは、制御転送の構造と、クライアントドライバーがデバイスにコントロール要求を送信する方法について説明します。

このトピックの内容:

-   [既定のエンドポイントについて](#about-the-default-endpoint)
-   [コントロール転送のレイアウト](#layout-of-a-control-transfer)
-   [サポートされているドライバーモデル](#supported-driver-models)
    -   [関連テクノロジ](#related-technologies)
-   [前提条件](#prerequisites)
-   [制御転送要求を送信するための Microsoft 定義のメソッド](#microsoft-defined-methods-for-sending-control-transfer-requests)
-   [ベンダコマンドの制御転送を送信する方法-KMDF](#how-to-send-a-control-transfer-for-vendor-commands---kmdf)
-   [GET @ no__t-1STATUS-UMDF の制御転送を送信する方法](#how-to-send-a-control-transfer-for-get_status---umdf)

## <a name="about-the-default-endpoint"></a>既定のエンドポイントについて


すべての USB デバイスは、*既定のエンドポイント*と呼ばれるエンドポイントを少なくとも1つサポートする必要があります。 既定のエンドポイントを対象とする転送は、*制御転送*と呼ばれます。 制御転送の目的は、ホストがデバイス情報を取得したり、デバイスを構成したり、デバイスに固有の制御操作を実行したりできるようにすることです。

まず、既定のエンドポイントの特性について説明します。

-   既定のエンドポイントのアドレスは0です。
-   既定のエンドポイントは双方向です。つまり、ホストはエンドポイントにデータを送信し、1つの転送内のデータを受信できます。
-   既定のエンドポイントはデバイスレベルで使用でき、デバイスのインターフェイスには定義されていません。
-   既定のエンドポイントは、ホストとデバイス間の接続が確立されるとすぐにアクティブになります。 構成が選択される前でもアクティブになります。
-   既定のエンドポイントの最大パケットサイズは、デバイスのバス速度によって異なります。 低速度、8バイト。完全かつ高速、64バイト。SuperSpeed、512バイト。

## <a name="layout-of-a-control-transfer"></a>コントロール転送のレイアウト


制御転送は優先度の高い転送であるため、一定量の帯域幅が、ホストによってバスに予約されます。 低および全速度のデバイスの場合、帯域幅の 10%高および SuperSpeed では 20% がデバイスを転送します。 次に、コントロール転送のレイアウトを見てみましょう。

![usb 制御の転送](images/control-transfer.png)

制御転送は、*セットアップトランザクション*、*データトランザクション*、および*ステータストランザクション*の3つのトランザクションに分割されます。 各トランザクションには、*トークンパケット*、*データパケット*、および*ハンドシェイクパケット*の3種類のパケットが含まれています。

一部のフィールドは、すべてのパケットに共通です。 これらのフィールドは次のとおりです。

-   パケットの先頭を示す同期フィールドです。
-   パケットの種類、トランザクションの方向を示すパケット識別子 (PID)、およびハンドシェイクパケットの場合は、トランザクションの成功または失敗を示します。
-   EOP フィールドは、パケットの末尾を示します。

その他のフィールドは、パケットの種類によって異なります。

-   **トークンパケット**

    すべてのセットアップトランザクションは、トークンパケットで開始されます。 パケットの構造を次に示します。 ホストは常にトークンパケットを送信します。

    ![トークンのパケットレイアウト](images/token.png)

    PID 値は、トークンパケットの種類を示します。 有効な値は次のとおりです。

    -   セットアップ制御転送のセットアップトランザクションの開始を示します。
    -   からホストがデバイスからのデータを要求している (ケース読み取り) ことを示します。
    -   入出力ホストがデバイスにデータを送信している (書き込みケース) ことを示します。
    -   ディメンジョンフレームの開始を示します。 この種類のトークンパケットには、11ビットのフレーム番号が含まれています。 ホストは、SOF パケットを送信します。 このパケットが送信される頻度は、バス速度によって異なります。 全速度で、ホストは1ミリ秒ごとにパケットを送信します。高速バス上の125マイクロ秒ごと。

<!-- -->

-   **データパケット**

    トークンパケットの直後には、ペイロードを含むデータパケットが表示されます。 各データパケットが格納できるバイト数は、既定のエンドポイントの最大パケットサイズによって異なります。 データパケットは、転送の方向に応じて、ホストまたはデバイスによって送信できます。

    ![データパケットのレイアウト](images/data.png)

<!-- -->

-   **ハンドシェイクパケット**

    データパケットの直後には、ハンドシェイクパケットがあります。 パケットの PID は、パケットがホストまたはデバイスによって受信されたかどうかを示します。 ハンドシェイクパケットは、転送の方向に応じて、ホストまたはデバイスによって送信できます。

    ![ハンドシェイクパケットレイアウト](images/handshake.png)

トランザクションとパケットの構造は、Beagle、Ellisys、LeCroy USB プロトコルアナライザーなどの任意の USB アナライザーを使用して確認できます。 Analyzer デバイスは、ネットワーク経由で USB デバイスとの間でデータを送受信する方法を示しています。 この例では、LeCroy USB アナライザーによってキャプチャされたトレースをいくつか確認してみましょう。 この例は、情報のみを対象としています。 これは Microsoft が保証するものではありません。

-   **セットアップトランザクション**

    ホストは常に制御転送を開始します。 これは、セットアップトランザクションを送信することによって行われます。 このトランザクションには、*セットアップトークン*と呼ばれるトークンパケットと、その後に8バイトのデータパケットが含まれます。 このスクリーンショットは、セットアップトランザクションの例を示しています。

    ![セットアップトランザクションのトレース。](images/setup-trans.png)

    前のトレースでは、ホストはセットアップトークンパケット \#434 を送信することによって、コントロールの転送を開始します ( **H ↓**によって示されます)。 PID によってセットアップトークンを示すセットアップが指定されていることに注意してください。 PID の後に、デバイスアドレスとエンドポイントのアドレスが続きます。 制御転送の場合、そのエンドポイントアドレスは常に0です。

    次に、ホストはデータパケット \#435 を送信します。 PID は DATA0 であり、その値はパケットシーケンスに使用されます (説明されています)。 PID の後には、この要求に関する主要な情報を含む8バイトが続きます。 これらの8バイトは、要求の種類と、デバイスが応答を書き込むバッファーのサイズを示します。

    すべてのバイトは逆順に受信されます。 セクション9.3 で説明したように、次のフィールドと値が表示されます。

    <table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>フィールド</th>
    <th>サイズ</th>
    <th>値</th>
    <th>説明</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><strong>bmrequesttype</strong> (「9.3.1 bmrequesttype」を参照)</td>
    <td>1</td>
    <td>0x80</td>
    <td><p>データ転送方向は、デバイスからホスト (D7 は 1) です。</p>
    <p>要求は標準要求 (D6...D5 は 0)</p>
    <p>要求の受信者がデバイスである (D4 が 0)</p></td>
    </tr>
    <tr class="even">
    <td><strong>Brequest</strong> (「9.3.2 and Table 9-4」を参照)</td>
    <td>1</td>
    <td>0x06</td>
    <td>要求の種類は GET_DESCRIPTOR です。</td>
    </tr>
    <tr class="odd">
    <td><strong>Wvalue</strong> (表9-5 を参照)</td>
    <td>2</td>
    <td>0x0100</td>
    <td>要求値は、記述子の種類がデバイスであることを示します。</td>
    </tr>
    <tr class="even">
    <td><strong>wIndex</strong>(セクション9.3.4 を参照)</td>
    <td>2</td>
    <td>0x0000</td>
    <td><p>ホストからデバイス (D7 は 1) までの方向です。</p>
    <p>エンドポイント番号が0です。</p></td>
    </tr>
    <tr class="odd">
    <td><strong>Wlength</strong> (セクション9.3.5 を参照)</td>
    <td>2</td>
    <td>0x0012</td>
    <td>要求では18バイトを取得します。</td>
    </tr>
    </tbody>
    </table>

    このため、この制御 (読み取り) 転送では、ホストはデバイス記述子を取得する要求を送信し、その記述子を保持するために、転送の長さとして18バイトを指定します。 デバイスが18バイトを送信する方法は、既定のエンドポイントが1つのトランザクションで送信できるデータの量によって異なります。 この情報は、データトランザクション内のデバイスによって返されるデバイス記述子に含まれています。

    応答として、デバイスは、 **↓**によって示されるハンドシェイクパケット (\#436) を送信します。 PID 値が ACK (ACK パケット) であることに注意してください。 これは、デバイスがトランザクションを受信確認したことを示します。

-   **データトランザクション**

    次に、要求に応答してデバイスが返す内容を見てみましょう。 実際のデータは、データトランザクションで転送されます。

    データトランザクションのトレースを次に示します。

    ![データトランザクション例のトレース。](images/datra-trans.png)

    ACK パケットを受信すると、ホストはデータトランザクションを開始します。 トランザクションを開始するには、(トークン内で呼び出された) のように方向を持つトークンパケット (\#450) を送信します。

    応答として、デバイスは、トークン内のの後に続くデータパケット (\#451) を送信します。 このデータパケットには、実際のデバイス記述子が含まれています。 最初のバイトは、デバイス記述子の長さ (18 バイト) を示します (0x12)。 このデータパケットの最後のバイトは、既定のエンドポイントでサポートされる最大パケットサイズを示します。 この場合は、デバイスが既定のエンドポイントを使用して一度に8バイトを送信できることがわかります。

    **メモ** 既定のエンドポイントの最大パケットサイズは、デバイスの速度によって異なります。 高速デバイスの既定のエンドポイントは64バイトです。低速度のデバイスは8バイトです。

    ホストは、ACK パケット (\#452) をデバイスに送信することによって、データトランザクションを確認します。

    返されるデータの量を計算してみましょう。 セットアップトランザクションのデータパケット (\#435) の**Wlength**フィールドで、ホストから18バイトが要求されました。 データトランザクションでは、デバイス記述子の最初の8バイトだけがデバイスから受信されていることがわかります。 ホストは、残りの10バイトに格納されている情報をどのように受信するのでしょうか。 デバイスは、次の2つのトランザクションで実行します。8バイトと最後の2バイト。

    ホストが既定のエンドポイントの最大パケットサイズを認識したので、ホストは新しいデータトランザクションを開始し、パケットサイズに基づいて次の部分を要求します。

    次のデータトランザクションは次のようになります。

    ![データトランザクション例のトレース。](images/datra-trans2.png)

    ホストは、トークン (\#463) を送信し、デバイスから次の8バイトを要求することによって、前のデータトランザクションを開始します。 デバイスは、デバイス記述子の次の8バイトを含むデータパケット (\#464) で応答します。

    8バイトが受信されると、ホストはデバイスに ACK パケット (\#465) を送信します。

    次に、ホストは、別のデータトランザクションの最後の2バイトを次のように要求します。

    ![データトランザクション例のトレース。](images/datra-trans3.png)

    そのため、18バイトをデバイスからホストに転送する場合、ホストは、転送されたバイト数と、3つのデータトランザクション (8 + 8 + 2) を開始したバイト数を追跡します。

    **メモ**  データトランザクション19、23、26におけるデータパケットの PID に注意してください。 PID は DATA0 と DATA1 の間で交互に切り替わります。 このシーケンスは、データの切り替えと呼ばれます。 複数のデータトランザクションがある場合は、データ切り替えを使用してパケットシーケンスが検証されます。 このメソッドを使用すると、データパケットが重複したり失われたりしないようにすることができます。

    統合データパケットをデバイス記述子の構造にマップすることによって (表9-8 を参照)、次のフィールドと値が表示されます。

    | フィールド                  | サイズ | 値  | 説明                                                                       |
    |------------------------|------|--------|-----------------------------------------------------------------------------------|
    | **bLength**            | 1    | 0x12   | デバイス記述子の長さ (18 バイト)。                               |
    | **B記述子の種類**    | 1    | 0x01   | 記述子の種類は device です。                                                    |
    | **bcdUSB**             | 2    | 0x0100 | 仕様のバージョン番号は1.00 です。                                         |
    | **bDeviceClass**       | 1    | 0x00   | デバイスクラスは0です。 構成内の各インターフェイスには、クラス情報があります。 |
    | **bDeviceSubClass**    | 1    | 0x00   | Device クラスが0であるため、サブクラスは0です。                                          |
    | **bProtocol**          | 1    | 0x00   | プロトコルは0です。 このデバイスはクラス固有のプロトコルを使用しません。             |
    | **bMaxPacketSize0**    | 1    | 0x08   | エンドポイントの最大パケットサイズは8バイトです。                               |
    | **idVendor**           | 2    | 0x0562 | テレックス通信。                                                             |
    | **idProduct**          | 2    | 0x0002 | USB マイク。                                                                   |
    | **bcdDevice**          | 2    | 0x0100 | デバイスのリリース番号を示します。                                              |
    | **iManufacturer**      | 1    | 0x01   | 製造元の文字列。                                                              |
    | **iProduct**           | 1    | 0x02   | 製品文字列。                                                                   |
    | **iSerialNumber**      | 1    | 0x03   | シリアル番号。                                                                    |
    | **bNumConfigurations** | 1    | 0x01   | 構成の数。                                                         |



    これらの値を調べることによって、デバイスに関する予備情報がいくつかあります。 デバイスは、低速の USB マイクです。 既定のエンドポイントの最大パケットサイズは8バイトです。 デバイスは、1つの構成をサポートします。

-   **状態トランザクション**

    最後に、ホストは最後のトランザクション status transaction を開始することで、コントロールの転送を完了します。

    ![データトランザクション例のトレース。](images/status-trans.png)

    ホストは、OUT トークンパケット (\#481) を使用してトランザクションを開始します。 このパケットの目的は、デバイスが要求されたすべてのデータを送信したことを確認することです。 この状態トランザクションで送信されたデータパケットはありません。 デバイスは ACK パケットで応答します。 エラーが発生した場合、PID は NAK または停止のいずれかになります。

## <a name="supported-driver-models"></a>サポートされているドライバーモデル


### <a name="related-technologies"></a>関連テクノロジ

-   [カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   [ユーザーモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   [WinUSB](winusb.md)

## <a name="prerequisites"></a>前提条件


クライアントドライバーがパイプを列挙できるようにするには、次の要件が満たされていることを確認します。

-   クライアントドライバーによって、フレームワークの USB ターゲットデバイスオブジェクトが作成されている必要があります。

    Microsoft Visual Studio Professional 2012 で提供されている USB テンプレートを使用している場合は、テンプレートコードによってそれらのタスクが実行されます。 テンプレートコードは、ターゲットデバイスオブジェクトへのハンドルを取得し、デバイスコンテキストに格納します。

    \* * KMDF クライアントドライバー: * *

    KMDF クライアントドライバーは、 [**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)メソッドを呼び出すことによって WDFUSBDEVICE ハンドルを取得する必要があります。 詳細については、「 [USB クライアントドライバーのコード構造 (KMDF)](understanding-the-kmdf-template-code-for-usb.md)について」の「デバイスのソースコード」を参照してください。

    \* * UMDF client driver: * *

    UMDF クライアントドライバーは、フレームワークのターゲットデバイスオブジェクトを照会することによって、 [**IWDFUsbTargetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetdevice)ポインターを取得する必要があります。 詳細については、「 [usb クライアントドライバーコード構造 (UMDF)](understanding-the-umdf-template-code-for-usb.md)について」の「[**IPnpCallbackHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackhardware)の実装と usb 固有のタスク」を参照してください。

-   制御転送の最も重要な側面は、セットアップトークンを適切にフォーマットすることです。 要求を送信する前に、次の一連の情報を収集します。

    -   要求の方向: ホストからデバイスまたはデバイスへのホスト。
    -   要求の受信者: デバイス、インターフェイス、エンドポイント、またはその他。
    -   要求のカテゴリ: 標準、クラス、またはベンダー。
    -   GET @ no__t-0DESCRIPTPOR 要求などの要求の種類。 詳細については、USB 仕様のセクション9.5 を参照してください。
    -   **Wvalue**と**wIndex**の値。 これらの値は、要求の種類によって異なります。

    すべての情報は、公式の USB 仕様から入手できます。

-   UMDF ドライバーを作成する場合は、OSR USB Fx2 Learning Kit の UMDF サンプルドライバーから、ヘッダーファイルである Usb @ no__t を取得します。 このヘッダーファイルには、制御転送用のセットアップパケットを書式設定するための便利なマクロと構造が含まれています。

    すべての UMDF ドライバーは、デバイスとの間でデータを送受信するために、カーネルモードドライバーと通信する必要があります。 USB UMDF ドライバーの場合、カーネルモードドライバーは常に Microsoft が提供するドライバー [winusb](winusb.md) (winusb .sys) です。

    UMDF ドライバーが USB ドライバースタックの要求を行うたびに、Windows i/o マネージャーが WinUSB に要求を送信します。 WinUSB は要求を受信すると、要求を処理するか、USB ドライバースタックに転送します。

## <a name="microsoft-defined-methods-for-sending-control-transfer-requests"></a>制御転送要求を送信するための Microsoft 定義のメソッド


ホスト上の USB クライアントドライバーは、デバイスに関する情報を取得したり、デバイスを構成したり、ベンダ制御コマンドを送信したりするために、ほとんどの制御要求を開始します。 これらの要求はすべて、次のカテゴリに分類できます。

-   標準要求-標準要求は、USB 仕様で定義されています。 これらの要求を送信する目的は、デバイス、その構成、インターフェイス、およびエンドポイントに関する情報を取得することです。 各要求の受信者は、要求の種類によって異なります。 受信者は、デバイス、インターフェイス、エンドポイントのどちらでもかまいません。

    **メモ** 制御転送のターゲットは常に既定のエンドポイントです。 受信者は、ホストが関心のある情報 (記述子、状態など) を持つデバイスのエンティティです。

    これらの要求は、構成要求、機能要求、およびステータス要求にさらに分類できます。

    -   構成要求は、デバイスから情報を取得するために送信されます。これにより、ホストは GET @ no__t-0DESCRIPTOR 要求などの情報を構成できます。 これらの要求は、デバイスで特定の構成または別の設定を設定するためにホストによって送信される書き込み要求でもあります。
    -   機能要求は、デバイス、インターフェイス、またはエンドポイントでサポートされている特定のブール型デバイス設定を有効または無効にするために、クライアントドライバーによって送信されます。
    -   USB デバイスは、デバイス、エンドポイント、またはインターフェイスの USB 定義ステータスビットを取得または設定するための状態要求をサポートします。

    詳細については、「USB 仕様 (バージョン 2.0)」のセクション9.4 を参照してください。 標準の要求の種類は、ヘッダーファイルである Usbspec. h に定義されています。

-   クラス要求: 特定のデバイスクラス仕様によって定義されます。
-   仕入先の要求-ベンダーによって提供され、デバイスでサポートされている要求に依存します。

Microsoft 提供の USB スタックは、前のトレースに示されているように、デバイスとのすべてのプロトコル通信を処理します。 ドライバーは、クライアントドライバーがさまざまな方法で制御転送を送信できるようにするデバイスドライバーインターフェイス (DDIs) を公開します。 クライアントドライバーが Windows Driver Foundation (WDF) ドライバーの場合、ルーチンを直接呼び出して、一般的な種類のコントロール要求を送信できます。 WDF は、KMDF と UMDF の両方の制御転送を本質的にサポートしています。

特定の種類のコントロール要求は、WDF を介して公開されません。 これらの要求については、クライアントドライバーは WDF ハイブリッドモデルを使用できます。 このモデルを使用すると、クライアントドライバーは WDM の URB スタイルの要求をビルドしてフォーマットし、WDF framework オブジェクトを使用してそれらの要求を送信できます。 ハイブリッドモデルは、カーネルモードドライバーにのみ適用されます。

**UMDF ドライバーの場合:**

Usb @ no__t に定義されているヘルパーマクロと構造体を使用します。 このヘッダーは、OSR USB Fx2 Learning Kit の UMDF サンプルドライバーに含まれています。

この表を使用して、制御要求を USB ドライバースタックに送信するための最適な方法を決定します。 このテーブルを表示できない場合は、[このトピック](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)の表を参照してください。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>コントロール要求を送信するには...</th>
<th>KMDF ドライバーの場合は、次の KMDF DDIs を使用します。</th>
<th>UMDF ドライバーの場合は、次の UMDF メソッドを使用します...</th>
<th>WDM ドライバーの場合は、URB 構造 (ヘルパールーチン) をビルドします。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>CLEAR_FEATURE:デバイス、その構成、インターフェイス、エンドポイントで特定の機能設定を無効にします。 USB 仕様の「9.4.1」セクションを参照してください。</td>
<td><ol>
<li>セットアップパケットを宣言します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"><strong>WDF_USB_CONTROL_SETUP_PACKET</strong></a>構造体を参照してください。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_feature" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_feature)"><strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong></a>を呼び出して、セットアップパケットを初期化します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient)"><strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a>で定義されている受取人の値を指定します。</li>
<li>機能セレクター (<strong>Wvalue</strong>) を指定します。 「USB_FEATURE_XXX constants in Usbspec を参照してください。 USB 仕様の表9-6 も参照してください。</li>
<li><em>Setfeature</em>を<strong>FALSE</strong>に設定します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a>を呼び出して要求を送信します。</li>
</ol></td>
<td><ol>
<li>セットアップパケットを宣言します。 Usb_hw で宣言されている<strong>WINUSB_CONTROL_SETUP_PACKET</strong>構造体を参照してください。</li>
<li>Usb_hw で定義されているヘルパーマクロ<strong>WINUSB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong>を呼び出して、セットアップパケットを初期化します。</li>
<li><strong>WINUSB_BMREQUEST_RECIPIENT</strong>で定義されている受取人の値を指定します。</li>
<li>機能セレクター (<strong>Wvalue</strong>) を指定します。 「 <strong>USB_FEATURE_XXX</strong> Constants in usbspec を参照してください。 USB 仕様の表9-6 も参照してください。</li>
<li><em>Setfeature</em>を<strong>FALSE</strong>に設定します。</li>
<li>初期化されたセットアップパケットをフレームワーク要求オブジェクトに関連付け、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice:: FormatRequestForControlTransfer</strong></a>メソッドを呼び出すことによって転送バッファーに要求を作成します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest:: Send</strong></a>メソッドを呼び出して要求を送信します。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_feature_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_FEATURE_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_feature_request)"><strong>_URB_CONTROL_FEATURE_REQUEST</strong></a></p>
<p>(<a href="https://docs.microsoft.com/previous-versions/ff538932(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildFeatureRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538932(v=vs.85))"><strong>UsbBuildFeatureRequest</strong></a>)</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_DEVICE</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_INTERFACE</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_ENDPOINT</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_OTHER</p></td>
</tr>
<tr class="even">
<td>GET_CONFIGURATION:現在の USB 構成を取得します。 USB 仕様の「9.4.2」セクションを参照してください。</td>
<td><p>既定では、KMDF によって最初の構成が選択されます。 デバイス定義の構成番号を取得するには、次のようにします。</p>
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"><strong>WDF_USB_CONTROL_SETUP_PACKET</strong></a>の書式を設定し、 <strong>Brequest</strong>メンバーを<strong>USB_REQUEST_GET_CONFIGURATION</strong>に設定します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a>を呼び出して要求を送信します。</li>
</ol></td>
<td><p>既定では、UMDF によって最初の構成が選択されます。 デバイス定義の構成番号を取得するには、次のようにします。</p>
<ol>
<li>セットアップパケットを宣言します。 Usb_hw で宣言されている<strong>WINUSB_CONTROL_SETUP_PACKET</strong>構造体を参照してください。</li>
<li>Usb_hw で定義されているヘルパーマクロ<strong>WINUSB_CONTROL_SETUP_PACKET_INIT</strong>を呼び出して、セットアップパケットを初期化します。</li>
<li>方向として<strong>Bmrequesttodevice</strong>を、受信者として<strong>bmrequesttodevice</strong>を、要求として<strong>USB_REQUEST_GET_CONFIGURATION</strong>を指定します。</li>
<li>初期化されたセットアップパケットをフレームワーク要求オブジェクトに関連付け、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice:: FormatRequestForControlTransfer</strong></a>メソッドを呼び出すことによって転送バッファーに要求を作成します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest:: Send</strong></a>メソッドを呼び出して要求を送信します。</li>
<li>転送バッファー内の構成番号を受信します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory" data-raw-source="[&lt;strong&gt;IWDFMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory)"><strong>Iwdfmemory</strong></a>メソッドを呼び出して、そのバッファーにアクセスします。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_get_configuration_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_CONFIGURATION_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_get_configuration_request)"><strong>_URB_CONTROL_GET_CONFIGURATION_REQUEST</strong></a></p>
<p>URB_FUNCTION_GET_CONFIGURATION</p></td>
</tr>
<tr class="odd">
<td>GET_DESCRIPTOR:デバイス、構成、インターフェイス、およびエンドポイント記述子を取得します。 USB 仕様の「9.4.3」セクションを参照してください。
<p>詳細については、「 <a href="usb-descriptors.md" data-raw-source="[USB Descriptors](usb-descriptors.md)">USB 記述子</a>」を参照してください。</p></td>
<td><p>次のメソッドを呼び出します。</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceGetDeviceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor)"><strong>WdfUsbTargetDeviceGetDeviceDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetdescriptor" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceGetDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetdescriptor)"><strong>WdfUsbInterfaceGetDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetendpointinformation" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceGetEndpointInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetendpointinformation)"><strong>WdfUsbInterfaceGetEndpointInformation</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeGetInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation)"><strong>WdfUsbTargetPipeGetInformation</strong></a>。 このメソッドは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_pipe_information" data-raw-source="[&lt;strong&gt;WDF_USB_PIPE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_pipe_information)"><strong>WDF_USB_PIPE_INFORMATION</strong></a>構造体のエンドポイント記述子フィールドを返します。</li>
</ul></td>
<td><p>次のメソッドを呼び出します。</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::RetrieveDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor)"><strong>IWDFUsbTargetDevice::RetrieveDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getinterfacedescriptor" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::GetInterfaceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getinterfacedescriptor)"><strong>IWDFUsbInterface:: GetInterfaceDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetpipe-getinformation" data-raw-source="[&lt;strong&gt;IWDFUsbTargetPipe::GetInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetpipe-getinformation)"><strong>IWDFUsbTargetPipe:: GetInformation</strong></a>。 このメソッドは、 <a href="https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information" data-raw-source="[&lt;strong&gt;WINUSB_PIPE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information)"><strong>WINUSB_PIPE_INFORMATION</strong></a>構造体のエンドポイント記述子フィールドを返します。</li>
</ul></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_descriptor_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_DESCRIPTOR_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_descriptor_request)"><strong>_URB_CONTROL_DESCRIPTOR_REQUEST</strong></a></p>
<p>(<a href="https://docs.microsoft.com/previous-versions/ff538943(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildGetDescriptorRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538943(v=vs.85))"><strong>Usbbuildget記述子要求</strong></a>)</p>
<p>URB_FUNCTION_GET_DESCRIPTOR_FROM_DEVICE</p>
<p>URB_FUNCTION_GET_DESCRIPTOR_FROM_ENDPOINT</p>
<p>URB_FUNCTION_GET_DESCRIPTOR_FROM_INTERFACE</p></td>
</tr>
<tr class="even">
<td>GET_INTERFACE:インターフェイスの現在の代替設定を取得します。 USB 仕様の「9.4.4」セクションを参照してください。</td>
<td><p></p>
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicegetinterface" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceGetInterface&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicegetinterface)"><strong>WdfUsbTargetDeviceGetInterface</strong></a>メソッドを呼び出して、ターゲットインターフェイスオブジェクトへの WDFUSBINTERFACE ハンドルを取得します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredsettingindex" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceGetConfiguredSettingIndex&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredsettingindex)"><strong>WdfUsbInterfaceGetConfiguredSettingIndex</strong></a>メソッドを呼び出します。</li>
</ol></td>
<td><ol>
<li>ターゲットインターフェイスオブジェクトへの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface" data-raw-source="[&lt;strong&gt;IWDFUsbInterface&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface)"><strong>IWDFUsbInterface</strong></a>ポインターを取得します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getconfiguredsettingindex" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::GetConfiguredSettingIndex&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getconfiguredsettingindex)"><strong>IWDFUsbInterface:: GetConfiguredSettingIndex</strong></a>メソッドを呼び出します。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_get_interface_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_INTERFACE_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_get_interface_request)"><strong>_URB_CONTROL_GET_INTERFACE_REQUEST</strong></a></p>
<p>URB_FUNCTION_GET_INTERFACE</p></td>
</tr>
<tr class="odd">
<td>GET_STATUS:デバイス、エンドポイント、またはインターフェイスから状態ビットを取得します。 「9.4.5」を参照してください。 USB 仕様の。</td>
<td><ol>
<li>セットアップパケットを宣言します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"><strong>WDF_USB_CONTROL_SETUP_PACKET</strong></a>構造体を参照してください。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_get_status" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_GET_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_get_status)"><strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_GET_STATUS</strong></a>を呼び出して、セットアップパケットを初期化します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient)"><strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a>で定義されている受取人の値を指定します。</li>
<li>取得する状態 (デバイス、インターフェイス、またはエンドポイント) (<strong>wIndex</strong>) を指定します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a>を呼び出して要求を送信します。</li>
</ol></td>
<td><ol>
<li>セットアップパケットを宣言します。 Usb_hw で宣言されている<strong>WINUSB_CONTROL_SETUP_PACKET</strong>構造体を参照してください。</li>
<li>Usb_hw で定義されているヘルパーマクロ<strong>WINUSB_CONTROL_SETUP_PACKET_INIT_GET_STATUS</strong>を呼び出して、セットアップパケットを初期化します。</li>
<li><strong>WINUSB_BMREQUEST_RECIPIENT</strong>で定義されている受取人の値を指定します。</li>
<li>取得する状態 (デバイス、インターフェイス、またはエンドポイント) (<strong>wIndex</strong>) を指定します。</li>
<li>初期化されたセットアップパケットをフレームワーク要求オブジェクトに関連付け、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice:: FormatRequestForControlTransfer</strong></a>メソッドを呼び出すことによって転送バッファーに要求を作成します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest:: Send</strong></a>メソッドを呼び出して要求を送信します。</li>
<li>転送バッファーの状態値を受信します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory" data-raw-source="[&lt;strong&gt;IWDFMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory)"><strong>Iwdfmemory</strong></a>メソッドを呼び出して、そのバッファーにアクセスします。</li>
<li>状態が自己電源付きのリモートウェイクアップであるかどうかを判断するには、 <strong>WINUSB_DEVICE_TRAITS</strong>列挙で定義されている値を使用します。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_get_status_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_STATUS_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_get_status_request)"><strong>_URB_CONTROL_GET_STATUS_REQUEST</strong></a></p>
<p>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbbuildgetstatusrequest" data-raw-source="[&lt;strong&gt;UsbBuildGetStatusRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbbuildgetstatusrequest)"><strong>Usbbuildgetstatusrequest</strong></a>)</p>
<p>URB_FUNCTION_GET_STATUS_FROM_DEVICE</p>
<p>URB_FUNCTION_GET_STATUS_FROM_INTERFACE</p>
<p>URB_FUNCTION_GET_STATUS_FROM_ENDPOINT</p>
<p>URB_FUNCTION_GET_STATUS_FROM_OTHER.</p></td>
</tr>
<tr class="even">
<td>SET_ADDRESS:「9.4.6 in USB specification」セクションを参照してください。</td>
<td>この要求は、USB ドライバースタックによって処理されます。クライアントドライバーはこの操作を実行できません。</td>
<td>この要求は、USB ドライバースタックによって処理されます。クライアントドライバーはこの操作を実行できません。</td>
<td>この要求は、USB ドライバースタックによって処理されます。クライアントドライバーはこの操作を実行できません。</td>
</tr>
<tr class="odd">
<td>SET_CONFIGURATION:構成を設定します。 「9.4.7 in USB specification」セクションを参照してください。
<p>詳細については、「 <a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">USB デバイスの構成を選択する方法</a>」を参照してください。</p></td>
<td>既定では、KMDF は各インターフェイスの既定の構成と最初の代替設定を選択します。 クライアントドライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdfusbtargetdeviceselectconfigtype" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSelectConfigType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdfusbtargetdeviceselectconfigtype)"><strong>WdfUsbTargetDeviceSelectConfigType</strong></a>メソッドを呼び出し、要求オプションとして<strong>WdfUsbTargetDeviceSelectConfigTypeUrb</strong>を指定することによって、既定の構成を変更できます。 次に、この要求の URB をフォーマットし、USB ドライバースタックに送信する必要があります。</td>
<td>既定では、UMDF は、各インターフェイスの既定の構成と最初の代替設定を選択します。 クライアントドライバーは、構成を変更できません。</td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_select_configuration" data-raw-source="[&lt;strong&gt;_URB_SELECT_CONFIGURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_select_configuration)"><strong>構成 (_C)</strong></a></p>
<p>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild" data-raw-source="[&lt;strong&gt;USBD_SelectConfigUrbAllocateAndBuild&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)"><strong>USBD_SelectConfigUrbAllocateAndBuild</strong></a>)</p>
<p>URB_FUNCTION_SELECT_CONFIGURATION</p></td>
</tr>
<tr class="even">
<td>SET_DESCRIPTOR:既存のデバイス、構成、または文字列記述子を更新します。 「9.4.8 in USB specification」セクションを参照してください。
<p>この要求は一般的には使用されません。 ただし、USB ドライバースタックは、クライアントドライバーからのこのような要求を受け入れます。</p></td>
<td><ol>
<li>要求の<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)"><strong>URB</strong></a>を割り当てて作成します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_descriptor_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_DESCRIPTOR_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_descriptor_request)"><strong>_URB_CONTROL_DESCRIPTOR_REQUEST</strong></a>構造体の転送情報を指定します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforurb" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForUrb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforurb)"><strong>WdfUsbTargetDeviceFormatRequestForUrb</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendUrbSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)"><strong>WdfUsbTargetDeviceSendUrbSynchronously</strong></a>を呼び出して要求を送信します。</li>
</ol></td>
<td><ol>
<li>セットアップパケットを宣言します。 Usb_hw で宣言されている<strong>WINUSB_CONTROL_SETUP_PACKET</strong>構造体を参照してください。</li>
<li>USB 仕様に従って、転送情報を指定します。</li>
<li>初期化されたセットアップパケットをフレームワーク要求オブジェクトに関連付け、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice:: FormatRequestForControlTransfer</strong></a>メソッドを呼び出すことによって転送バッファーに要求を作成します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest:: Send</strong></a>メソッドを呼び出して要求を送信します。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_descriptor_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_DESCRIPTOR_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_descriptor_request)"><strong>_URB_CONTROL_DESCRIPTOR_REQUEST</strong></a></p>
<p>URB_FUNCTION_SET_DESCRIPTOR_TO_DEVICE</p>
<p>URB_FUNCTION_SET_DESCRIPTOR_TO_ENDPOINT</p>
<p>URB_FUNCTION_SET_DESCRIPTOR_TO_INTERFACE</p></td>
</tr>
<tr class="odd">
<td>SET_FEATURE:デバイス、その構成、インターフェイス、エンドポイントで特定の機能設定を有効にします。 USB 仕様の「9.4.9」セクションを参照してください。</td>
<td><ol>
<li>セットアップパケットを宣言します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"><strong>WDF_USB_CONTROL_SETUP_PACKET</strong></a>構造体を参照してください。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_feature" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_feature)"><strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong></a>を呼び出して、セットアップパケットを初期化します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient)"><strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a>で定義されている受取人の値 (デバイス、インターフェイス、エンドポイント) を指定します。</li>
<li>機能セレクター (<strong>Wvalue</strong>) を指定します。 「USB_FEATURE_XXX constants in Usbspec を参照してください。 USB 仕様の表9-6 も参照してください。</li>
<li><em>Setfeature</em>を<strong>TRUE</strong>に設定します</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a>を呼び出して要求を送信します。</li>
</ol></td>
<td><ol>
<li>セットアップパケットを宣言します。 Usb_hw で宣言されている<strong>WINUSB_CONTROL_SETUP_PACKET</strong>構造体を参照してください。</li>
<li>Usb_hw で定義されているヘルパーマクロ<strong>WINUSB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong>を呼び出して、セットアップパケットを初期化します。</li>
<li><strong>WINUSB_BMREQUEST_RECIPIENT</strong>で定義されている受取人の値を指定します。</li>
<li>機能セレクター (<strong>Wvalue</strong>) を指定します。 「 <strong>USB_FEATURE_XXX</strong> Constants in usbspec を参照してください。 USB 仕様の表9-6 も参照してください。</li>
<li><em>Setfeature</em>を<strong>TRUE</strong>に設定します。</li>
<li>初期化されたセットアップパケットをフレームワーク要求オブジェクトに関連付け、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice:: FormatRequestForControlTransfer</strong></a>メソッドを呼び出すことによって転送バッファーに要求を作成します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest:: Send</strong></a>メソッドを呼び出して要求を送信します。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_feature_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_FEATURE_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_feature_request)"><strong>_URB_CONTROL_FEATURE_REQUEST</strong></a></p>
<p>(<a href="https://docs.microsoft.com/previous-versions/ff538932(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildFeatureRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538932(v=vs.85))"><strong>UsbBuildFeatureRequest</strong></a>)</p>
<p>URB_FUNCTION_SET_FEATURE_TO_DEVICE</p>
<p>URB_FUNCTION_SET_FEATURE_TO_INTERFACE</p>
<p>URB_FUNCTION_SET_FEATURE_TO_ENDPOINT</p>
<p>URB_FUNCTION_SET_FEATURE_TO_OTHER</p></td>
</tr>
<tr class="even">
<td>SET_INTERFACE:インターフェイスの代替設定を変更します。 USB 仕様の「9.4.9」セクションを参照してください。
<p>詳細については、「 <a href="select-a-usb-alternate-setting.md" data-raw-source="[How to select an alternate setting in a USB interface](select-a-usb-alternate-setting.md)">USB インターフェイスで別の設定を選択する方法</a>」を参照してください。</p></td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSelectConfig&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)"><strong>WdfUsbTargetDeviceSelectConfig</strong></a>
<p></p>
<ol>
<li>ターゲットインターフェイスオブジェクトへの WDFUSBINTERFACE ハンドルを取得します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceSelectSetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting)"><strong>WdfUsbInterfaceSelectSetting</strong></a>メソッドを呼び出します。</li>
</ol></td>
<td><ol>
<li>ターゲットインターフェイスオブジェクトへの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface" data-raw-source="[&lt;strong&gt;IWDFUsbInterface&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface)"><strong>IWDFUsbInterface</strong></a>ポインターを取得します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-selectsetting" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::SelectSetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-selectsetting)"><strong>IWDFUsbInterface:: SelectSetting</strong></a>メソッドを呼び出します。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_select_interface" data-raw-source="[&lt;strong&gt;_URB_SELECT_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_select_interface)"><strong>_URB_SELECT_INTERFACE</strong></a></p>
<p>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild" data-raw-source="[&lt;strong&gt;USBD_SelectInterfaceUrbAllocateAndBuild&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)"><strong>USBD_SelectInterfaceUrbAllocateAndBuild</strong></a>)</p>
<p>URB_FUNCTION_SELECT_INTERFACE</p></td>
</tr>
<tr class="odd">
<td>SYNC_FRAME:Set と get、およびエンドポイントの同期フレーム番号。 USB 仕様の「9.4.10」セクションを参照してください。</td>
<td>この要求は、USB ドライバースタックによって処理されます。クライアントドライバーはこの操作を実行できません。</td>
<td>この要求は、USB ドライバースタックによって処理されます。クライアントドライバーはこの操作を実行できません。</td>
<td>この要求は、USB ドライバースタックによって処理されます。クライアントドライバーはこの操作を実行できません。</td>
</tr>
<tr class="even">
<td>デバイスクラス固有の要求とベンダーコマンド。</td>
<td><ol>
<li>セットアップパケットを宣言します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"><strong>WDF_USB_CONTROL_SETUP_PACKET</strong></a>構造体を参照してください。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_class" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_CLASS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_class)"><strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_CLASS</strong></a>固有の要求を呼び出すか、ベンダーのコマンドに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_vendor" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_VENDOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_vendor)"><strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_VENDOR</strong></a>を呼び出して、セットアップパケットを初期化します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient)"><strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a>で定義されている受取人の値 (デバイス、インターフェイス、エンドポイント) を指定します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a>を呼び出して要求を送信します。</li>
</ol></td>
<td><ol>
<li>セットアップパケットを宣言します。 Usb_hw で宣言されている<strong>WINUSB_CONTROL_SETUP_PACKET</strong>構造体を参照してください。</li>
<li>Usb_hw で定義されているヘルパーマクロ<strong>WINUSB_CONTROL_SETUP_PACKET_INIT_CLASS</strong>または<strong>WINUSB_CONTROL_SETUP_PACKET_INIT_VENDOR</strong>を呼び出して、セットアップパケットを初期化します。</li>
<li>クラスまたはハードウェアの仕様に従って、方向 ( <strong>WINUSB_BMREQUEST_DIRECTION</strong>列挙体を参照)、受信者 ( <strong>WINUSB_BMREQUEST_RECIPIENT</strong>列挙体を参照)、および要求を指定します。</li>
<li>初期化されたセットアップパケットをフレームワーク要求オブジェクトに関連付け、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice:: FormatRequestForControlTransfer</strong></a>メソッドを呼び出すことによって転送バッファーに要求を作成します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest:: Send</strong></a>メソッドを呼び出して要求を送信します。</li>
<li>転送バッファー内のデバイスから情報を受信します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory" data-raw-source="[&lt;strong&gt;IWDFMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory)"><strong>Iwdfmemory</strong></a>メソッドを呼び出して、そのバッファーにアクセスします。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_vendor_or_class_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_VENDOR_OR_CLASS_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_vendor_or_class_request)"><strong>_URB_CONTROL_VENDOR_OR_CLASS_REQUEST</strong></a></p>
<p>(<a href="https://docs.microsoft.com/previous-versions/ff538986(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildVendorRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538986(v=vs.85))"><strong>UsbBuildVendorRequest</strong></a>)</p>
<p>URB_FUNCTION_VENDOR_DEVICE</p>
<p>URB_FUNCTION_VENDOR_INTERFACE</p>
<p>URB_FUNCTION_VENDOR_ENDPOINT</p>
<p>URB_FUNCTION_VENDOR_OTHER</p>
<p>URB_FUNCTION_CLASS_DEVICE</p>
<p>URB_FUNCTION_CLASS_INTERFACE</p>
<p>URB_FUNCTION_CLASS_ENDPOINT</p>
<p>URB_FUNCTION_CLASS_OTHER</p></td>
</tr>
</tbody>
</table>



## <a name="how-to-send-a-control-transfer-for-vendor-commands---kmdf"></a>ベンダコマンドの制御転送を送信する方法-KMDF


この手順では、クライアントドライバーが制御転送を送信する方法を示します。 この例では、クライアントドライバーは、デバイスからファームウェアのバージョンを取得するベンダコマンドを送信します。

1.  Vendor コマンドの定数を宣言します。 ハードウェアの仕様を調べ、使用するベンダコマンドを決定します。
2.  [**WDF @ no__t-2MEMORY @ no__t-3descriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/ns-wdfmemory-_wdf_memory_descriptor)構造体を宣言し、 [**WDF @ NO__T-6memory @ NO__T-7descriptor @ NO__T-8init @ NO__T-9buffer**](https://msdn.microsoft.com/library/windows/hardware/ff552392_init_buffer)マクロを呼び出して初期化します。 この構造は、USB ドライバーが要求を完了した後に、デバイスからの応答を受信します。
3.  要求を同期または非同期のどちらで送信するかに応じて、送信オプションを指定します。
    -   [**WdfUsbTargetDeviceSendControlTransferSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)を呼び出して要求を同期的に送信する場合は、タイムアウト値を指定します。 この値は、タイムアウトがないとスレッドを無期限にブロックできるため、重要です。

        この場合は、 [**WDF @ no__t-2REQUEST @ no__t-3SEND @ no__t-4options**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/ns-wdfrequest-_wdf_request_send_options)構造体を宣言し、 [**WDF @ NO__T-7request @ NO__T-8send @ NO__T-9options @ NO__T-10init**](https://msdn.microsoft.com/library/windows/hardware/ff552491_init)マクロを呼び出して初期化します。 オプションを**WDF @ no__t-1REQUEST @ no__t-2SEND @ no__t-3OPTION @ no__t-4TIMEOUT**として指定します。

        次に、 [**WDF @ no__t-2REQUEST @ no__t-3SEND @ no__t-4OPTIONS @ no__t-5SET @ no__t-6timeout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdf_request_send_options_set_timeout)マクロを呼び出して、タイムアウト値を設定します。

    -   要求を非同期に送信する場合は、完了ルーチンを実装します。 完了ルーチンで割り当てられているすべてのリソースを解放します。

4.  [**WDF @ no__t-2USB @ no__t-3CONTROL @ no__t-4SETUP @ no__t-5PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)構造体を宣言してセットアップトークンを格納し、構造体の形式を設定します。 これを行うには、 [**WDF @ no__t-2USB @ no__t-3CONTROL @ no__t-4SETUP @ no__t-5PACKET @ no__t-6INIT @ no__t-7VENDOR**](https://msdn.microsoft.com/library/windows/hardware/ff552568_init_vendor)マクロを呼び出して、セットアップパケットの形式を設定します。 呼び出しで、要求の方向、受信者、送信要求オプション (手順3で初期化)、および vendor コマンドの定数を指定します。
5.  [**WdfUsbTargetDeviceSendControlTransferSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)または[**WdfUsbTargetDeviceFormatRequestForControlTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)を呼び出して要求を送信します。
6.  フレームワークによって返された NTSTATUS 値を確認し、受信した値を調べます。

このコード例では、制御転送要求を USB デバイスに送信して、ファームウェアのバージョンを取得します。 要求は同期的に送信され、クライアントドライバーは、相対タイムアウト値を5秒 (100 ナノ秒単位) で指定します。 ドライバーは、受信した応答をドライバーによって定義されたデバイスコンテキストに格納します。

```cpp
enum {   
    USBFX2_GET_FIRMWARE_VERSION = 0x1,  
....

} USBFX2_VENDOR_COMMANDS; 

#define WDF_TIMEOUT_TO_SEC              ((LONGLONG) 1 * 10 * 1000 * 1000)  // defined in wdfcore.h

const __declspec(selectany) LONGLONG   
            DEFAULT_CONTROL_TRANSFER_TIMEOUT = 5 * -1 * WDF_TIMEOUT_TO_SEC; 


typedef struct _DEVICE_CONTEXT
{

    ...
       union {  
        USHORT      VersionAsUshort;  
        struct {  
            BYTE Minor;  
            BYTE Major;  
        } Version;  
    } Firmware; // Firmware version.

} DEVICE_CONTEXT, *PDEVICE_CONTEXT;


__drv_requiresIRQL(PASSIVE_LEVEL)  
VOID  GetFirmwareVersion(  
    __in PDEVICE_CONTEXT DeviceContext  
)  
{  
    NTSTATUS                        status;  
    WDF_USB_CONTROL_SETUP_PACKET    controlSetupPacket;  
    WDF_REQUEST_SEND_OPTIONS        sendOptions;  
    USHORT                          firmwareVersion;  
    WDF_MEMORY_DESCRIPTOR           memoryDescriptor;  

    PAGED_CODE();  

    firmwareVersion = 0;  

    WDF_MEMORY_DESCRIPTOR_INIT_BUFFER(&memoryDescriptor, (PVOID) &firmwareVersion, sizeof(firmwareVersion));  

    WDF_REQUEST_SEND_OPTIONS_INIT(  
                                  &sendOptions,  
                                  WDF_REQUEST_SEND_OPTION_TIMEOUT  
                                  );  

    WDF_REQUEST_SEND_OPTIONS_SET_TIMEOUT(  
                                         &sendOptions,  
                                         DEFAULT_CONTROL_TRANSFER_TIMEOUT  
                                         );  

    WDF_USB_CONTROL_SETUP_PACKET_INIT_VENDOR(&controlSetupPacket,  
                                        BmRequestDeviceToHost,       // Direction of the request
                                        BmRequestToDevice,           // Recipient
                                        USBFX2_GET_FIRMWARE_VERSION, // Vendor command
                                        0,                           // Value
                                        0);                          // Index    

    status = WdfUsbTargetDeviceSendControlTransferSynchronously(  
                                        DeviceContext->UsbDevice,  
                                        WDF_NO_HANDLE,               // Optional WDFREQUEST
                                        &sendOptions,  
                                        &controlSetupPacket,  
                                        &memoryDescriptor,           // MemoryDescriptor                                          
                                        NULL);                       // BytesTransferred    

    if (!NT_SUCCESS(status)) 
    {  
        KdPrint(("Device %d: Failed to get device firmware version 0x%x\n", DeviceContext->DeviceNumber, status));  
        TraceEvents(DeviceContext->DebugLog,  
                    TRACE_LEVEL_ERROR,  
                    DBG_RUN,  
                    "Device %d: Failed to get device firmware version 0x%x\n",  
                    DeviceContext->DeviceNumber,  
                    status);  
    }
    else 
    {  
        DeviceContext->Firmware.VersionAsUshort = firmwareVersion;  
        TraceEvents(DeviceContext->DebugLog,  
                    TRACE_LEVEL_INFORMATION,  
                    DBG_RUN,  
                    "Device %d: Get device firmware version : 0x%x\n",  
                    DeviceContext->DeviceNumber,  
                    firmwareVersion);  
    }  

    return;  
}  
```

##<a name="how-to-send-a-control-transfer-for-get_status---umdf"></a>GET @ no__t-1STATUS-UMDF の制御転送を送信する方法


この手順では、クライアントドライバーが GET @ no__t-0STATUS コマンドの制御転送を送信する方法について説明します。 要求の受信者はデバイスであり、要求はビット D1-D0 で情報を取得します。 詳細については、「USB 仕様」の図9-4 を参照してください。

1.  OSR USB Fx2 Learning Kit 用の UMDF サンプルドライバーで利用できるヘッダーファイル Usb @ no__t をインクルードします。
2.  **Winusb @ no__t-1CONTROL @ no__t-2SETUP @ no__t-3PACKET**構造体を宣言します。
3.  ヘルパーマクロを呼び出して、セットアップパケットを初期化します。 **Winusb @ no__t-1CONTROL @ no__t-2SETUP @ no__t-3PACKET @ no__t-4INIT @ no__t-5GET @ no__t-6STATUS**.
4.  受信者として**Bmrequesttodevice**を指定します。
5.  *インデックス*値に0を指定します。
6.  要求を同期的に送信するために、ヘルパーメソッド SendControlTransferSynchronously 同期的に呼び出します。

    ヘルパーメソッドは、 [**IWDFUsbTargetDevice:: FormatRequestForControlTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)メソッドを呼び出すことによって、初期化されたセットアップパケットをフレームワークの要求オブジェクトと転送バッファーに関連付けることによって、要求をビルドします。 ヘルパーメソッドは、 [**IWDFIoRequest:: Send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)メソッドを呼び出すことによって要求を送信します。 メソッドから制御が戻った後、返された値を調べます。

7.  状態が自己電源付きのリモートウェイクアップであるかどうかを判断するには、 **Winusb @ no__t-1DEVICE @ no__t-2TRAITS**列挙で定義されている次の値を使用します。

このコード例では、デバイスの状態を取得するために、コントロール転送要求をに送信します。 この例では、SendControlTransferSynchronously いう名前のヘルパーメソッドを同期的に呼び出して、要求を同期的に送信します。

```cpp
HRESULT  
CDevice::GetDeviceStatus ()  
{  

    HRESULT hr = S_OK;

    USHORT deviceStatus;  
    ULONG bytesTransferred;  


    TraceEvents(TRACE_LEVEL_INFORMATION,  
                DRIVER_ALL_INFO,  
                "%!FUNC!: entry");  


    // Setup the control packet.      

    WINUSB_CONTROL_SETUP_PACKET setupPacket;  

    WINUSB_CONTROL_SETUP_PACKET_INIT_GET_STATUS(  
                                      &setupPacket,  
                                      BmRequestToDevice,  
                                      0);  

    hr = SendControlTransferSynchronously(  
                 &(setupPacket.WinUsb),  
                 & deviceStatus,  
                 sizeof(USHORT),  
                 &bytesReturned  
                ); 

     if (SUCCEEDED(hr))  
    {  
        if (deviceStatus & USB_GETSTATUS_SELF_POWERED)
        {
             m_Self_Powered = true;
        } 
        if (deviceStatus & USB_GETSTATUS_REMOTE_WAKEUP_ENABLED)
        {
             m_remote_wake-enabled = true;
        }  

    }  


    return hr;  

 }
```

次のコード例は、SendControlTransferSynchronously いう名前のヘルパーメソッドを同期的に実装する方法を示しています。 このメソッドは、要求を同期的に送信します。

```cpp
HRESULT  
CDevice::SendControlTransferSynchronously(  
    _In_ PWINUSB_SETUP_PACKET SetupPacket,  
    _Inout_ PBYTE Buffer,  
    _In_ ULONG BufferLength,  
    _Out_ PULONG LengthTransferred  
    )  
{  
    HRESULT hr = S_OK;  
    IWDFIoRequest *pWdfRequest = NULL;  
    IWDFDriver * FxDriver = NULL;  
    IWDFMemory * FxMemory = NULL;   
    IWDFRequestCompletionParams * FxComplParams = NULL;  
    IWDFUsbRequestCompletionParams * FxUsbComplParams = NULL;  

    *LengthTransferred = 0;  

    hr = m_FxDevice->CreateRequest( NULL, //pCallbackInterface
                                    NULL, //pParentObject
                                    &pWdfRequest);  

    if (SUCCEEDED(hr))  
    {  
        m_FxDevice->GetDriver(&FxDriver);  

        hr = FxDriver->CreatePreallocatedWdfMemory( Buffer,  
                                                    BufferLength,  
                                                    NULL,        //pCallbackInterface
                                                    pWdfRequest, //pParetObject
                                                    &FxMemory );  
    }  

    if (SUCCEEDED(hr))  
    {  
        hr = m_pIUsbTargetDevice->FormatRequestForControlTransfer( pWdfRequest,  
                                                                   SetupPacket,  
                                                                   FxMemory,  
                                                                   NULL); //TransferOffset
    }                                                            

    if (SUCCEEDED(hr))  
    {  
        hr = pWdfRequest->Send( m_pIUsbTargetDevice,  
                                WDF_REQUEST_SEND_OPTION_SYNCHRONOUS,  
                                0); //Timeout      }  

    if (SUCCEEDED(hr))  
    {  
        pWdfRequest->GetCompletionParams(&FxComplParams);  

        hr = FxComplParams->GetCompletionStatus();  
    }  

    if (SUCCEEDED(hr))  
    {  
        HRESULT hrQI = FxComplParams->QueryInterface(IID_PPV_ARGS(&FxUsbComplParams));  
        WUDF_TEST_DRIVER_ASSERT(SUCCEEDED(hrQI));  

        WUDF_TEST_DRIVER_ASSERT( WdfUsbRequestTypeDeviceControlTransfer ==   
                            FxUsbComplParams->GetCompletedUsbRequestType() );  

        FxUsbComplParams->GetDeviceControlTransferParameters( NULL,  
                                                             LengthTransferred,  
                                                             NULL,  
                                                             NULL );  
    }  

    SAFE_RELEASE(FxUsbComplParams);  
    SAFE_RELEASE(FxComplParams);  
    SAFE_RELEASE(FxMemory);  

    pWdfRequest->DeleteWdfObject();          
    SAFE_RELEASE(pWdfRequest);  

    SAFE_RELEASE(FxDriver);  

    return hr;  
}  
```

## <a name="remarks"></a>コメント


デバイスの関数ドライバーとして Winusb .sys を使用している場合は、アプリケーションから制御転送を送信できます。 WinUSB でセットアップパケットをフォーマットするには、このトピックの表に記載されている UMDF helper マクロと構造体を使用します。 要求を送信するには、 [**Winusb @ no__t-2ControlTransfer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer)関数を呼び出します。








