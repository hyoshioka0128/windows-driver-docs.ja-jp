---
Description: このトピックでは、コントロールの転送とクライアント ドライバーがデバイスを制御要求を送信する必要がある方法の構造について説明します。
title: USB コントロール転送の送信方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af468cb6a9960169bedc56e37253691ac01f8b3b
ms.sourcegitcommit: 0504cc497918ebb7b41a205f352046a66c0e26a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2019
ms.locfileid: "65405080"
---
# <a name="how-to-send-a-usb-control-transfer"></a>USB コントロール転送の送信方法


このトピックでは、コントロールの転送とクライアント ドライバーがデバイスを制御要求を送信する必要がある方法の構造について説明します。

このトピックの内容:

-   [既定のエンドポイントについて](#about-the-default-endpoint)
-   [転送コントロールのレイアウト](#layout-of-a-control-transfer)
-   [サポートされているドライバー モデル](#supported-driver-models)
    -   [関連テクノロジ](#related-technologies)
-   [前提条件](#prerequisites)
-   [コントロールを送信するためのメソッドの Microsoft による要求を転送します。](#microsoft-defined-methods-for-sending-control-transfer-requests)
-   [仕入先コマンド - KMDF の制御の移動を送信する方法](#how-to-send-a-control-transfer-for-vendor-commands---kmdf)
-   [GET の制御の移動を送信する方法\_状態 - UMDF](#how-to-send-a-control-transfer-for-get_status---umdf)

## <a name="about-the-default-endpoint"></a>既定のエンドポイントについて


すべての USB デバイスと呼ばれる 1 つ以上のエンドポイントをサポートする必要があります、*既定のエンドポイント*します。 既定のエンドポイントを対象とするすべての転送と呼ばれる、*転送を制御*します。 コントロールの転送では、デバイス情報を取得するには、デバイスを構成するホストを有効にするか、デバイスに固有の管理操作を実行します。

既定のエンドポイントのこれらの特性の調査を見てみましょう。

-   既定のエンドポイントのアドレスには 0 です。
-   既定のエンドポイントは双方向、つまり、ホストがエンドポイントにデータを送信し、転送は 1 つ内からデータを受信できます。
-   既定のエンドポイントは、デバイス レベルで使用し、デバイスの任意のインターフェイスで定義されていません。
-   既定のエンドポイントは、ホストとデバイス間の接続が確立されているとすぐにアクティブです。 構成が選択されていなくてがアクティブです。
-   既定のエンドポイントの最大パケット サイズは、デバイスのバス速度に依存します。 低速、8 バイトです。完全な高の速度では、64 バイトです。SuperSpeed、512 バイトです。

## <a name="layout-of-a-control-transfer"></a>転送コントロールのレイアウト


コントロールの転送が高優先順位の転送であるため、一定量の帯域幅がホストによってバスに予約されています。 低とフル スピード デバイスの場合、帯域幅の 10%高の 20%、SuperSpeed デバイスを転送します。 ここで、コントロールの転送のレイアウトを見てみましょう。

![usb 制御転送](images/control-transfer.png)

コントロールの転送は 3 つのトランザクションに分かれています:*セットアップ トランザクション*、*データ トランザクション*と*状態のトランザクション*。 各トランザクションには、次の 3 つの種類パケットにはが含まれています:*トークン パケット*、*データ パケット*、および*ハンドシェイク パケット*します。

特定のフィールドは、すべてのパケットに共通です。 これらのフィールドは次のとおりです。

-   パケットの開始を示すフィールドを同期します。
-   トランザクションの成功または失敗を示しますが、ハンドシェイク パケットの場合、トランザクションの方向、パケットの種類を示すパケット識別子 (PID)。
-   EOP フィールドでは、パケットの末尾を示します。

その他のフィールドは、パケットの種類によって異なります。

-   **トークンのパケット**

    セットアップのすべてのトランザクションは、トークンのパケットで始まります。 パケットの構造を次に示します。 常に、ホストには、トークンのパケットが送信されます。

    ![トークンのパケットのレイアウト](images/token.png)

    PID 値では、トークンのパケットの種類を示します。 使用可能な値を次に示します。

    -   セットアップ:コントロールの転送でのセットアップ トランザクションの開始を示します。
    -   IN:ホストが (読み取りの場合)、デバイスからデータを要求することを示します。
    -   送信メール:ホストがデバイス (書き込みの場合) にデータを送信していることを示します。
    -   SOF:フレームの開始を示します。 この種類トークンのパケットにはには、11 ビット フレーム番号が含まれています。 ホストには、SOF パケットが送信されます。 このパケットが送信される頻度は、バス速度によって異なります。 完全な速度は、ホスト、パケットを送信すべて 1millisecond;高速バス上のすべて 125 マイクロします。

<!-- -->

-   **データ パケット**

    すぐに次のトークンのパケットは、ペイロードを含むデータ パケットです。 各データ パケットに格納できるバイト数は、既定のエンドポイントの最大パケット サイズに依存します。 ホストまたは転送の方向に応じて、デバイスのいずれかによって、データ パケットを送信できます。

    ![データ パケットのレイアウト](images/data.png)

<!-- -->

-   **ハンドシェイク パケット**

    すぐに次のデータ パケットは、ハンドシェイク パケットです。 パケットの PID は、ホストまたはデバイスで、パケットを受信したかどうかを示します。 ホストまたは転送の方向に応じて、デバイスのいずれかによって、ハンドシェイク パケットを送信できます。

    ![ハンドシェイク パケットのレイアウト](images/handshake.png)

Beagle、Ellisys、LeCroy USB プロトコル アナライザーなどの任意の USB アナライザーを使用して、トランザクションとパケットの構造を確認できます。 アナライザー、デバイスは、データを送信または、ネットワーク経由で USB デバイスから受信する方法を示します。 この例では、LeCroy USB アナライザーによってキャプチャされた一部のトレースを調べてみましょう。 この例では、参照するだけです。 これは Microsoft によって、保証ではありません。

-   **トランザクションをセットアップします。**

    ホストは、常にコントロールの転送を開始します。 これには、セットアップ トランザクションを送信します。 このトランザクションにはと呼ばれるトークンのパケットが含まれています*セットアップ トークン*8 バイトのデータ パケットを続けています。 このスクリーン ショットでは、セットアップ トランザクションの例を示します。

    ![セットアップのトランザクションのトレース。](images/setup-trans.png)

    ホストを開始する前は、トレース内 (によって示される**H↓**) セットアップ トークン パケットを送信することによって制御転送\#434 します。 PID がセットアップ トークンを示すセットアップを指定することに注意してください。 PID は続いて、デバイスのアドレスとエンドポイントのアドレス。 コントロールの転送、そのエンドポイント アドレスは常に 0 です。

    次に、データ パケットの送信ホスト\#435 します。 PID は、data 0 および (について説明します) にパケットの優先順位の値を使用するには。 PID には、この要求に関する主な情報を含む 8 バイトが続きます。 この 8 バイト領域は、要求の種類と、デバイスがその応答を書き込むバッファーのサイズを示します。

    すべてのバイトは、逆の順序で受信されます。 セクション 9.3 のように、これらのフィールドと値がわかります。

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
    <td><strong>bmRequestType</strong> (を参照してください 9.3.1 bmRequestType)</td>
    <td>1</td>
    <td>0x80</td>
    <td><p>データ転送の方向をデバイスからホストには (D7 は 1)</p>
    <p>要求が標準の要求 (D6.D5 には 0)</p>
    <p>要求の受信者は、デバイス (D4 は 0)</p></td>
    </tr>
    <tr class="even">
    <td><strong>bRequest</strong> (9.3.2「」を参照および表 9-4 を参照してください)</td>
    <td>1</td>
    <td>0x06</td>
    <td>要求の種類は、GET_DESCRIPTOR です。</td>
    </tr>
    <tr class="odd">
    <td><strong>wValue</strong> (「表 9-5)</td>
    <td>2</td>
    <td>0x0100</td>
    <td>要求の値は、記述子の種類がデバイスであることを示します。</td>
    </tr>
    <tr class="even">
    <td><strong>wIndex</strong>(9.3.4 セクションを参照してください)</td>
    <td>2</td>
    <td>0x0000</td>
    <td><p>方向は、ホストからデバイス (D7 は 1) には</p>
    <p>エンドポイントの数には 0 です。</p></td>
    </tr>
    <tr class="odd">
    <td><strong>wLength</strong> (9.3.5 セクションを参照してください)</td>
    <td>2</td>
    <td>0x0012</td>
    <td>要求では、18 バイトを取得します。</td>
    </tr>
    </tbody>
    </table>

    したがって、ことでこのコントロール (読み取り) 転送ホスト デバイス記述子を取得する要求を送信、18 バイトとして指定その記述子を保持するために転送の長さを判断できます。 デバイスが送信する 18 バイト数。 これらは、データの量によって異なります。 方法は、既定のエンドポイントは、1 つのトランザクションで送信できます。 データのトランザクションで、デバイスによって返されるデバイス記述子では、その情報が含まれます。

    デバイスに応じて、ハンドシェイク パケットを送信します (\#によって示される 436 **D↓**)。 PID 値が確認 (ACK パケット) に注意してください。 これは、デバイスが、トランザクションを確認することを示します。

-   **データのトランザクション**

    ここで、デバイスが戻る、要求に応答を見てみましょう。 実際のデータは、データのトランザクションで転送されます。

    データのトランザクションのトレースを次に示します。

    ![データ トランザクションの例のトレース。](images/datra-trans.png)

    ACK パケットを受信するとは、ホストは、データのトランザクションを開始します。 トークンのパケットを送信、トランザクションを開始する (\#450) (で呼び出されたトークン) のようにの方向を使用します。

    デバイスに応じて、データ パケットを送信します (\#451) 内のトークンが続きます。 このデータ パケットには、実際のデバイスの記述子が含まれています。 最初のバイトでは、デバイスの記述子、18 バイト (0x12) の長さを示します。 このデータ パケットの最後のバイトは、パケットの最大サイズは、既定のエンドポイントでサポートされていることを示します。 ここで、デバイスがその既定のエンドポイントを一度に 8 バイトを送信できることがわかります。

    **注**既定のエンドポイントの最大パケット サイズ、デバイスの速度に依存します。 高速のデバイスの既定のエンドポイントは 64 バイトです。低速デバイスは、8 バイトです。

    ホストが ACK パケットを送信することによって、データのトランザクションを確認 (\#452) デバイスにします。

    返されるデータの量を計算してみましょう。 **WLength**データ パケットのフィールド (\#435) セットアップのトランザクションで、ホストは 18 バイトを要求します。 データのトランザクションで、デバイスからのみデバイス記述子の最初の 8 バイトを受信したことがわかります。 そのため、ホストが残りの 10 バイトで格納されている情報に表示されるでしょうか。 デバイスは 2 つのトランザクション。8 バイトとし、最後の 2 つのバイト数。

    これで、ホストは、既定のエンドポイントの最大パケット サイズを知っていれば、ホストは新しいデータ トランザクションを開始し、パケット サイズに基づいて、次の部分を要求します。

    データの次のトランザクションを次に示します。

    ![データ トランザクションの例のトレース。](images/datra-trans2.png)

    ホストのトークンを送信することによって、前のデータ トランザクションを開始します (\#463) と、デバイスから、次の 8 バイトを要求します。 デバイスは、データ パケットで応答 (\#464) デバイス記述子の次の 8 バイトを格納しています。

    8 バイトを受信すると、ホストが ACK パケットを送信 (\#465) デバイスにします。

    次に、ホストが別のデータ トランザクションで最後の 2 バイトを次のように、要求します。

    ![データ トランザクションの例のトレース。](images/datra-trans3.png)

    そのため、18 バイトをデバイスからホストに転送する、ホストの保存されるバイトの 3 つのデータを転送し、開始されたトランザクションの数が表示 (8 + 8 + 2)。

    **注**データ トランザクション 19、23、26 のデータ パケットの PID に注意してください。 PID は、DATA0、DATA1 で交互に表示します。 このシーケンスは、データの切り替えと呼ばれます。 場合、パケットのシーケンスの検証に使用データの切り替えが複数のデータのトランザクションがある場合。 このメソッドは、データ パケットがない重複または失われたことを確認します。

    デバイス記述子 (「表 9-8) の構造に統合されたデータ パケットをマップすることによって、これらのフィールドと値を表示します。

    | フィールド                  | サイズ | 値  | 説明                                                                       |
    |------------------------|------|--------|-----------------------------------------------------------------------------------|
    | **bLength**            | 1    | 0x12   | デバイス記述子は、これは 18 バイトの長さ。                               |
    | **bDescriptorType**    | 1    | 0x01   | 記述子の型は、デバイスです。                                                    |
    | **bcdUSB**             | 2    | 0x0100 | 仕様のバージョン番号は、1.00 です。                                         |
    | **bDeviceClass**       | 1    | 0x00   | デバイス クラスには 0 です。 構成内の各インターフェイスには、クラスの情報があります。 |
    | **bDeviceSubClass**    | 1    | 0x00   | デバイスのクラスが 0 であるために、サブクラスは 0 です。                                          |
    | **bProtocol**          | 1    | 0x00   | プロトコルには 0 です。 このデバイスは、クラス固有のプロトコルを使用しません。             |
    | **bMaxPacketSize0**    | 1    | 0x08   | エンドポイントの最大パケット サイズは 8 バイトです。                               |
    | **idVendor**           | 2    | 0x0562 | テレックス通信します。                                                             |
    | **idProduct**          | 2    | 0x0002 | USB のマイクです。                                                                   |
    | **bcdDevice**          | 2    | 0x0100 | デバイスのリリース番号を示します。                                              |
    | **iManufacturer**      | 1    | 0x01   | 製造元の文字列。                                                              |
    | **iProduct**           | 1    | 0x02   | 製品の文字列。                                                                   |
    | **iSerialNumber**      | 1    | 0x03   | シリアル番号。                                                                    |
    | **bNumConfigurations** | 1    | 0x01   | 構成の数。                                                         |



    これらの値を調べることで、デバイスの事前情報があります。 デバイスは、低速の USB マイクです。 既定のエンドポイントの最大パケット サイズは 8 バイトです。 デバイスは、1 つの構成をサポートします。

-   **トランザクションの状態**

    最後のトランザクションを開始することによって、ホストがコントロールの転送を完了する最後に、: 状態のトランザクション。

    ![データ トランザクションの例のトレース。](images/status-trans.png)

    ホストにパケットを出力トークンにトランザクションを開始する (\#481)。 このパケットでは、デバイスにはすべての要求されたデータが送信されることを確認します。 この状態のトランザクションで送信されるデータ パケットはありません。 デバイスは、ACK パケットに応答します。 エラーが発生した場合は、NAK または停止のいずれか、PID をされている可能性があります。

## <a name="supported-driver-models"></a>サポートされているドライバー モデル


### <a name="related-technologies"></a>関連テクノロジ

-   [カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   [ユーザー モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   [WinUSB](winusb.md)

## <a name="prerequisites"></a>前提条件


クライアント ドライバーでは、パイプを列挙できます、前に、これらの要件を満たしていることを確認します。

-   クライアント ドライバー フレームワーク USB ターゲット デバイス オブジェクトを作成する必要があります。

    Microsoft Visual Studio Professional 2012 と共に用意されている USB テンプレートを使用する場合、テンプレート コードは、これらのタスクを実行します。 テンプレート コードでは、ターゲット デバイス オブジェクトを識別するハンドルを取得し、デバイス コンテキストに格納します。

    * * クライアント ドライバーの KMDF: * *

    KMDF クライアント ドライバーは、呼び出すことによって WDFUSBDEVICE ハンドルを取得する必要があります、 [ **WdfUsbTargetDeviceCreateWithParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh439428)メソッド。 詳細については、「デバイスのソース コード」を参照してください[USB クライアント ドライバー コード構造 (KMDF) について](understanding-the-kmdf-template-code-for-usb.md)します。

    * * クライアント ドライバーの UMDF: * *

    UMDF クライアント ドライバーを入手する必要があります、 [ **IWDFUsbTargetDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff560362)フレームワーク ターゲットのデバイス オブジェクトのクエリを実行してポインター。 詳細については、次を参照してください。"[**IPnpCallbackHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556764)実装と USB の特定のタスク"で[USB クライアント ドライバー コード構造 (UMDF) について](understanding-the-umdf-template-code-for-usb.md)します。

-   コントロールの転送の最も重要な側面では、セットアップ トークンを適切に書式設定します。 要求を送信する前に、この一連の情報を収集します。

    -   要求の方向: デバイスまたはホストにデバイスをホストします。
    -   要求の受信者: デバイス、インターフェイス、エンドポイント、またはその他。
    -   要求のカテゴリ: standard、クラス、またはベンダー。
    -   GET などの要求の種類\_DESCRIPTPOR 要求。 詳細については、USB 仕様の 9.5」セクションを参照してください。
    -   **wValue**と**wIndex**値。 これらの値は、要求の種類によって異なります。

    公式の USB 仕様からすべての情報を取得できます。

-   UMDF ドライバーを作成する場合は、Usb、ヘッダー ファイルを取得\_hw.h OSR USB Fx2 Learning kit UMDF ドライバーのサンプルから。 このヘッダー ファイルには、便利なマクロと制御の移動のセットアップのパケットを書式設定の構造が含まれています。

    すべて UMDF ドライバーは、デバイスからデータを送受信するには、カーネル モード ドライバーと通信する必要があります。 USB UMDF ドライバーの場合は常に、Microsoft 提供のドライバーには、カーネル モード ドライバー [WinUSB](winusb.md) (Winusb.sys)。

    UMDF ドライバーでは、USB ドライバー スタックの要求を行う、たびに、Windows I/O マネージャーは WinUSB に要求を送信します。 要求を受け取った後 WinUSB は要求を処理するか、または USB ドライバー スタックに転送。

## <a name="microsoft-defined-methods-for-sending-control-transfer-requests"></a>コントロールを送信するためのメソッドの Microsoft による要求を転送します。


ホスト上の USB クライアント ドライバーは、ほとんどのコントロールを開始します。 デバイスに関する情報を取得、デバイスの構成または仕入先の送信要求の制御コマンド。 これらの要求のすべてに分類できます。

-   標準的な要求: 標準的な要求は、USB 仕様で定義されます。 これらの要求を送信する目的は、デバイス、その構成、インターフェイス、およびエンドポイント情報を入手します。 各要求の受信者は、要求の種類によって異なります。 受信者は、デバイス、インターフェイス、エンドポイントを指定できます。

    **注**コントロールのすべての転送の対象は、既定のエンドポイントでは常にします。 受信デバイスがデバイスのエンティティ、ホストが興味を情報 (記述子、状態、およびなど) です。

    これらの要求をさらに分類できます。 要求の構成、機能要求、および状態要求。

    -   GET など、ホストで構成できるようにするために、デバイスから情報を取得する構成要求が送信されます\_記述子の要求。 これらの要求には、書き込み要求、デバイスで特定の構成または代替の設定を設定する、ホストによって送信されることができます。
    -   機能要求は、有効または、デバイス、インターフェイス、またはエンドポイントでサポートされている特定のブール型のデバイス設定を無効にするクライアント ドライバーによって送信されます。
    -   USB デバイスは、ホストの取得を有効にするか、デバイス、エンドポイント、またはインターフェイスの USB 定義のステータス ビットを設定する状態要求をサポートします。

    詳細については、USB 仕様、バージョン 2.0 で 9.4 のセクションを参照してください。 標準の要求の種類が定義されているヘッダー ファイル、Usbspec.h します。

-   クラスの要求-特定のデバイス クラス仕様によって定義されます。
-   仕入先の要求-は、ベンダーによって提供され、デバイスでサポートされている要求に依存します。

Microsoft 提供の USB スタックは、上記のトレースで示すように、デバイスとプロトコルのすべての通信を処理します。 ドライバーは、さまざまな方法でコントロールの転送を送信するためのクライアント ドライバーを有効にするデバイス ドライバー インターフェイス (Ddi) を公開します。 クライアント ドライバーが Windows Driver Foundation (WDF) ドライバーの場合、一般的な種類のコントロール要求を送信するには、直接ルーチンを呼び出すことができます。 WDF は、KMDF と UMDF の両方の本質的にコントロールの転送をサポートします。

特定の種類のコントロール要求は、WDF で公開されていません。 これらの要求では、クライアント ドライバーは WDF ハイブリッド モデルを使用できます。 このモデルには、ビルド、WDM URB スタイルの要求の書式設定し、WDF framework オブジェクトを使用してそれらの要求を送信して、クライアント ドライバーができます。 ハイブリッド モデルは、カーネル モード ドライバーにのみ適用されます。

**UMDF ドライバー。**

ヘルパー マクロと usb で定義された構造を使用して、\_hw.h します。 このヘッダーは、OSR USB Fx2 Learning kit UMDF ドライバーのサンプルに含まれています。

このテーブルを使用すると、USB ドライバー スタックにコントロールの要求を送信するのに最善の方法を判断できます。 このテーブルに表示されない場合は、表を参照して[このトピックの「](https://msdn.microsoft.com/library/ff539261(VS.85).aspx)します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>コントロールの要求を送信する場合.</th>
<th>KMDF ドライバーの場合は、これらの KMDF Ddi を使用してください.</th>
<th>UMDF ドライバーの場合は、これらの UMDF メソッドを使用してください.</th>
<th>WDM ドライバーの場合は、ビルド、URB 構造 (ヘルパー ルーチン)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>CLEAR_FEATURE:デバイス、その構成、インターフェイス、およびエンドポイントで特定の機能設定を無効にします。 USB 仕様の 9.4.1」セクションを参照してください。</td>
<td><ol>
<li>セットアップのパケットを宣言します。 参照してください、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff552568" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552568)"> <strong>WDF_USB_CONTROL_SETUP_PACKET</strong> </a>構造体。</li>
<li>セットアップのパケットを呼び出すことによって初期化<a href="https://msdn.microsoft.com/library/windows/hardware/ff552576" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552576)"> <strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong></a>します。</li>
<li>定義されている受信者の値を指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff552554" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552554)"> <strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a>します。</li>
<li>機能のセレクターを指定 (<strong>wValue</strong>)。 Usbspec.h USB_FEATURE_XXX 定数を参照してください。 USB 仕様では、表 9-6 を参照してください。</li>
<li>設定<em>SetFeature</em>に<strong>FALSE</strong>します。</li>
<li>呼び出すことによって、要求を送信<a href="https://msdn.microsoft.com/library/windows/hardware/ff550104" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550104)"> <strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff550082" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550082)"> <strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a>.</li>
</ol></td>
<td><ol>
<li>セットアップのパケットを宣言します。 参照してください、 <strong>WINUSB_CONTROL_SETUP_PACKET</strong> usb_hw.h で構造体を宣言します。</li>
<li>セットアップのパケットをヘルパー マクロを呼び出すことによって初期化<strong>WINUSB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong>usb_hw.h で定義されている。</li>
<li>定義されている受信者の値を指定<strong>WINUSB_BMREQUEST_RECIPIENT</strong>します。</li>
<li>機能のセレクターを指定 (<strong>wValue</strong>)。 参照してください<strong>USB_FEATURE_XXX</strong> Usbspec.h で使用される定数。 USB 仕様では、表 9-6 を参照してください。</li>
<li>設定<em>SetFeature</em>に<strong>FALSE</strong>します。</li>
<li>呼び出して framework 要求オブジェクトと転送バッファーとセットアップの初期化されたパケットを関連付けることによって、要求をビルド<a href="https://msdn.microsoft.com/library/windows/hardware/ff560363" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560363)"> <strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong> </a>メソッド.</li>
<li>呼び出すことによって、要求を送信、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559149" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559149)"> <strong>IWDFIoRequest::Send</strong> </a>メソッド。</li>
</ol></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540361" data-raw-source="[&lt;strong&gt;_URB_CONTROL_FEATURE_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540361)"><strong>_URB_CONTROL_FEATURE_REQUEST</strong></a></p>
<p>(<a href="https://msdn.microsoft.com/library/windows/hardware/ff538932" data-raw-source="[&lt;strong&gt;UsbBuildFeatureRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538932)"><strong>UsbBuildFeatureRequest</strong></a>)</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_DEVICE</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_INTERFACE</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_ENDPOINT</p>
<p>URB_FUNCTION_CLEAR_FEATURE_TO_OTHER</p></td>
</tr>
<tr class="even">
<td>GET_CONFIGURATION:USB の現在の構成を取得します。 USB 仕様の 9.4.2」セクションを参照してください。</td>
<td><p>KMDF は、既定では、最初の構成を選択します。 デバイス定義の構成の数を取得するには。</p>
<ol>
<li>形式を<a href="https://msdn.microsoft.com/library/windows/hardware/ff552568" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552568)"> <strong>WDF_USB_CONTROL_SETUP_PACKET</strong> </a>設定とその<strong>bRequest</strong>メンバー <strong>USB_REQUEST_GET_CONFIGURATION</strong>します。</li>
<li>呼び出すことによって、要求を送信<a href="https://msdn.microsoft.com/library/windows/hardware/ff550104" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550104)"> <strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff550082" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550082)"> <strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a>.</li>
</ol></td>
<td><p>UMDF は、既定では、最初の構成を選択します。 デバイス定義の構成の数を取得するには。</p>
<ol>
<li>セットアップのパケットを宣言します。 参照してください、 <strong>WINUSB_CONTROL_SETUP_PACKET</strong> usb_hw.h で構造体を宣言します。</li>
<li>セットアップのパケットをヘルパー マクロを呼び出すことによって初期化<strong>WINUSB_CONTROL_SETUP_PACKET_INIT</strong>usb_hw.h で定義されている。</li>
<li>指定<strong>BmRequestToDevice</strong>方向として<strong>BmRequestToDevice</strong>受信者であると<strong>USB_REQUEST_GET_CONFIGURATION</strong>の要求とします。</li>
<li>呼び出して framework 要求オブジェクトと転送バッファーとセットアップの初期化されたパケットを関連付けることによって、要求をビルド<a href="https://msdn.microsoft.com/library/windows/hardware/ff560363" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560363)"> <strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong> </a>メソッド.</li>
<li>呼び出すことによって、要求を送信、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559149" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559149)"> <strong>IWDFIoRequest::Send</strong> </a>メソッド。</li>
<li>転送バッファーで構成数が表示されます。 そのバッファーを呼び出すことによってアクセス<a href="https://msdn.microsoft.com/library/windows/hardware/ff559249" data-raw-source="[&lt;strong&gt;IWDFMemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559249)"> <strong>IWDFMemory</strong> </a>メソッド。</li>
</ol></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540365" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_CONFIGURATION_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540365)"><strong>_URB_CONTROL_GET_CONFIGURATION_REQUEST</strong></a></p>
<p>URB_FUNCTION_GET_CONFIGURATION</p></td>
</tr>
<tr class="odd">
<td>GET_DESCRIPTOR:デバイス、構成、インターフェイス、およびエンドポイントの記述子を取得します。 USB 仕様の 9.4.3」セクションを参照してください。
<p>詳細については、次を参照してください。<a href="usb-descriptors.md" data-raw-source="[USB Descriptors](usb-descriptors.md)">の USB ディスクリプター</a>します。</p></td>
<td><p>これらのメソッドを呼び出します。</p>
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff550090" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceGetDeviceDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550090)"><strong>WdfUsbTargetDeviceGetDeviceDescriptor</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff550060" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceGetDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550060)"><strong>WdfUsbInterfaceGetDescriptor</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff550063" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceGetEndpointInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550063)"><strong>WdfUsbInterfaceGetEndpointInformation</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff551142" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeGetInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551142)"> <strong>WdfUsbTargetPipeGetInformation</strong></a>します。 このメソッドは、エンドポイントの記述子フィールドを返します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff553037" data-raw-source="[&lt;strong&gt;WDF_USB_PIPE_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553037)"> <strong>WDF_USB_PIPE_INFORMATION</strong> </a>構造体。</li>
</ul></td>
<td><p>これらのメソッドを呼び出します。</p>
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff560374" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::RetrieveDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560374)"><strong>IWDFUsbTargetDevice::RetrieveDescriptor</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff560320" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::GetInterfaceDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560320)"><strong>IWDFUsbInterface::GetInterfaceDescriptor</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff560403" data-raw-source="[&lt;strong&gt;IWDFUsbTargetPipe::GetInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560403)"><strong>IWDFUsbTargetPipe::GetInformation</strong></a>します。 このメソッドは、エンドポイントの記述子フィールドを返します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540285" data-raw-source="[&lt;strong&gt;WINUSB_PIPE_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540285)"> <strong>WINUSB_PIPE_INFORMATION</strong> </a>構造体。</li>
</ul></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540357" data-raw-source="[&lt;strong&gt;_URB_CONTROL_DESCRIPTOR_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540357)"><strong>_URB_CONTROL_DESCRIPTOR_REQUEST</strong></a></p>
<p>(<a href="https://msdn.microsoft.com/library/windows/hardware/ff538943" data-raw-source="[&lt;strong&gt;UsbBuildGetDescriptorRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538943)"><strong>UsbBuildGetDescriptorRequest</strong></a>)</p>
<p>URB_FUNCTION_GET_DESCRIPTOR_FROM_DEVICE</p>
<p>URB_FUNCTION_GET_DESCRIPTOR_FROM_ENDPOINT</p>
<p>URB_FUNCTION_GET_DESCRIPTOR_FROM_INTERFACE</p></td>
</tr>
<tr class="even">
<td>GET_INTERFACE:インターフェイスの現在の代替設定を取得します。 USB 仕様の 9.4.4」セクションを参照してください。</td>
<td><p></p>
<ol>
<li>呼び出してターゲット インターフェイス オブジェクトへの WDFUSBINTERFACE ハンドルを取得、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff550092" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceGetInterface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550092)"> <strong>WdfUsbTargetDeviceGetInterface</strong> </a>メソッド。</li>
<li>呼び出す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff550059" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceGetConfiguredSettingIndex&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550059)"> <strong>WdfUsbInterfaceGetConfiguredSettingIndex</strong> </a>メソッド。</li>
</ol></td>
<td><ol>
<li>取得、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff560312" data-raw-source="[&lt;strong&gt;IWDFUsbInterface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560312)"> <strong>IWDFUsbInterface</strong> </a>ターゲット インターフェイス オブジェクトへのポインター。</li>
<li>呼び出す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff560317" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::GetConfiguredSettingIndex&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560317)"> <strong>IWDFUsbInterface::GetConfiguredSettingIndex</strong> </a>メソッド。</li>
</ol></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540373" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_INTERFACE_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540373)"><strong>_URB_CONTROL_GET_INTERFACE_REQUEST</strong></a></p>
<p>URB_FUNCTION_GET_INTERFACE</p></td>
</tr>
<tr class="odd">
<td>GET_STATUS:デバイス、エンドポイント、またはインターフェイスからのステータス ビットを取得します。 9.4. 5. セクションを参照してください。 USB 仕様。</td>
<td><ol>
<li>セットアップのパケットを宣言します。 参照してください、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff552568" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552568)"> <strong>WDF_USB_CONTROL_SETUP_PACKET</strong> </a>構造体。</li>
<li>セットアップのパケットを呼び出すことによって初期化<a href="https://msdn.microsoft.com/library/windows/hardware/ff552582" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_GET_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552582)"> <strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_GET_STATUS</strong></a>します。</li>
<li>受信者の値で定義されている指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff552554" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552554)"> <strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a>します。</li>
<li>取得するステータスを指定します。 デバイス、インターフェイス、またはエンドポイント (<strong>wIndex</strong>)。</li>
<li>呼び出すことによって、要求を送信<a href="https://msdn.microsoft.com/library/windows/hardware/ff550104" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550104)"> <strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff550082" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550082)"> <strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a>.</li>
</ol></td>
<td><ol>
<li>セットアップのパケットを宣言します。 参照してください、 <strong>WINUSB_CONTROL_SETUP_PACKET</strong> usb_hw.h で構造体を宣言します。</li>
<li>セットアップのパケットをヘルパー マクロを呼び出すことによって初期化<strong>WINUSB_CONTROL_SETUP_PACKET_INIT_GET_STATUS</strong>usb_hw.h で定義されている。</li>
<li>定義されている受信者の値を指定<strong>WINUSB_BMREQUEST_RECIPIENT</strong>します。</li>
<li>取得するステータスを指定します。 デバイス、インターフェイス、またはエンドポイント (<strong>wIndex</strong>)。</li>
<li>呼び出して framework 要求オブジェクトと転送バッファーとセットアップの初期化されたパケットを関連付けることによって、要求をビルド<a href="https://msdn.microsoft.com/library/windows/hardware/ff560363" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560363)"> <strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong> </a>メソッド.</li>
<li>呼び出すことによって、要求を送信、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559149" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559149)"> <strong>IWDFIoRequest::Send</strong> </a>メソッド。</li>
<li>転送バッファーの状態値が表示されます。 そのバッファーを呼び出すことによってアクセス<a href="https://msdn.microsoft.com/library/windows/hardware/ff559249" data-raw-source="[&lt;strong&gt;IWDFMemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559249)"> <strong>IWDFMemory</strong> </a>メソッド。</li>
<li>状態が自己供給型のリモート ウェイク アップを示すかどうかを判断するには、値を使用して 3 つで定義されている、 <strong>WINUSB_DEVICE_TRAITS</strong>列挙体。</li>
</ol></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540378" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_STATUS_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540378)"><strong>_URB_CONTROL_GET_STATUS_REQUEST</strong></a></p>
<p>(<a href="https://msdn.microsoft.com/library/windows/hardware/ff538946" data-raw-source="[&lt;strong&gt;UsbBuildGetStatusRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538946)"><strong>UsbBuildGetStatusRequest</strong></a>)</p>
<p>URB_FUNCTION_GET_STATUS_FROM_DEVICE</p>
<p>URB_FUNCTION_GET_STATUS_FROM_INTERFACE</p>
<p>URB_FUNCTION_GET_STATUS_FROM_ENDPOINT</p>
<p>URB_FUNCTION_GET_STATUS_FROM_OTHER します。</p></td>
</tr>
<tr class="even">
<td>SET_ADDRESS:USB 仕様の 9.4.6」セクションを参照してください。</td>
<td>この要求は、USB ドライバー スタックによって処理されます。クライアント ドライバーでは、この操作を実行できません。</td>
<td>この要求は、USB ドライバー スタックによって処理されます。クライアント ドライバーでは、この操作を実行できません。</td>
<td>この要求は、USB ドライバー スタックによって処理されます。クライアント ドライバーでは、この操作を実行できません。</td>
</tr>
<tr class="odd">
<td>SET_CONFIGURATION:構成を設定します。 USB 仕様の 9.4.7」セクションを参照してください。
<p>詳細については、次を参照してください。 <a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">USB デバイスの構成を選択する方法</a>します。</p></td>
<td>既定では、KMDF は、各インターフェイスの既定の構成と代替の最初の設定を選択します。 クライアント ドライバーは呼び出すことで、既定の構成を変更することができます<a href="https://msdn.microsoft.com/library/windows/hardware/ff550102" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSelectConfigType&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550102)"> <strong>WdfUsbTargetDeviceSelectConfigType</strong> </a>メソッドを指定する<strong>WdfUsbTargetDeviceSelectConfigTypeUrb</strong>要求オプションとして。 この要求に対して、URB の書式を設定し、USB ドライバー スタックに送信する必要があります。</td>
<td>既定では、UMDF は、各インターフェイスの既定の構成と代替の最初の設定を選択します。 クライアント ドライバーでは、構成を変更できません。</td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540422" data-raw-source="[&lt;strong&gt;_URB_SELECT_CONFIGURATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540422)"><strong>_URB_SELECT_CONFIGURATION</strong></a></p>
<p>(<a href="https://msdn.microsoft.com/library/windows/hardware/hh406243" data-raw-source="[&lt;strong&gt;USBD_SelectConfigUrbAllocateAndBuild&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406243)"><strong>USBD_SelectConfigUrbAllocateAndBuild</strong></a>)</p>
<p>URB_FUNCTION_SELECT_CONFIGURATION</p></td>
</tr>
<tr class="even">
<td>SET_DESCRIPTOR:既存のデバイス、構成、または文字列記述子を更新します。 USB 仕様の 9.4.8」セクションを参照してください。
<p>この要求は、通常使用されません。 ただし、USB ドライバー スタックは、クライアント ドライバーからのような要求を受け入れます。</p></td>
<td><ol>
<li>ビルドの割り当てと、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff538923" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538923)"> <strong>URB</strong> </a>要求。</li>
<li>転送情報を指定する<a href="https://msdn.microsoft.com/library/windows/hardware/ff540357" data-raw-source="[&lt;strong&gt;_URB_CONTROL_DESCRIPTOR_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540357)"> <strong>_URB_CONTROL_DESCRIPTOR_REQUEST</strong> </a>構造体。</li>
<li>呼び出すことによって、要求を送信<a href="https://msdn.microsoft.com/library/windows/hardware/ff550088" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForUrb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550088)"> <strong>WdfUsbTargetDeviceFormatRequestForUrb</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff550105" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendUrbSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550105)"> <strong>WdfUsbTargetDeviceSendUrbSynchronously</strong> </a>します。</li>
</ol></td>
<td><ol>
<li>セットアップのパケットを宣言します。 参照してください、 <strong>WINUSB_CONTROL_SETUP_PACKET</strong> usb_hw.h で構造体を宣言します。</li>
<li>USB 仕様に従って転送情報を指定します。</li>
<li>呼び出して framework 要求オブジェクトと転送バッファーとセットアップの初期化されたパケットを関連付けることによって、要求をビルド<a href="https://msdn.microsoft.com/library/windows/hardware/ff560363" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560363)"> <strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong> </a>メソッド.</li>
<li>呼び出すことによって、要求を送信、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559149" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559149)"> <strong>IWDFIoRequest::Send</strong> </a>メソッド。</li>
</ol></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540357" data-raw-source="[&lt;strong&gt;_URB_CONTROL_DESCRIPTOR_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540357)"><strong>_URB_CONTROL_DESCRIPTOR_REQUEST</strong></a></p>
<p>URB_FUNCTION_SET_DESCRIPTOR_TO_DEVICE</p>
<p>URB_FUNCTION_SET_DESCRIPTOR_TO_ENDPOINT</p>
<p>URB_FUNCTION_SET_DESCRIPTOR_TO_INTERFACE</p></td>
</tr>
<tr class="odd">
<td>SET_FEATURE:デバイス、その構成、インターフェイス、およびエンドポイントで特定の機能設定を有効にします。 USB 仕様の 9.4.9」セクションを参照してください。</td>
<td><ol>
<li>セットアップのパケットを宣言します。 参照してください、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff552568" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552568)"> <strong>WDF_USB_CONTROL_SETUP_PACKET</strong> </a>構造体。</li>
<li>セットアップのパケットを呼び出すことによって初期化<a href="https://msdn.microsoft.com/library/windows/hardware/ff552576" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552576)"> <strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong></a>します。</li>
<li>定義されている受信者の値 (デバイス、インターフェイス、エンドポイント) を指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff552554" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552554)"> <strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a>します。</li>
<li>機能のセレクターを指定 (<strong>wValue</strong>)。 Usbspec.h USB_FEATURE_XXX 定数を参照してください。 USB 仕様では、表 9-6 を参照してください。</li>
<li>設定<em>SetFeature</em>に<strong>は TRUE。</strong></li>
<li>呼び出すことによって、要求を送信<a href="https://msdn.microsoft.com/library/windows/hardware/ff550104" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550104)"> <strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff550082" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550082)"> <strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a>.</li>
</ol></td>
<td><ol>
<li>セットアップのパケットを宣言します。 参照してください、 <strong>WINUSB_CONTROL_SETUP_PACKET</strong> usb_hw.h で構造体を宣言します。</li>
<li>セットアップのパケットをヘルパー マクロを呼び出すことによって初期化<strong>WINUSB_CONTROL_SETUP_PACKET_INIT_FEATURE</strong>usb_hw.h で定義されている。</li>
<li>定義されている受信者の値を指定<strong>WINUSB_BMREQUEST_RECIPIENT</strong>します。</li>
<li>機能のセレクターを指定 (<strong>wValue</strong>)。 参照してください<strong>USB_FEATURE_XXX</strong> Usbspec.h で使用される定数。 USB 仕様では、表 9-6 を参照してください。</li>
<li>設定<em>SetFeature</em>に<strong>TRUE</strong>します。</li>
<li>呼び出して framework 要求オブジェクトと転送バッファーとセットアップの初期化されたパケットを関連付けることによって、要求をビルド<a href="https://msdn.microsoft.com/library/windows/hardware/ff560363" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560363)"> <strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong> </a>メソッド.</li>
<li>呼び出すことによって、要求を送信、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559149" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559149)"> <strong>IWDFIoRequest::Send</strong> </a>メソッド。</li>
</ol></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540361" data-raw-source="[&lt;strong&gt;_URB_CONTROL_FEATURE_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540361)"><strong>_URB_CONTROL_FEATURE_REQUEST</strong></a></p>
<p>(<a href="https://msdn.microsoft.com/library/windows/hardware/ff538932" data-raw-source="[&lt;strong&gt;UsbBuildFeatureRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538932)"><strong>UsbBuildFeatureRequest</strong></a>)</p>
<p>URB_FUNCTION_SET_FEATURE_TO_DEVICE</p>
<p>URB_FUNCTION_SET_FEATURE_TO_INTERFACE</p>
<p>URB_FUNCTION_SET_FEATURE_TO_ENDPOINT</p>
<p>URB_FUNCTION_SET_FEATURE_TO_OTHER</p></td>
</tr>
<tr class="even">
<td>SET_INTERFACE:インターフェイス内で別の設定を変更します。 USB 仕様の 9.4.9」セクションを参照してください。
<p>詳細については、次を参照してください。 <a href="select-a-usb-alternate-setting.md" data-raw-source="[How to select an alternate setting in a USB interface](select-a-usb-alternate-setting.md)">USB インターフェイスで代替の設定を選択する方法</a>します。</p></td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff550101" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSelectConfig&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550101)"><strong>WdfUsbTargetDeviceSelectConfig</strong></a>
<p></p>
<ol>
<li>ターゲットのインターフェイス オブジェクトに WDFUSBINTERFACE ハンドルを取得します。</li>
<li>呼び出す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff550073" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceSelectSetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550073)"> <strong>WdfUsbInterfaceSelectSetting</strong> </a>メソッド。</li>
</ol></td>
<td><ol>
<li>取得、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff560312" data-raw-source="[&lt;strong&gt;IWDFUsbInterface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560312)"> <strong>IWDFUsbInterface</strong> </a>ターゲット インターフェイス オブジェクトへのポインター。</li>
<li>呼び出す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff560343" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::SelectSetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560343)"> <strong>IWDFUsbInterface::SelectSetting</strong> </a>メソッド。</li>
</ol></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540425" data-raw-source="[&lt;strong&gt;_URB_SELECT_INTERFACE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540425)"><strong>_URB_SELECT_INTERFACE</strong></a></p>
<p>(<a href="https://msdn.microsoft.com/library/windows/hardware/hh406245" data-raw-source="[&lt;strong&gt;USBD_SelectInterfaceUrbAllocateAndBuild&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406245)"><strong>USBD_SelectInterfaceUrbAllocateAndBuild</strong></a>)</p>
<p>URB_FUNCTION_SELECT_INTERFACE</p></td>
</tr>
<tr class="odd">
<td>SYNC_FRAME:Get およびエンドポイントの同期の設定とはフレーム番号です。 USB 仕様の 9.4.10」セクションを参照してください。</td>
<td>この要求は、USB ドライバー スタックによって処理されます。クライアント ドライバーでは、この操作を実行できません。</td>
<td>この要求は、USB ドライバー スタックによって処理されます。クライアント ドライバーでは、この操作を実行できません。</td>
<td>この要求は、USB ドライバー スタックによって処理されます。クライアント ドライバーでは、この操作を実行できません。</td>
</tr>
<tr class="even">
<td>クラスに固有とデバイスの要求と仕入先コマンド。</td>
<td><ol>
<li>セットアップのパケットを宣言します。 参照してください、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff552568" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552568)"> <strong>WDF_USB_CONTROL_SETUP_PACKET</strong> </a>構造体。</li>
<li>セットアップのパケットを呼び出すことによって初期化<a href="https://msdn.microsoft.com/library/windows/hardware/ff552574" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_CLASS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552574)"> <strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_CLASS</strong></a>-特定の要求または<a href="https://msdn.microsoft.com/library/windows/hardware/ff552588" data-raw-source="[&lt;strong&gt;WDF_USB_CONTROL_SETUP_PACKET_INIT_VENDOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552588)"> <strong>WDF_USB_CONTROL_SETUP_PACKET_INIT_VENDOR</strong></a>ベンダー コマンド。</li>
<li>定義されている受信者の値 (デバイス、インターフェイス、エンドポイント) を指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff552554" data-raw-source="[&lt;strong&gt;WDF_USB_BMREQUEST_RECIPIENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552554)"> <strong>WDF_USB_BMREQUEST_RECIPIENT</strong></a>します。</li>
<li>呼び出すことによって、要求を送信<a href="https://msdn.microsoft.com/library/windows/hardware/ff550104" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550104)"> <strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff550082" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550082)"> <strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a>.</li>
</ol></td>
<td><ol>
<li>セットアップのパケットを宣言します。 参照してください、 <strong>WINUSB_CONTROL_SETUP_PACKET</strong> usb_hw.h で構造体を宣言します。</li>
<li>セットアップのパケットをヘルパー マクロを呼び出すことによって初期化<strong>WINUSB_CONTROL_SETUP_PACKET_INIT_CLASS</strong>または<strong>WINUSB_CONTROL_SETUP_PACKET_INIT_VENDOR</strong>usb_hw.h で定義されている。</li>
<li>方向を指定 (を参照してください、 <strong>WINUSB_BMREQUEST_DIRECTION</strong>列挙型)、受信者 (を参照してください、 <strong>WINUSB_BMREQUEST_RECIPIENT</strong>列挙型)、クラスの説明に従って、要求、またはハードウェアの仕様。</li>
<li>呼び出して framework 要求オブジェクトと転送バッファーとセットアップの初期化されたパケットを関連付けることによって、要求をビルド<a href="https://msdn.microsoft.com/library/windows/hardware/ff560363" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560363)"> <strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong> </a>メソッド.</li>
<li>呼び出すことによって、要求を送信、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559149" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559149)"> <strong>IWDFIoRequest::Send</strong> </a>メソッド。</li>
<li>転送バッファー内のデバイスから情報を受信します。 そのバッファーを呼び出すことによってアクセス<a href="https://msdn.microsoft.com/library/windows/hardware/ff559249" data-raw-source="[&lt;strong&gt;IWDFMemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559249)"> <strong>IWDFMemory</strong> </a>メソッド。</li>
</ol></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540393" data-raw-source="[&lt;strong&gt;_URB_CONTROL_VENDOR_OR_CLASS_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540393)"><strong>_URB_CONTROL_VENDOR_OR_CLASS_REQUEST</strong></a></p>
<p>(<a href="https://msdn.microsoft.com/library/windows/hardware/ff538986" data-raw-source="[&lt;strong&gt;UsbBuildVendorRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538986)"><strong>UsbBuildVendorRequest</strong></a>)</p>
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



