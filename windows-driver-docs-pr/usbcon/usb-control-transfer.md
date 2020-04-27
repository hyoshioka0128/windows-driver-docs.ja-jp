---
Description: このトピックでは、コントロール転送の構造についてと、クライアント ドライバーでデバイスに制御要求を送信する方法について説明します。
title: USB コントロール転送の送信方法
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 23cf718b0797d6ca04ea4f96a91b59b1564e3d39
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "72844834"
---
# <a name="how-to-send-a-usb-control-transfer"></a>USB コントロール転送の送信方法


このトピックでは、コントロール転送の構造についてと、クライアント ドライバーでデバイスに制御要求を送信する方法について説明します。

このトピックの内容:

-   [既定のエンドポイントについて](#about-the-default-endpoint)
-   [コントロール転送のレイアウト](#layout-of-a-control-transfer)
-   [サポートされているドライバー モデル](#supported-driver-models)
    -   [関連テクノロジ](#related-technologies)
-   [前提条件](#prerequisites)
-   [コントロール転送要求を送信するための Microsoft 定義メソッド](#microsoft-defined-methods-for-sending-control-transfer-requests)
-   [ベンダー コマンドのコントロール転送を送信する方法 - KMDF](#how-to-send-a-control-transfer-for-vendor-commands---kmdf)
-   [GET\_STATUS のコントロール転送を送信する方法 - UMDF](#how-to-send-a-control-transfer-for-get_status---umdf)

## <a name="about-the-default-endpoint"></a>既定のエンドポイントについて


すべての USB デバイスで、*既定のエンドポイント*と呼ばれているエンドポイントを少なくとも 1 つサポートする必要があります。 既定のエンドポイントを対象とする転送は、*コントロール転送*と呼ばれています。 コントロール転送の目的は、ホストがデバイス情報を取得したり、デバイスを構成したり、デバイスに固有のコントロール操作を実行したりできるようにすることです。

まず、既定のエンドポイントの特性について調べることから始めます。

-   既定のエンドポイントのアドレスは 0 です。
-   既定のエンドポイントは双方向です。つまり、ホストでは、1 回の転送内でエンドポイントにデータを送信し、エンドポイントからデータを受信できます。
-   既定のエンドポイントはデバイス レベルで利用できます。デバイスのインターフェイスには定義されていません。
-   既定のエンドポイントは、ホストとデバイスの間の接続が確立された直後にアクティブになります。 構成が選択される前でもアクティブになります。
-   既定のエンドポイントの最大パケット サイズは、デバイスのバス速度によって異なります。 低速、8 バイト。全速/高速、64 バイト。SuperSpeed、512 バイト。

## <a name="layout-of-a-control-transfer"></a>コントロール転送のレイアウト


コントロール転送は優先度の高い転送であるため、一定量の帯域幅がホストによってバスに予約されます。 低速転送と全速転送のデバイスの場合、帯域幅の 10% が、高速転送と SuperSpeed 転送のデバイスの場合、20% が予約されます。 次に、コントロール転送のレイアウトを見てみましょう。

![USB コントロール転送](images/control-transfer.png)

コントロール転送は、"*セットアップ トランザクション*"、"*データ トランザクション*"、"*ステータス トランザクション*" の 3 つのトランザクションに分けられます。 各トランザクションには、"*トークン パケット*"、"*データ パケット*"、"*ハンドシェイク パケット*" という 3 種類のパケットが含まれています。

一部のフィールドはすべてのパケットに共通しています。 これらのフィールドを次に示します。

-   パケットの先頭を示す同期フィールド。
-   パケットの種類、トランザクションの方向、ハンドシェイク パケットの場合はトランザクションの成功または失敗を示すパケット識別子 (PID)。
-   EOP フィールドは、パケットの末尾を示します。

その他のフィールドは、パケットの種類によって異なります。

-   **トークン パケット**

    すべてのセットアップ トランザクションは、トークン パケットから始まります。 パケットの構造を次に示します。 ホストは常にトークン パケットを送信します。

    ![トークン パケット レイアウト](images/token.png)

    PID 値は、トークン パケットの種類を示します。 設定できる値は次のとおりです。

    -   SETUP:コントロール転送のセットアップ トランザクションの開始を示します。
    -   IN:ホストがデバイスにデータを要求していることを示します (読み取りの場合)。
    -   OUT:ホストによってデバイスにデータが送信されていることを示します (書き込みの場合)。
    -   SOF:フレームの開始を示します。 この種類のトークン パケットには、11 ビットのフレーム番号が含まれています。 ホストから SOF パケットが送信されます。 このパケットが送信される頻度は、バス速度によって異なります。 全速の場合、ホストは 1 ミリ秒ごとにパケットを送信します。高速バスの場合、125 マイクロ秒ごとです。

<!-- -->

-   **データ パケット**

    トークン パケットの直後に続くのが、ペイロードを含むデータ パケットです。 各データ パケットで格納できるバイト数は、既定のエンドポイントの最大パケット サイズによって異なります。 データ パケットは、転送の方向に応じてホストまたはデバイスによって送信されます。

    ![データ パケット レイアウト](images/data.png)

<!-- -->

-   **ハンドシェイク パケット**

    データ パケットの直後に続くのがハンドシェイク パケットです。 パケットの PID は、パケットがホストによって受信されたのか、デバイスによって受信されたのかを示します。 ハンドシェイク パケットは、転送の方向に応じてホストまたはデバイスによって送信されます。

    ![ハンドシェイク パケット レイアウト](images/handshake.png)

トランザクションとパケットの構造は、Beagle、Ellisys、LeCroy USB プロトコル アナライザーなど、あらゆる USB アナライザーを使用して確認できます。 アナライザー デバイスには、通信回線経由で USB デバイスとの間でデータを送受信する方法が示されます。 この例では、LeCroy USB アナライザーによってキャプチャされたトレースをいくつか確認してみましょう。 この例は、情報提供目的のみで用意されています。 Microsoft がこの製品を推薦するものではありません。

-   **セットアップ トランザクション**

    ホストから常にコントロール転送が開始されます。 これはセットアップ トランザクションを送信することによって行われます。 このトランザクションには "*セットアップ トークン*" と呼ばれているトークン パケットが含まれ、その後に 8 バイトのデータ パケットが続きます。 このスクリーンショットでは、セットアップ トランザクションの例を示しています。

    ![セットアップ トランザクションのトレース。](images/setup-trans.png)

    前のトレースでは、セットアップ トークン パケット \#434 を送信することによってホストによりコントロール転送が開始されます (**H↓** がそれを示しています)。 PID によってセットアップ トークンを示す SETUP が指定されることにご注意ください。 PID の後に、デバイス アドレスとエンドポイントのアドレスが続きます。 コントロール転送の場合、そのエンドポイント アドレスは常に 0 です。

    次に、ホストからデータ パケット \#435 が送信されます。 PID は DATA0 であり、その値はパケット シーケンスに使用されます (これについては、これから説明します)。 PID の後には、この要求に関する主要な情報を含む 8 バイトが続きます。 これらの 8 バイトは、要求の種類と、デバイスがその応答を書き込むバッファーのサイズを示します。

    すべてのバイトは逆順で受信されます。 セクション 9.3 で説明したように、次のフィールドと値が表示されます。

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
    <th>Size</th>
    <th>値</th>
    <th>説明</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><strong>bmRequestType</strong> (「9.3.1 bmRequestType」を参照)</td>
    <td>1</td>
    <td>0x80</td>
    <td><p>データ転送方向はデバイスからホストです (D7 は 1 です)</p>
    <p>要求は標準要求です (D6...D5 は 0)</p>
    <p>要求の受信者はデバイスです (D4 は 0)</p></td>
    </tr>
    <tr class="even">
    <td><strong>bRequest</strong> (セクション 9.3.2 と表 9-4 を参照)</td>
    <td>1</td>
    <td>0x06</td>
    <td>要求の種類は GET_DESCRIPTOR です。</td>
    </tr>
    <tr class="odd">
    <td><strong>wValue</strong> (表 9-5 参照)</td>
    <td>2 で保護されたプロセスとして起動されました</td>
    <td>0x0100</td>
    <td>要求値は、記述子の種類が DEVICE であることを示します。</td>
    </tr>
    <tr class="even">
    <td><strong>wIndex</strong>(セクション 9.3.4 を参照)</td>
    <td>2 で保護されたプロセスとして起動されました</td>
    <td>0x0000</td>
    <td><p>方向はホストからデバイスです (D7 は 1)。</p>
    <p>エンドポイント番号は 0 です。</p></td>
    </tr>
    <tr class="odd">
    <td><strong>wLength</strong> (セクション 9.3.5 を参照)</td>
    <td>2 で保護されたプロセスとして起動されました</td>
    <td>0x0012</td>
    <td>要求は 18 バイトを取得することです。</td>
    </tr>
    </tbody>
    </table>

    そのため、このコントロール (読み取り) 転送では、ホストがデバイスの記述子を取得する要求を送信し、その記述子を保持するため、転送長として 18 バイトを指定するものと結論付けることができます。 デバイスが 18 バイトを送信する方法は、既定のエンドポイントが 1 回のトランザクションで送信できるデータの量によって異なります。 その情報は、データ トランザクションでデバイスによって返されるデバイスの記述子に含まれます。

    応答の中で、デバイスからハンドシェイク パケットが送信されます (\#436、**D↓** で示されます)。 PID 値が ACK (ACK パケット) であることにご注意ください。 これは、デバイスがトランザクションを受信確認したことを示します。

-   **データ トランザクション**

    次に、要求に応答してデバイスから返される内容を見てみましょう。 実際のデータは、データ トランザクションで転送されます。

    データ トランザクションのトレースは次のようになります。

    ![サンプル データ トランザクションのトレース。](images/datra-trans.png)

    ACK パケットを受信すると、ホストではデータ トランザクションが開始されます。 トランザクションを開始するために、IN 方向でトークン パケット (\#450) が送信されます (IN トークンと呼ばれています)。

    応答の中で、IN トークンに続くデータ パケット (\#451) がデバイスから送信されます。 このデータ パケットには、実際のデバイス記述子が含まれています。 最初のバイトはデバイス記述子の長さ、18 バイト (0x12) を示します。 このデータ パケットの最後のバイトは、既定のエンドポイントでサポートされる最大パケット サイズを示します。 この例の場合、デバイスが既定のエンドポイントを使用して一度に 8 バイトを送信できることがわかります。

    **注記** 既定のエンドポイントの最大パケット サイズは、デバイスの速度によって異なります。 高速デバイスの既定のエンドポイントは 64 バイトです。低速デバイスの場合は 8 バイトです。

    ホストでは ACK パケット (\#452) をデバイスに送信することでデータ トランザクションを受信確認します。

    返されるデータの量を計算しましょう。 セットアップ トランザクションのデータ パケット (\#435) の **wLength** フィールドで、ホストから 18 バイトが要求されました。 データ トランザクションで、デバイス記述子の最初の 8 バイトだけがデバイスから受信されたことがわかります。 それでは、残りの 10 バイトに保存されている情報をホストはどのように受信するのでしょうか。 デバイスではそれが次の 2 つのトランザクションで行われます。8 バイトと最後の 2 バイトです。

    これで、既定のエンドポイントの最大パケット サイズがホストに認識されたので、ホストでは、新しいデータ トランザクションを開始し、パケット サイズに基づいて次の部分を要求します。

    次のデータ トランザクションはこのようになります。

    ![サンプル データ トランザクションのトレース。](images/datra-trans2.png)

    ホストでは、IN トークン (\#463) を送信し、デバイスに次の 8 バイトを要求することで前述のデータ トランザクションを開始します。 デバイスは、デバイス記述子の次の 8 バイトを含むデータパケット (\#464) で応答します。

    8 バイトが受信されると、ホストからデバイスに ACK パケット (\#465) が送信されます。

    次に、ホストでは、次のように別のデータ トランザクションで最後の 2 バイトを要求します。

    ![サンプル データ トランザクションのトレース。](images/datra-trans3.png)

    結果的に、デバイスからホストに 18 バイトを転送するために、ホストでは転送されたバイト数を追跡記録し、3 回のデータ トランザクション (8+8+2) を開始したことがわかります。

    **注記** データ トランザクション 19、23、26 のデータ パケットの PID にご注意ください。 PID は DATA0 と DATA1 の間で交互に切り替わります。 このシーケンスはデータ切り替えと呼ばれています。 複数のデータ トランザクションが存在するとき、パケットのシーケンスを確認する目的でデータ切り替えが利用されます。 この手法により、データ パケットが重複したり、失われたりすることはありません。

    統合データ パケットをデバイス記述子の構造にマップすることで (表 9-8 参照)、次のフィールドと値が表示されます。

    | フィールド                  | Size | 値  | 説明                                                                       |
    |------------------------|------|--------|-----------------------------------------------------------------------------------|
    | **bLength**            | 1    | 0x12   | デバイス記述子の長さ (18 バイト)。                               |
    | **bDescriptorType**    | 1    | 0x01   | 記述子の種類はデバイスです。                                                    |
    | **bcdUSB**             | 2 で保護されたプロセスとして起動されました    | 0x0100 | 仕様バージョン番号は 1.00 です。                                         |
    | **bDeviceClass**       | 1    | 0x00   | デバイス クラスは 0 です。 構成内の各インターフェイスにはクラス情報が与えられます。 |
    | **bDeviceSubClass**    | 1    | 0x00   | デバイス クラスが 0 のため、サブクラスは 0 です。                                          |
    | **bProtocol**          | 1    | 0x00   | プロトコルは 0 です。 このデバイスでは、いかなるクラス固有プロトコルも使用されません。             |
    | **bMaxPacketSize0**    | 1    | 0x08   | エンドポイントの最大パケット サイズは 8 バイトです。                               |
    | **idVendor**           | 2 で保護されたプロセスとして起動されました    | 0x0562 | テレックス通信。                                                             |
    | **idProduct**          | 2 で保護されたプロセスとして起動されました    | 0x0002 | USB マイク。                                                                   |
    | **bcdDevice**          | 2 で保護されたプロセスとして起動されました    | 0x0100 | デバイスのリリース番号を示します。                                              |
    | **iManufacturer**      | 1    | 0x01   | 製造元文字列。                                                              |
    | **iProduct**           | 1    | 0x02   | 製品文字列。                                                                   |
    | **iSerialNumber**      | 1    | 0x03   | シリアル番号。                                                                    |
    | **bNumConfigurations** | 1    | 0x01   | 構成の数。                                                         |



    これらの値を調べることで、デバイスに関する予備情報を得られます。 このデバイスは低速の USB マイクです。 既定のエンドポイントの最大パケット サイズは 8 バイトです。 このデバイスでは、1 つの構成がサポートされます。

-   **ステータス トランザクション**

    最後に、ホストでは、最後のトランザクションであるステータス トランザクションを開始し、コントロール転送を完了とします。

    ![サンプル データ トランザクションのトレース。](images/status-trans.png)

    ホストは、OUT トークン パケット (\#481) でトランザクションを開始します。 このパケットの目的は、要求されたすべてのデータをデバイスが送信したことを確認することです。 このステータス トランザクションで送信されたデータ パケットはありません。 デバイスは ACK パケットで応答します。 エラーが発生した場合、PID は NAK か STALL になります。

## <a name="supported-driver-models"></a>サポートされているドライバー モデル


### <a name="related-technologies"></a>関連テクノロジ

-   [カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   [ユーザー モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   [WinUSB](winusb.md)

## <a name="prerequisites"></a>前提条件


クライアント ドライバーでパイプを列挙するには、次の要件が満たされている必要があります。

-   クライアント ドライバーによって、フレームワーク USB ターゲット デバイス オブジェクトが作成されている必要があります。

    Microsoft Visual Studio Professional 2012 に付属する USB テンプレートを使用している場合、テンプレート コードでこれらのタスクが実行されます。 テンプレート コードによりターゲット デバイス オブジェクトのハンドルが取得され、デバイス コンテキストに格納されます。

    **KMDF クライアント ドライバー: **

    KMDF クライアント ドライバーでは、[**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters) メソッドを呼び出すことで WDFUSBDEVICE ハンドルを取得する必要があります。 詳細については、「[USB クライアント ドライバー コード構造について (KMDF)](understanding-the-kmdf-template-code-for-usb.md)」の「デバイスのソース コード」を参照してください。

    **UMDF クライアント ドライバー: **

    UMDF クライアント ドライバーは、フレームワーク ターゲット デバイス オブジェクトを問い合わせることで、[**IWDFUsbTargetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice) ポインターを取得する必要があります。 詳細については、「[USB クライアント ドライバー コード構造について (UMDF)](understanding-the-umdf-template-code-for-usb.md)」の「[**IPnpCallbackHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware) 実装と USB 固有のタスク」を参照してください。

-   コントロール転送の最も重要な側面は、セットアップ トークンを正しくフォーマットすることです。 要求を送信する前に、次の一連の情報を収集します。

    -   要求の方向: ホストからデバイス、またはデバイスからホスト。
    -   要求の受信者: デバイス、インターフェイス、エンドポイント、その他。
    -   要求のカテゴリ: 標準、クラス、ベンダー。
    -   要求の種類 (GET\_DESCRIPTPOR 要求など)。 詳細については、USB 仕様のセクション 9.5 を参照してください。
    -   **wValue** 値と **wIndex** 値。 これらの値は、要求の種類によって異なります。

    この情報はすべて、公式の USB 仕様から入手できます。

-   UMDF ドライバーを記述している場合、UMDF Sample Driver for OSR USB Fx2 Learning Kit から Usb\_hw というヘッダー ファイルを取得します。 このヘッダー ファイルには、コントロール転送用のセットアップ パケットをフォーマットするための便利なマクロと構造体が含まれています。

    UMDF ドライバーはすべて、デバイスとの間でデータを送受信するために、カーネルモード ドライバーと通信する必要があります。 USB UMDF ドライバーの場合、カーネルモード ドライバーは常に Microsoft 提供ドライバー [WinUSB](winusb.md) (Winusb.sys) になります。

    UMDF ドライバーから USB ドライバー スタックが要求されるたびに、Windows I/O マネージャーでは、WinUSB に要求を送信します。 WinUSB は要求を受信すると、要求を処理するか、USB ドライバー スタックに転送します。

## <a name="microsoft-defined-methods-for-sending-control-transfer-requests"></a>コントロール転送要求を送信するための Microsoft 定義メソッド


ホスト上の USB クライアント ドライバーでは、デバイスに関する情報を取得するか、デバイスを構成するか、ベンダー コントロール コマンドを送信する目的でほとんどの制御要求を開始します。 このような要求はすべて、次に分類できます。

-   標準要求 - 標準要求は USB 仕様で定義されています。 この要求を送信する目的は、デバイス、その構成、インターフェイス、エンドポイントに関する情報を取得することです。 各要求の受信者は、要求の種類によって異なります。 受信者には、デバイス、インターフェイス、エンドポイントがあります。

    **注記** コントロール転送の転送先は常に既定のエンドポイントです。 受信者は、ホストがその情報 (記述子やステータスなど) に関心を持っているデバイスのエンティティです。

    以上の要求はさらに、構成要求、機能要求、ステータス要求に分類できます。

    -   構成要求は、ホストでそれを構成できるよう、デバイスから情報を取得する目的で送信されます。たとえば、GET\_DESCRIPTOR 要求です。 この要求は、デバイスで特定または代替の構成を設定する目的でホストにより送信される書き込み要求になることもあります。
    -   機能要求は、デバイス、インターフェイス、またはエンドポイントでサポートされている特定のブール値デバイス設定を有効または無効にする目的で、クライアント ドライバーにより送信されます。
    -   USB デバイスは、デバイス、インターフェイス、またはエンドポイントの USB 定義ステータス ビットをホストで取得または設定できるよう、ステータス要求に対応しています。

    詳細については、USB 仕様バージョン 2.0 のセクション 9.4 を参照してください。 標準要求の種類は、Usbspec.h というヘッダー ファイルに定義されています。

-   クラス要求: 特定のデバイス クラス仕様によって定義されます。
-   ベンダー要求: ベンダーにより提供され、デバイスでサポートされている要求によって異なります。

Microsoft 提供の USB スタックでは、前述のトレースで確認できるように、デバイスとのあらゆるプロトコル通信が処理されます。 ドライバーからは、クライアント ドライバーからさまざまな方法でコントロール転送を送信することを可能にするデバイス ドライバー インターフェイス (DDI) が公開されます。 クライアント ドライバーが Windows Driver Foundation (WDF) ドライバーの場合、ルーチンを直接呼び出し、一般的な種類の制御要求を送信できます。 WDF は、KMDF と UMDF の両方のコントロール転送を本質的にサポートしています。

特定の種類の制御要求は、WDF 経由で公開されません。 そのような要求の場合、クライアント ドライバーでは WDF ハイブリッド モデルを使用できます。 このモデルでは、クライアント ドライバーで WDM URB スタイルの要求を作成し、フォーマットし、WDF フレームワーク オブジェクトで送信することが可能になります。 ハイブリッド モデルは、カーネルモード ドライバーにのみ適用されます。

**UMDF ドライバーの場合:**

usb\_hw.h に定義されているヘルパー マクロと構造体を使用します。 このヘッダーは UMDF Sample Driver for OSR USB Fx2 Learning Kit に付属しています。

この表を利用し、制御要求を USB ドライバー スタックに送信するための最適な方法を決定します。 この表を表示できない場合、[こちらのトピック](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)の表を参照してください。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>制御要求を送信するには...</th>
<th>KMDF ドライバーの場合、次の KMDF DDI を使用して...</th>
<th>UMDF ドライバーの場合、次の UMDF メソッドを使用して...</th>
<th>WDM ドライバーの場合、URB 構造体 (ヘルパー ルーチン) を構築します。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>CLEAR_FEATURE:デバイス、その構成、インターフェイス、エンドポイントで特定の機能設定を無効にします。 USB 仕様のセクション 9.4.1 を参照してください。</td>
<td><ol>
<li>セットアップ パケットを宣言します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"><strong>WDF_USB_CONTROL_SETUP_PACKET</strong></a> 構造体を参照してください。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_feature" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_feature)"><strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong></a> を呼び出してセットアップ パケットを初期化します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient)"><strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a> に定義されている受信者値を指定します。</li>
<li>機能セレクターを指定します (<strong>wValue</strong>)。 Usbspec.h の「USB_FEATURE_XXX 定数」セクションを参照してください。 USB 仕様の表 9-6 も参照してください。</li>
<li><em>SetFeature</em> を <strong>FALSE</strong> に設定します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a> または <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a> を呼び出して要求を送信します。</li>
</ol></td>
<td><ol>
<li>セットアップ パケットを宣言します。 usb_hw.h で宣言されている <strong>WINUSB_CONTROL_SETUP_PACKET</strong> を参照してください。</li>
<li>usb_hw.h に定義されている <strong>WINUSB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong> というヘルパー マクロを呼び出してセットアップ パケットを初期化します。</li>
<li><strong>WINUSB_BMREQUEST_RECIPIENT</strong> に定義されている受信者値を指定します。</li>
<li>機能セレクターを指定します (<strong>wValue</strong>)。 Usbspec.h の「<strong>USB_FEATURE_XXX</strong> 定数」セクションを参照してください。 USB 仕様の表 9-6 も参照してください。</li>
<li><em>SetFeature</em> を <strong>FALSE</strong> に設定します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong></a> メソッドを呼び出し、フレームワーク要求オブジェクトと転送バッファーを初期化されたセットアップ パケットに関連付けることで要求を作成します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest::Send</strong></a> メソッドを呼び出して要求を送信します。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_feature_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_FEATURE_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_feature_request)"><strong>_URB_CONTROL_FEATURE_REQUEST</strong></a></p>
<p>(<a href="https://docs.microsoft.com/previous-versions/ff538932(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildFeatureRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538932(v=vs.85))"><strong>UsbBuildFeatureRequest</strong></a>)</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_DEVICE</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_INTERFACE</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_ENDPOINT</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_OTHER</p></td>
</tr>
<tr class="even">
<td>GET_CONFIGURATION:現在の USB 構成を取得します。 USB 仕様のセクション 9.4.2 を参照してください。</td>
<td><p>KMDF では、既定で最初の構成が選択されます。 デバイス定義の構成番号を取得するには:</p>
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"><strong>WDF_USB_CONTROL_SETUP_PACKET</strong></a> をフォーマットし、その <strong>bRequest</strong> メンバーを <strong>USB_REQUEST_GET_CONFIGURATION</strong> に設定します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a> または <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a> を呼び出して要求を送信します。</li>
</ol></td>
<td><p>UMDF では、既定で最初の構成が選択されます。 デバイス定義の構成番号を取得するには:</p>
<ol>
<li>セットアップ パケットを宣言します。 usb_hw.h で宣言されている <strong>WINUSB_CONTROL_SETUP_PACKET</strong> を参照してください。</li>
<li>usb_hw.h に定義されている <strong>WINUSB_CONTROL_SETUP_PACKET_INIT</strong> というヘルパー マクロを呼び出してセットアップ パケットを初期化します。</li>
<li>方向として <strong>BmRequestToDevice</strong> を、受信者として <strong>BmRequestToDevice</strong> を、要求として <strong>USB_REQUEST_GET_CONFIGURATION</strong> を指定します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong></a> メソッドを呼び出し、フレームワーク要求オブジェクトと転送バッファーを初期化されたセットアップ パケットに関連付けることで要求を作成します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest::Send</strong></a> メソッドを呼び出して要求を送信します。</li>
<li>転送バッファー内の構成番号を受信します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfmemory" data-raw-source="[&lt;strong&gt;IWDFMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfmemory)"><strong>IWDFMemory</strong></a> メソッドを呼び出してそのバッファーにアクセスします。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_configuration_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_CONFIGURATION_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_configuration_request)"><strong>_URB_CONTROL_GET_CONFIGURATION_REQUEST</strong></a></p>
<p>URB_FUNCTION_GET_CONFIGURATION</p></td>
</tr>
<tr class="odd">
<td>GET_DESCRIPTOR:デバイス、構成、インターフェイス、エンドポイント記述子を取得します。 USB 仕様のセクション 9.4.3 を参照してください。
<p>詳細については、「<a href="usb-descriptors.md" data-raw-source="[USB Descriptors](usb-descriptors.md)">USB 記述子</a>」を参照してください。</p></td>
<td><p>以下のメソッドを呼び出します。</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceGetDeviceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor)"><strong>WdfUsbTargetDeviceGetDeviceDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetdescriptor" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceGetDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetdescriptor)"><strong>WdfUsbInterfaceGetDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetendpointinformation" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceGetEndpointInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetendpointinformation)"><strong>WdfUsbInterfaceGetEndpointInformation</strong></a> または <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeGetInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation)"><strong>WdfUsbTargetPipeGetInformation</strong></a>。 このメソッドでは、<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_pipe_information" data-raw-source="[&lt;strong&gt;WDF_USB_PIPE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_pipe_information)"><strong>WDF_USB_PIPE_INFORMATION</strong></a> 構造体でエンドポイント記述子フィールドが返されます。</li>
</ul></td>
<td><p>以下のメソッドを呼び出します。</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::RetrieveDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor)"><strong>IWDFUsbTargetDevice::RetrieveDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getinterfacedescriptor" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::GetInterfaceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getinterfacedescriptor)"><strong>IWDFUsbInterface::GetInterfaceDescriptor</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-getinformation" data-raw-source="[&lt;strong&gt;IWDFUsbTargetPipe::GetInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-getinformation)"><strong>IWDFUsbTargetPipe::GetInformation</strong></a>。 このメソッドでは、<a href="https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information" data-raw-source="[&lt;strong&gt;WINUSB_PIPE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information)"><strong>WINUSB_PIPE_INFORMATION</strong></a> 構造体でエンドポイント記述子フィールドが返されます。</li>
</ul></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_descriptor_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_DESCRIPTOR_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_descriptor_request)"><strong>_URB_CONTROL_DESCRIPTOR_REQUEST</strong></a></p>
<p>(<a href="https://docs.microsoft.com/previous-versions/ff538943(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildGetDescriptorRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538943(v=vs.85))"><strong>UsbBuildGetDescriptorRequest</strong></a>)</p>
<p>URB_FUNCTION_GET_DESCRIPTOR_FROM_DEVICE</p>
<p>URB_FUNCTION_GET_DESCRIPTOR_FROM_ENDPOINT</p>
<p>URB_FUNCTION_GET_DESCRIPTOR_FROM_INTERFACE</p></td>
</tr>
<tr class="even">
<td>GET_INTERFACE:インターフェイスの現在の代替設定を取得します。 USB 仕様のセクション 9.4.4 を参照してください。</td>
<td><p></p>
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetinterface" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceGetInterface&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetinterface)"><strong>WdfUsbTargetDeviceGetInterface</strong></a> メソッドを呼び出し、ターゲット インターフェイス オブジェクトの WDFUSBINTERFACE ハンドルを取得します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredsettingindex" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceGetConfiguredSettingIndex&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredsettingindex)"><strong>WdfUsbInterfaceGetConfiguredSettingIndex</strong></a> メソッドを呼び出します。</li>
</ol></td>
<td><ol>
<li>ターゲット インターフェイス オブジェクトへの <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface" data-raw-source="[&lt;strong&gt;IWDFUsbInterface&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface)"><strong>IWDFUsbInterface</strong></a> ポインターを取得します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getconfiguredsettingindex" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::GetConfiguredSettingIndex&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getconfiguredsettingindex)"><strong>IWDFUsbInterface::GetConfiguredSettingIndex</strong></a> メソッドを呼び出します。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_interface_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_INTERFACE_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_interface_request)"><strong>_URB_CONTROL_GET_INTERFACE_REQUEST</strong></a></p>
<p>URB_FUNCTION_GET_INTERFACE</p></td>
</tr>
<tr class="odd">
<td>GET_STATUS:デバイス、エンドポイント、またはインターフェイスからステータス ビットを取得します。 USB 仕様のセクション 9.4.5 を ご覧ください。</td>
<td><ol>
<li>セットアップ パケットを宣言します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"><strong>WDF_USB_CONTROL_SETUP_PACKET</strong></a> 構造体を参照してください。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_get_status" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_GET_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_get_status)"><strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_GET_STATUS</strong></a> を呼び出してセットアップ パケットを初期化します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient)"><strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a> に定義されている受信者値を指定します。</li>
<li>デバイス、インターフェイス、またはエンドポイントのどのステータスを取得するかを指定します (<strong>wIndex</strong>)。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a> または <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a> を呼び出して要求を送信します。</li>
</ol></td>
<td><ol>
<li>セットアップ パケットを宣言します。 usb_hw.h で宣言されている <strong>WINUSB_CONTROL_SETUP_PACKET</strong> を参照してください。</li>
<li>usb_hw.h に定義されている <strong>WINUSB_CONTROL_SETUP_PACKET_INIT_GET_STATUS</strong> というヘルパー マクロを呼び出してセットアップ パケットを初期化します。</li>
<li><strong>WINUSB_BMREQUEST_RECIPIENT</strong> に定義されている受信者値を指定します。</li>
<li>デバイス、インターフェイス、またはエンドポイントのどのステータスを取得するかを指定します (<strong>wIndex</strong>)。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong></a> メソッドを呼び出し、フレームワーク要求オブジェクトと転送バッファーを初期化されたセットアップ パケットに関連付けることで要求を作成します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest::Send</strong></a> メソッドを呼び出して要求を送信します。</li>
<li>転送バッファーのステータス値を受信します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfmemory" data-raw-source="[&lt;strong&gt;IWDFMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfmemory)"><strong>IWDFMemory</strong></a> メソッドを呼び出してそのバッファーにアクセスします。</li>
<li>ステータスにより自己供給のリモートウェイクアップが示されるかどうかを判断するには、<strong>WINUSB_DEVICE_TRAITS</strong> 列挙型に定義されている値を使用します。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_status_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_STATUS_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_status_request)"><strong>_URB_CONTROL_GET_STATUS_REQUEST</strong></a></p>
<p>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbbuildgetstatusrequest" data-raw-source="[&lt;strong&gt;UsbBuildGetStatusRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbbuildgetstatusrequest)"><strong>UsbBuildGetStatusRequest</strong></a>)</p>
<p>URB_FUNCTION_GET_STATUS_FROM_DEVICE</p>
<p>URB_FUNCTION_GET_STATUS_FROM_INTERFACE</p>
<p>URB_FUNCTION_GET_STATUS_FROM_ENDPOINT</p>
<p>URB_FUNCTION_GET_STATUS_FROM_OTHER</p></td>
</tr>
<tr class="even">
<td>SET_ADDRESS:USB 仕様のセクション 9.4.6 を参照してください。</td>
<td>この要求は USB ドライバーによって処理されます。クライアント ドライバーではこの操作を実行できません。</td>
<td>この要求は USB ドライバーによって処理されます。クライアント ドライバーではこの操作を実行できません。</td>
<td>この要求は USB ドライバーによって処理されます。クライアント ドライバーではこの操作を実行できません。</td>
</tr>
<tr class="odd">
<td>SET_CONFIGURATION:構成を設定します。 USB 仕様のセクション 9.4.7 を参照してください。
<p>詳細については、「<a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">USB デバイス用の構成の選択方法</a>」を参照してください。</p></td>
<td>KMDF では既定で、既定の構成と各インターフェイスにおける最初の代替設定が選択されます。 クライアント ドライバーでは、<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ne-wdfusb-_wdfusbtargetdeviceselectconfigtype" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSelectConfigType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ne-wdfusb-_wdfusbtargetdeviceselectconfigtype)"><strong>WdfUsbTargetDeviceSelectConfigType</strong></a> メソッドを呼び出し、<strong>WdfUsbTargetDeviceSelectConfigTypeUrb</strong> を要求オプションとして指定することで既定の構成を変更できます。 次に、この要求の URB をフォーマットし、それを USB ドライバー スタックに提出する必要があります。</td>
<td>UMDF では既定で、既定の構成と各インターフェイスにおける最初の代替設定が選択されます。 クライアント ドライバーでは、構成を変更できません。</td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_select_configuration" data-raw-source="[&lt;strong&gt;_URB_SELECT_CONFIGURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_select_configuration)"><strong>_URB_SELECT_CONFIGURATION</strong></a></p>
<p>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild" data-raw-source="[&lt;strong&gt;USBD_SelectConfigUrbAllocateAndBuild&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)"><strong>USBD_SelectConfigUrbAllocateAndBuild</strong></a>)</p>
<p>URB_FUNCTION_SELECT_CONFIGURATION</p></td>
</tr>
<tr class="even">
<td>SET_DESCRIPTOR:既存のデバイス、構成、または文字列記述子を更新します。 USB 仕様のセクション 9.4.8 を参照してください。
<p>この要求は一般的には使用されません。 ただし、USB ドライバー スタックは、クライアント ドライバーからこのような要求を受け取ります。</p></td>
<td><ol>
<li>要求の <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)"><strong>URB</strong></a> を割り当て、構築します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_descriptor_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_DESCRIPTOR_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_descriptor_request)"><strong>_URB_CONTROL_DESCRIPTOR_REQUEST</strong></a> 構造体で転送情報を指定します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforurb" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForUrb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforurb)"><strong>WdfUsbTargetDeviceFormatRequestForUrb</strong></a> または <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendUrbSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)"><strong>WdfUsbTargetDeviceSendUrbSynchronously</strong></a> を呼び出して要求を送信します。</li>
</ol></td>
<td><ol>
<li>セットアップ パケットを宣言します。 usb_hw.h で宣言されている <strong>WINUSB_CONTROL_SETUP_PACKET</strong> を参照してください。</li>
<li>USB 仕様に従って転送情報を指定します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong></a> メソッドを呼び出し、フレームワーク要求オブジェクトと転送バッファーを初期化されたセットアップ パケットに関連付けることで要求を作成します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest::Send</strong></a> メソッドを呼び出して要求を送信します。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_descriptor_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_DESCRIPTOR_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_descriptor_request)"><strong>_URB_CONTROL_DESCRIPTOR_REQUEST</strong></a></p>
<p>URB_FUNCTION_SET_DESCRIPTOR_TO_DEVICE</p>
<p>URB_FUNCTION_SET_DESCRIPTOR_TO_ENDPOINT</p>
<p>URB_FUNCTION_SET_DESCRIPTOR_TO_INTERFACE</p></td>
</tr>
<tr class="odd">
<td>SET_FEATURE:デバイス、その構成、インターフェイス、エンドポイントで特定の機能設定を有効にします。 USB 仕様のセクション 9.4.9 を参照してください。</td>
<td><ol>
<li>セットアップ パケットを宣言します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"><strong>WDF_USB_CONTROL_SETUP_PACKET</strong></a> 構造体を参照してください。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_feature" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_feature)"><strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong></a> を呼び出してセットアップ パケットを初期化します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient)"><strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a> に定義されている受信者値 (デバイス、インターフェイス、エンドポイント) を指定します。</li>
<li>機能セレクターを指定します (<strong>wValue</strong>)。 Usbspec.h の「USB_FEATURE_XXX 定数」セクションを参照してください。 USB 仕様の表 9-6 も参照してください。</li>
<li><em>SetFeature</em> を <strong>TRUE</strong> に設定します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a> または <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a> を呼び出して要求を送信します。</li>
</ol></td>
<td><ol>
<li>セットアップ パケットを宣言します。 usb_hw.h で宣言されている <strong>WINUSB_CONTROL_SETUP_PACKET</strong> を参照してください。</li>
<li>usb_hw.h に定義されている <strong>WINUSB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong> というヘルパー マクロを呼び出してセットアップ パケットを初期化します。</li>
<li><strong>WINUSB_BMREQUEST_RECIPIENT</strong> に定義されている受信者値を指定します。</li>
<li>機能セレクターを指定します (<strong>wValue</strong>)。 Usbspec.h の「<strong>USB_FEATURE_XXX</strong> 定数」セクションを参照してください。 USB 仕様の表 9-6 も参照してください。</li>
<li><em>SetFeature</em> を <strong>TRUE</strong> に設定します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong></a> メソッドを呼び出し、フレームワーク要求オブジェクトと転送バッファーを初期化されたセットアップ パケットに関連付けることで要求を作成します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest::Send</strong></a> メソッドを呼び出して要求を送信します。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_feature_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_FEATURE_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_feature_request)"><strong>_URB_CONTROL_FEATURE_REQUEST</strong></a></p>
<p>(<a href="https://docs.microsoft.com/previous-versions/ff538932(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildFeatureRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538932(v=vs.85))"><strong>UsbBuildFeatureRequest</strong></a>)</p>
<p>URB_FUNCTION_SET_FEATURE_TO_DEVICE</p>
<p>URB_FUNCTION_SET_FEATURE_TO_INTERFACE</p>
<p>URB_FUNCTION_SET_FEATURE_TO_ENDPOINT</p>
<p>URB_FUNCTION_SET_FEATURE_TO_OTHER</p></td>
</tr>
<tr class="even">
<td>SET_INTERFACE:インターフェイスの代替設定を変更します。 USB 仕様のセクション 9.4.9 を参照してください。
<p>詳細については、「<a href="select-a-usb-alternate-setting.md" data-raw-source="[How to select an alternate setting in a USB interface](select-a-usb-alternate-setting.md)">USB インターフェイスにおける代替設定の選択方法</a>」を参照してください。</p></td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSelectConfig&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)"><strong>WdfUsbTargetDeviceSelectConfig</strong></a>
<p></p>
<ol>
<li>ターゲット インターフェイス オブジェクトへの WDFUSBINTERFACE ハンドルを取得します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceSelectSetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting)"><strong>WdfUsbInterfaceSelectSetting</strong></a> メソッドを呼び出します。</li>
</ol></td>
<td><ol>
<li>ターゲット インターフェイス オブジェクトへの <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface" data-raw-source="[&lt;strong&gt;IWDFUsbInterface&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface)"><strong>IWDFUsbInterface</strong></a> ポインターを取得します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-selectsetting" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::SelectSetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-selectsetting)"><strong>IWDFUsbInterface::SelectSetting</strong></a> メソッドを呼び出します。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_select_interface" data-raw-source="[&lt;strong&gt;_URB_SELECT_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_select_interface)"><strong>_URB_SELECT_INTERFACE</strong></a></p>
<p>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild" data-raw-source="[&lt;strong&gt;USBD_SelectInterfaceUrbAllocateAndBuild&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)"><strong>USBD_SelectInterfaceUrbAllocateAndBuild</strong></a>)</p>
<p>URB_FUNCTION_SELECT_INTERFACE</p></td>
</tr>
<tr class="odd">
<td>SYNC_FRAME:エンドポイントの同期フレーム番号を設定し、取得します。 USB 仕様のセクション 9.4.10 を参照してください。</td>
<td>この要求は USB ドライバーによって処理されます。クライアント ドライバーではこの操作を実行できません。</td>
<td>この要求は USB ドライバーによって処理されます。クライアント ドライバーではこの操作を実行できません。</td>
<td>この要求は USB ドライバーによって処理されます。クライアント ドライバーではこの操作を実行できません。</td>
</tr>
<tr class="even">
<td>デバイス クラス固有の要求とベンダーコマンド用。</td>
<td><ol>
<li>セットアップ パケットを宣言します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet)"><strong>WDF_USB_CONTROL_SETUP_PACKET</strong></a> 構造体を参照してください。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_class" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_CLASS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_class)"><strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_CLASS</strong></a> 固有要件または <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_vendor" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_VENDOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_control_setup_packet_init_vendor)"><strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_VENDOR</strong></a> (ベンダー コマンド用) を呼び出し、セットアップ パケットを初期化します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ne-wdfusb-_wdf_usb_bmrequest_recipient)"><strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a> に定義されている受信者値 (デバイス、インターフェイス、エンドポイント) を指定します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a> または <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a> を呼び出して要求を送信します。</li>
</ol></td>
<td><ol>
<li>セットアップ パケットを宣言します。 usb_hw.h で宣言されている <strong>WINUSB_CONTROL_SETUP_PACKET</strong> を参照してください。</li>
<li>usb_hw.h に定義されている <strong>WINUSB_CONTROL_SETUP_PACKET_INIT_CLASS</strong> または <strong>WINUSB_CONTROL_SETUP_PACKET_INIT_VENDOR</strong> というヘルパー マクロを呼び出してセットアップ パケットを初期化します。</li>
<li>クラスまたはハードウェア仕様の説明を参照し、方向 (<strong>WINUSB_BMREQUEST_DIRECTION</strong> 列挙型を参照)、受信者 (<strong>WINUSB_BMREQUEST_RECIPIENT</strong> 列挙型を参照)、要求を指定します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong></a> メソッドを呼び出し、フレームワーク要求オブジェクトと転送バッファーを初期化されたセットアップ パケットに関連付けることで要求を作成します。</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest::Send</strong></a> メソッドを呼び出して要求を送信します。</li>
<li>転送バッファー内のデバイスから情報を受信します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfmemory" data-raw-source="[&lt;strong&gt;IWDFMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfmemory)"><strong>IWDFMemory</strong></a> メソッドを呼び出してそのバッファーにアクセスします。</li>
</ol></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_vendor_or_class_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_VENDOR_OR_CLASS_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_vendor_or_class_request)"><strong>_URB_CONTROL_VENDOR_OR_CLASS_REQUEST</strong></a></p>
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