## <a name="how-to-send-a-control-transfer-for-vendor-commands---kmdf"></a>仕入先コマンド - KMDF の制御の移動を送信する方法


この手順では、クライアント ドライバーがコントロールの転送を送信する方法を示します。 この例では、クライアント ドライバーは、デバイスから、ファームウェアのバージョンを取得するベンダー コマンドを送信します。

1.  仕入先のコマンドは、するための定数を宣言します。 ハードウェア仕様を調査し、仕入先のコマンドを使用するを確認します。
2.  宣言を[ **WDF\_メモリ\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff552392)構造体を呼び出すことによって初期化、 [ **WDF\_メモリ\_記述子\_INIT\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff552392_init_buffer)マクロ。 この構造体が、USB ドライバーは、要求を完了した後は、デバイスから応答を受信します。
3.  かどうか、要求を送信する、同期または非同期、に応じて送信オプションを指定します。
    -   呼び出すことによって、要求を同期的に送信する場合[ **WdfUsbTargetDeviceSendControlTransferSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff550104)タイムアウト値を指定します。 その値は、なし、タイムアウトすることができます、スレッドは無期限にブロックするために重要です。

        これは、宣言、 [ **WDF\_要求\_送信\_オプション**](https://msdn.microsoft.com/library/windows/hardware/ff552491)構造体を呼び出すことによって初期化、 [ **WDF\_要求\_送信\_オプション\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff552491_init)マクロ。 オプションとして指定**WDF\_要求\_送信\_オプション\_タイムアウト**します。

        次に、呼び出すことによって、タイムアウト値を設定、 [ **WDF\_要求\_送信\_オプション\_設定\_タイムアウト**](https://msdn.microsoft.com/library/windows/hardware/ff552498)マクロ。

    -   要求を非同期的に送信する場合は、完了ルーチンを実装します。 完了ルーチンで割り当てられているすべてのリソースを解放します。

4.  宣言を[ **WDF\_USB\_コントロール\_セットアップ\_パケット**](https://msdn.microsoft.com/library/windows/hardware/ff552568)セットアップ トークンを含めるし、構造体の書式を設定する構造体。 これを行うには、呼び出し、 [ **WDF\_USB\_コントロール\_セットアップ\_パケット\_INIT\_ベンダー** ](https://msdn.microsoft.com/library/windows/hardware/ff552568_init_vendor)マクロは、セットアップを書式設定するにはパケットです。 呼び出しの方向を指定、要求、受信者、(手順 3 で初期化する)、送信された要求オプションおよび仕入先のコマンドを表す定数。
5.  呼び出すことによって、要求を送信[ **WdfUsbTargetDeviceSendControlTransferSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff550104)または[ **WdfUsbTargetDeviceFormatRequestForControlTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff550082).
6.  フレームワークによって返される NTSTATUS 値を確認し、受信した値を検査します。

このコード例では、USB デバイスのファームウェア バージョンを取得するコントロールの転送要求を送信します。 要求が同期的に送信され、クライアント ドライバーが 5 秒 (100 ナノ秒単位) での相対的なタイムアウト値を指定します。 ドライバーは、ドライバーの定義済みのデバイス コンテキストで受信した応答を格納します。

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

## <a name="how-to-send-a-control-transfer-for-getstatus---umdf"></a>GET の制御の移動を送信する方法\_状態 - UMDF


この手順は、クライアント ドライバーが、GET の制御の移動を送信する方法を示しています。\_STATUS コマンド。 要求の受信者は、デバイスと、要求は、D1 D0 のビット単位の情報を取得します。 詳細については、USB 仕様の図 9-4 を参照してください。

1.  Usb のヘッダー ファイル インクルード\_hw.h OSR USB Fx2 Learning kit UMDF ドライバーのサンプルで使用できます。
2.  宣言を**WINUSB\_コントロール\_セットアップ\_パケット**構造体。
3.  セットアップのパケットをヘルパー マクロを呼び出すことによって初期化**WINUSB\_コントロール\_セットアップ\_パケット\_INIT\_取得\_状態**します。
4.  指定**BmRequestToDevice**受信者として。
5.  0 を指定、*インデックス*値。
6.  SendControlTransferSynchronously 同期的に要求を送信するヘルパー メソッドを呼び出します。

    ヘルパー メソッドを呼び出して framework 要求オブジェクトと転送バッファーとセットアップの初期化されたパケットを関連付けることによって、要求を作成する[ **IWDFUsbTargetDevice::FormatRequestForControlTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff560363)メソッド。 ヘルパー メソッドが呼び出すことによって、要求を送信、 [ **IWDFIoRequest::Send** ](https://msdn.microsoft.com/library/windows/hardware/ff559149)メソッド。 メソッドが返された後に返される値を検査します。

7.  状態が自己供給型のリモート ウェイク アップを示すかどうかを判断で定義されているこれらの値を使用して、 **WINUSB\_デバイス\_TRAITS**列挙体。

このコード例では、get、デバイスの状態に制御の転送要求を送信します。 この例は、SendControlTransferSynchronously をという名前のヘルパー メソッドを呼び出すことによって同期的に、要求を送信します。

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

次のコード例では、SendControlTransferSynchronously をという名前のヘルパー メソッドの実装を示します。 このメソッドは、同期的に要求を送信します。

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


デバイスの機能のドライバーとして Winusb.sys を使用する場合は、アプリケーションからコントロールの転送を送信できます。 WinUSB でセットアップ パケットの書式を設定するには、UMDF ヘルパー マクロと、このトピックの表で説明されている構造体を使用します。 要求を送信する呼び出し[ **WinUsb\_ControlTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff540219)関数。