## <a name="how-to-send-a-control-transfer-for-vendor-commands---kmdf"></a>ベンダー コマンドのコントロール転送を送信する方法 - KMDF


この手順からは、クライアント ドライバーでコントロール転送を送信するしくみがわかります。 この例では、クライアント ドライバーからベンダー コマンドが送信され、そのコマンドでデバイスからファームウェア バージョンが取得されます。

1.  ベンダー コマンドの定数を宣言します。 ハードウェア仕様を調べ、使用するベンダー コマンドを決めます。
2.  [**WDF\_MEMORY\_DESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/ns-wdfmemory-_wdf_memory_descriptor) 構造体を宣言し、[**WDF\_MEMORY\_DESCRIPTOR\_INIT\_BUFFER**](https://msdn.microsoft.com/library/windows/hardware/ff552392_init_buffer) マクロを呼び出してそれを初期化します。 この構造は、USB ドライバーで要求が完了した後、デバイスから応答を受信します。
3.  要求の送信を同期にするのか、非同期にするのかに合わせて送信オプションを指定します。
    -   [**WdfUsbTargetDeviceSendControlTransferSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously) を呼び出して要求を同期で送信する場合、タイムアウト値を指定します。 タイムアウトなしでは、スレッドが無限にブロックされる可能性があるため、この値は重要です。

        そのため、[**WDF\_REQUEST\_SEND\_OPTIONS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ns-wdfrequest-_wdf_request_send_options) 構造体を宣言し、[**WDF\_REQUEST\_SEND\_OPTIONS\_INIT**](https://msdn.microsoft.com/library/windows/hardware/ff552491_init) マクロを呼び出してそれを初期化します。 オプションとして **WDF\_REQUEST\_SEND\_OPTION\_TIMEOUT** を指定します。

        次に、[**WDF\_REQUEST\_SEND\_OPTIONS\_SET\_TIMEOUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdf_request_send_options_set_timeout) マクロを呼び出し、タイムアウト値を設定します。

    -   要求を非同期で送信する場合は、完了ルーチンを実装します。 完了ルーチンで、割り当てられているすべてのリソースを解放します。

4.  セットアップ トークンを含める [**WDF\_USB\_CONTROL\_SETUP\_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_control_setup_packet) 構造体を宣言し、構造体をフォーマットします。 これを行うには、[**WDF\_USB\_CONTROL\_SETUP\_PACKET\_INIT\_VENDOR**](https://msdn.microsoft.com/library/windows/hardware/ff552568_init_vendor) マクロを呼び出し、セットアップ パケットをフォーマットします。 呼び出しで、要求の方向、受信者、要求送信オプション (手順 3 で初期化)、ベンダー コマンドの定数を指定します。
5.  [**WdfUsbTargetDeviceSendControlTransferSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously) または [**WdfUsbTargetDeviceFormatRequestForControlTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer) を呼び出して要求を送信します。
6.  フレームワークによって返された NTSTATUS 値を確認して受信した値を調べます。

このコード例では、コントロール転送要求が USB デバイスに送信され、そのファームウェア バージョンが取得されます。 要求は同期で送信され、クライアント ドライバーにより、5 秒 (100 ナノ秒単位) という相対的タイムアウト値が指定されます。 ドライバーにより、受信した応答がドライバー定義のデバイス コンテキストに格納されます。

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

##<a name="how-to-send-a-control-transfer-for-get_status---umdf"></a><a name="how-to-send-a-control-transfer-for-get_status---umdf"></a>GET\_STATUS のコントロール転送を送信する方法 - UMDF


この手順からは、GET\_STATUS コマンドの場合にクライアント ドライバーでコントロール転送を送信するしくみがわかります。 要求の受信者はデバイスであり、要求によりビット D1-D0 の情報が取得されます。 詳細については、USB 仕様の図 9-4 を参照してください。

1.  UMDF Sample Driver for OSR USB Fx2 Learning Kit に付属する Usb\_hw.h というヘッダー ファイルを含めます。
2.  **WINUSB\_CONTROL\_SETUP\_PACKET** 構造体を宣言します。
3.  **WINUSB\_CONTROL\_SETUP\_PACKET\_INIT\_GET\_STATUS** というヘルパー マクロを呼び出し、セットアップ パケットを初期化します。
4.  受信者として **BmRequestToDevice** を指定します。
5.  *Index* 値に 0 を指定します。
6.  ヘルパー メソッド SendControlTransferSynchronously を呼び出し、要求を同期で送信します。

    ヘルパー メソッドが [**IWDFUsbTargetDevice::FormatRequestForControlTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer) メソッドを呼び出し、フレームワーク要求オブジェクトと転送バッファーを初期化されたセットアップ パケットに関連付けることで要求が作成されます。 次に、ヘルパー メソッドが [**IWDFIoRequest::Send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send) メソッドを呼び出して要求が送信されます。 メソッドが戻ったら、返された値を調べます。

7.  ステータスにより自己供給のリモートウェイクアップが示されるかどうかを判断するには、**WINUSB\_DEVICE\_TRAITS** 列挙型に定義されている値を使用します。

このコード例では、デバイスのステータスを取得する目的でコントロール転送要求が送信されます。 この例では、SendControlTransferSynchronously という名前のヘルパー メソッドを呼び出すことで要求が同期で送信されます。

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

次のコード例では、SendControlTransferSynchronously という名前のヘルパー メソッドの実装を確認できます。 このメソッドでは、要求が同期で送信されます。

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


デバイスの関数ドライバーとして Winusb.sys を使用している場合、アプリケーションからコントロール転送を送信できます。 WinUSB のセットアップ パケットをフォーマットするには、このトピックの表で説明されている、UMDF のヘルパー マクロと構造体を使用します。 要求を送信するには、[**WinUsb\_ControlTransfer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer) 関数を呼び出します。








