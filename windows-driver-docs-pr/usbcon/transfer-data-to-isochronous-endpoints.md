---
Description: This topic describes how a client driver can build a USB Request Block (URB) to transfer data to and from isochronous endpoints in a USB device.
title: USB 等時性エンドポイントへのデータの転送方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d7895644493e58c4d72ce0a7054007d12655b26
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579867"
---
# <a name="how-to-transfer-data-to-usb-isochronous-endpoints"></a>USB 等時性エンドポイントへのデータの転送方法


このトピックでは、クライアント ドライバーが、USB 要求ブロック (URB) USB デバイス アイソクロナス エンドポイントとの間のデータ転送を作成する方法について説明します。

ユニバーサル シリアル バス (USB) デバイスでは、オーディオ/ビデオ ストリーミングなど、一定の速度で時間に依存するデータを転送するアイソクロナス エンドポイントをサポートできます。 データを転送するには、クライアント ドライバーは、アイソクロナス エンドポイントにデータを読み書きの要求を発行します。 その結果、ホスト コント ローラーは、一定の間隔でデバイスをポーリングすることによってデータを送受信するアイソクロナスの転送を開始します。

高速とフル_スピードのデバイスでは、(入力/出力) パケットのトークンを使用して、ポーリングが行われます。 エンドポイントのデータを送信する準備ができたら、デバイスは、データを送信して IN トークン パケットの 1 つに応答します。 デバイスへの書き込みには、ホスト コント ローラーは、データ パケットを続けて、外トークン パケットを送信します。 ホスト コント ローラーまたはデバイスのハンドシェイク パケットを送信しませんし、そのため、配信の保証はありません。 ホスト コント ローラーが、転送を再試行しませんのでは、エラーが発生した場合のデータが失われます。

Isochronous 転送には、ホスト コント ローラーは、バス上の特定の期間を予約します。 アイソクロナス エンドポイントの予約済みの時間を管理するため、時間が分割連続する論理スニーカーと呼びます*間隔のバス*します。 バスの間隔の単位は、バス速度に依存します。

フル スピードは、バスの間隔は、*フレーム*します。 フレームの長さは、1 ミリ秒です。

高速および SuperSpeed は、バス間隔は、microframe です。 Microframe の長さは、125 (マイクロ秒) です。 8 つの連続する microframes を構成するいずれかの高速または SuperSpeed フレーム。

Isochronous 転送は、基に、パケットです。 用語*アイソクロナス パケット*このトピックでは 1 つのバスの間隔で転送されるデータの量を指します。 エンドポイントの特性は、各パケットのサイズが固定されており、エンドポイントの特性によって決まりますを決定します。

クライアント ドライバーでは、要求に対して、URB を作成し、USB ドライバー スタックに URB を送信してアイソクロナスの転送を開始します。 USB ドライバー スタックの下位のドライバーのいずれかによって、要求が処理されます。 URB を受信すると、USB ドライバー スタックは、要求の一連の検証とスケジュールのトランザクションを実行します。 フル スピードは、各 bus 間隔で転送されるアイソクロナスのパケットは、ネットワーク上で単一のトランザクションで含まれています。 特定の高速デバイスは、バスの間隔で複数のトランザクションを許可します。 その場合は、クライアント ドライバーは送信または 1 つの要求 (URB) isochronous パケットでより多くのデータを受信できます。 SuperSpeed デバイスは、複数のトランザクションをサポートし、バースト転送では、バスの間隔ごとのさらに多くのバイト数を許可します。 バースト転送の詳細については、USB 3.0 仕様ページ 9 42 を参照してください。

### <a name="prerequisites"></a>前提条件

アイソクロナスの転送要求を作成する前に、アイソクロナス エンドポイントが開かれたパイプに関する情報が必要です。

Windows Driver Model (WDM) ルーチンを使用するクライアント ドライバーでは、いずれかでパイプ情報が含まれている、 [ **USBD\_パイプ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff539114)の構造を[ **USBD\_インターフェイス\_一覧\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff539076)配列。 クライアント ドライバーでは、ドライバーの構成を選択する前回の要求では、その配列またはデバイスのインターフェイスを取得します。

Windows Driver Framework (WDF) のクライアント ドライバーは、フレームワークの対象になるパイプ オブジェクトと呼び出しへの参照を取得する必要があります[ **WdfUsbTargetPipeGetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff551142)パイプ情報を取得する、 [**WDF\_USB\_パイプ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff553037)構造体。

パイプの情報に基づき、この一連の情報を決定します。

-   ホスト コント ローラーは、パイプの各パケットに、データの量を送信できます。

    クライアント ドライバーは、要求で送信できるデータの量は、ホスト コント ローラーが送信またはエンドポイントから受信するバイトの最大数を超えることはできません。 最大バイト数がで示される、 **MaximumPacketSize**のメンバー [ **USBD\_パイプ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff539114)と[**WDF\_USB\_パイプ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff553037)構造体。 USB ドライバー スタックのセット、 **MaximumPacketSize**値、構成を選択または選択インターフェイス要求中にします。

    フル スピード デバイス、 **MaximumPacketSize**の最初の 11 ビットから派生したが、 **wMaxPacketSize**のエンドポイントができるバイトの最大数を示すエンドポイント記述子フィールド送信またはトランザクションで受信します。 フル スピード デバイスのコント ローラーは、バス間隔ごとの 1 つのトランザクションを送信します。

    Isochronous 転送を高速ホスト コント ローラーが、エンドポイントを使用して場合に、バスの間隔で追加のトランザクションを送信できます。 その他のトランザクションの数が、デバイスごとに設定し、のビット 12..11 に示されている、 **wMaxPacketSize**します。 その数 0、1、または 2 を使用できます。 12..11 0 場合、microframe あたり追加のトランザクションは、エンドポイントではサポートされていません。 数が 1 の場合は、ホスト コント ローラーが別のトランザクション (microframe あたり 2 つのトランザクションの合計); できます送信2 では、2 つの追加トランザクション (microframe あたり 3 つのトランザクションの合計) を示します。 **MaximumPacketSize** USB ドライバー スタックで設定されている値には、追加のトランザクションで送信できるバイト数が含まれています。

    USB の特定の値、SuperSpeed isochronous 転送の\_SUPERSPEED\_エンドポイント\_コンパニオン\_記述子が重要です (Usbspec.h を参照してください)。 USB ドライバー スタックでは、これらの値を使って、バス間隔の最大バイト数を計算します。

    -   **Isochronous.Mult**エンドポイント コンパニオンの記述子フィールド。 SuperSpeed isochronous 転送では、(より高速デバイス) などの追加のトランザクションをバースト トランザクションと呼びます。 **Mult**値は、エンドポイントがサポートされるバースト トランザクションの最大数を示します。 サービス期間内 (0 ~ 2 のインデックス付き)、3 つまでのバースト トランザクションがあります。
    -   **bMaxBurst**エンドポイント コンパニオンの記述子フィールド。 この値は、チャンクの数を示します。 **wMaxPacketSize**バーストの 1 つのトランザクション内に存在することができます。 バーストのトランザクションで最大 16 のチャンクが (0 ~ 15 のインデックス付き) があります。
    -   **wBytesPerInterval**ホストが送信できるまたはバス間隔で受信するバイトの合計数を示します。 場合でも、バス間隔あたりのバイト数の最大数として計算できます (**bMaxBurst**+1) \* (**Mult**+1) \* **wMaxPacketSize**、USB 3.0 の仕様では、使用することをお勧め、 **wBytesPerInterval**値の代わりにします。 **WBytesPerInterval**値はその計算値未満である必要があります。

    **重要な**上記で説明されている値は、クライアント ドライバーは情報提供用です。 ドライバーは常に使用する必要があります、 **MaximumPacketSize**転送バッファーのレイアウトを判別エンドポイント記述子の値。



-   どのくらいの頻度は、エンドポイント データ送信または受信します。

    **間隔**メンバーは、エンドポイントが送信またはデータの受信頻度を決定するために使用します。 値と、クライアント ドライバー変更することはできませんが、デバイスに設定します。 USB ドライバー スタックは別の番号を使用してデータ ストリームにアイソクロナス パケットを挿入する頻度を決定します。 から派生するポーリング期間、**間隔**値。

    フル スピードの送信、**間隔**とポーリングの期間の値は常に 1; USB ドライバー スタックは、その他の値を無視します。

    次の表は**間隔**と高速および SuperSpeed 転送の計算のポーリング期間。

    | 間隔 | ポーリング間隔 (2Interval 1)                      |
    |----------|---------------------------------------------------|
    | 1        | 1 になります。データが転送されるすべてのバス間隔。        |
    | 2        | 2 です。データが転送される 2 つ目のバス間隔。 |
    | 3        | 4 です。データが転送される 4 つ目のバス間隔。 |
    | 4        | 8 です。データが転送される 8 番目のバス間隔。 |



-   各バス速度のパケットの数に制限は。

    URB、のみを送信できます最大 255 アイソクロナス パケット フル スピード デバイスです。高速および SuperSpeed デバイスでの URB で 1024 パケット。 URB で送信するパケットの数は、各フレームでパケットの数の倍数である必要があります。

    | ポーリング間隔 | 高速/SuperSpeed のパケットの数 |
    |----------------|---------------------------------------------|
    | 1              | 8 の倍数                               |
    | 2              | 4 の倍数                               |
    | 3              | 2 の倍数                               |
    | 4              | 任意                                         |



例の完全な速度エンドポイントを検討してください**wMaxPacketSize** 1,023 です。 この例では、アプリケーションは、25,575 バイトのバッファーを提供します。 そのバッファーの転送には、25 アイソクロナス パケット (25575/1023) が必要です。

次の特性を持つ高速のエンドポイントをエンドポイント記述子に示されている例を検討してください。

-   **wMaxPacketSize** 1,024 です。
-   12..11 のビットは、2 つの追加トランザクションを示します。
-   **間隔**は 1 です。

クライアント ドライバーを選択した後構成では、 **MaximumPacketSize**アイソクロナス パイプ示します 3,072 バイトの (トランザクション数合計\* **wMaxPacketSize**)。 その他のトランザクションを使用すると、クライアント ドライバーですべての microframe 3,072 バイトおよび 1 つのフレームで 24,576 バイト数の合計を転送します。 次の図は、高速な転送の 1 つ microframe でアイソクロナスのパケットを転送する頻度を示します。

![アイソクロナス転送](images/iso-packets.png)

エンドポイントと SuperSpeed エンドポイント コンパニオンの記述子に示されているこれらの特性を持つ、たとえば、SuperSpeed エンドポイントを考慮してください。

-   **wMaxPacketSize** 1,024 です。
-   **bMaxBurst** 15 です。
-   **間隔**は 1 です。
-   **Isochronous.Mult**は 2 です。
-   **wBytesPerInterval** 45000 です。

前の例では、最大バイト数として計算できますもで**wMaxPacketSize** \* (**bMaxBurst** +1) \* (**Mult** + 1)49,152 バイトでその結果、デバイスの制限値を**wBytesPerInterval** 45,000 バイト値。 値がも反映**MaximumPacketSize** 45,000 します。 クライアント ドライバーを使用する必要がありますのみ、 **MaximumPacketSize**値。 この例では、バーストの 3 つのトランザクションに要求を分割できます。 最初の 2 つのバースト トランザクションの 16 のチャンクを含む**wMaxPacketSize**します。 最後のバースト トランザクションには、残りのバイトを保持するために 12 のチャンクが含まれています。 このイメージは、ポーリング間隔と SuperSpeed 伝送アイソクロナスのパケットを転送されたバイト数を示します。

![superspeed アイソクロナス](images/iso-packets-superspeed.png)

次の手順では、アイソクロナスの転送の要求を構築する方法について説明します。

1.  各 isochronous パケットのサイズを取得します。
2.  フレームごとの isochronous パケットの数を決定します。
3.  転送内容をすべてのバッファーを保持するために必要な isochronous パケットの数を計算します。
4.  割り当て、 [ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)転送の詳細を説明する構造体。
5.  各 isochronous パケット、パケットのオフセットなどの詳細を指定します。

完全なコード アイソクロナスを送信する方法の例は、USBSAMP 要求を転送します。

この例では、このトピックでは、アイソクロナス転送の USBSAMP 実装を簡略化します。 サンプルでは、転送に必要なフレームの合計数を計算します。 転送バッファーは、フレームに送信できるデータの量に基づき、小さいチャンク サイズ (バイト) に分けられます。

次の手順では、上記の手順を詳しく説明して、計算とクライアント ドライバーは、ビルドし、高速アイソクロナス エンドポイント アイソクロナス転送要求の送信に使用できるルーチンを示しています。 プロシージャで使用される値は、前に説明した例のエンドポイントの特性に基づいています。

<a name="instructions"></a>手順
------------

### <a href="" id="get-the-size-of-an-isochronous-packet--"></a>手順 1:アイソクロナスのパケットのサイズを取得します。

パイプの検査することによってアイソクロナスのパケット サイズを決定する**MaximumPacketSize**値。

完全な高速転送、アイソクロナスのパケットのサイズは 1 つのフレームで転送できるバイト数です。 高速および SuperSpeed 転送、アイソクロナスのパケットのサイズが 1 つ microframe で転送できるバイトの合計数。 これらの値は、パイプに示される**MaximumPacketSize**します。

例では、 **MaximumPacketSize**は 1023 バイト (フル_スピード) フレームあたり; microframe (高速) あたりのバイト数を 3072; microframe (SuperSpeed) あたり 45,000 のバイト数。

**注**、 **MaximumPacketSize**値がアイソクロナス パケットの最大許容サイズを示します。 クライアント ドライバーは、任意の値を各 isochronous パケットのサイズを設定できますより小さい**MaximumPacketSize**値。



### <a href="" id="determine-the-number-of-isochronous-packets-per-frame-"></a>手順 2:フレームごとの isochronous パケットの数を決定します。

フル スピードの伝送の各フレームで 1 つの isochronous パケットを転送します。

高速および SuperSpeed 転送では、この値は、間隔の値から派生する必要があります。 この例では間隔は 1 です。 そのため、isochronous パケットの数がフレームあたり 8 個である必要があります。 その他の間隔の値は、前提条件のセクションの表を参照してください。

### <a href="" id="calculate-the-number-of-isochronous-packets-that-are-required-to-hold-the-entire-transfer-buffer-"></a>手順 3:転送内容をすべてのバッファーを保持するために必要な isochronous パケットの数を計算します。

バッファー全体を転送するために必要な isochronous パケットの数を計算します。 転送バッファーの長さをアイソクロナスのパケットのサイズで割ることによって、この値を計算できます。

この例で仮定アイソクロナス各パケットのサイズがある**MaximumPacketSize**転送バッファーの長さは、複数の**MaximumPacketSize**値。

たとえば、完全高速転送 25,575 バイトの指定されたバッファー 25 アイソクロナス パケット (25575/1023) が必要です。 高速の転送には、24,576 サイズのバッファーは、転送 8 アイソクロナス パケット (24576/3072) に分けられます。 SuperSpeed、360,000 バイト サイズのバッファーは 8 つアイソクロナス パケット (360000/45000) に適合します。

クライアント ドライバーでは、これらの要件を検証する必要があります。

-   アイソクロナス パケットの数は、フレームごとのパケットの数の倍数である必要があります。
-   アイソクロナス パケットを転送する必要がの最大数は、フル スピード デバイス; 255 を超えていない必要があります。1024 を高速または SuperSpeed デバイス。

### <a href="" id="allocate-an-urb-structure-to-describe-the-details-of-the-transfer-"></a>手順 4:転送の詳細を説明する URB 構造体を割り当てます。

1.  割り当て、 [ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)非ページ プール内の構造体。

    ドライバーを呼び出す必要があります、クライアント ドライバー WDM ルーチンを使用する場合、 [ **USBD\_IsochUrbAllocate** ](https://msdn.microsoft.com/library/windows/hardware/hh406231) for Windows 8、Windows Driver Kit (WDK) がある場合。 クライアント ドライバーでは、Windows Vista および Windows オペレーティング システムの以降のバージョンを対象に、ルーチンを使用できます。 Windows 8 の WDK がないか、クライアント ドライバーを以前のバージョンのオペレーティング システムの場合は、呼び出すことによってスタックまたは非ページ プール内の構造を割り当てることができるかどうか[ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520).

    WDF のクライアント ドライバーを呼び出すことができます、 [ **WdfUsbTargetDeviceCreateIsochUrb** ](https://msdn.microsoft.com/library/windows/hardware/hh439420)メモリを割り当てる対象のメソッド、 [ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)構造体。

2.  **UrbIsochronousTransfer**のメンバー、 [ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)へのポインターを構造体、 [  **\_URB\_アイソクロナス\_転送**](https://msdn.microsoft.com/library/windows/hardware/ff540414)アイソクロナスの転送の詳細を記述する構造体。 次の初期化**UrbIsochronousTransfer**メンバーとして次のとおりです。
    -   設定、 **UrbIsochronousTransfer.Hdr.Length** URB のサイズのメンバー。 URB のサイズを取得するには、呼び出す[**取得\_ISO\_URB\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff537144)マクロ パケットの数を指定します。
    -   設定、 **UrbIsochronousTransfer.Hdr.Function**メンバー`URB_FUNCTION_ISOCH_TRANSFER`します。
    -   設定、 **UrbIsochronousTransfer.NumberOfPackets**アイソクロナス パケットの数のメンバー。
    -   設定、 **UrbIsochronousTransfer.PipeHandle**パイプ エンドポイントに関連付けられている不透明なハンドルにします。 パイプ ハンドルが、ユニバーサル シリアル バス (USB) ドライバー スタックで使用される USBD パイプ ハンドルであることを確認します。

        USBD パイプ ハンドルを取得するには、WDF のクライアント ドライバーを呼び出すことができます、 [ **WdfUsbTargetPipeWdmGetPipeHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff551162)メソッドとフレームワークのパイプ オブジェクトへの WDFUSBPIPE ハンドルを指定します。 WDM クライアント ドライバーで取得したのと同じハンドルを使用する必要があります、 **PipeHandle**のメンバー、 [ **USBD\_パイプ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff539114)構造体。

    -   転送の方向を指定します。 設定**UrbIsochronousTransfer.TransferFlags** USBD に\_転送\_方向\_IN isochronous 転送 (デバイスからの読み取り); でのUSBD\_転送\_方向\_アイソクロナス (デバイスへの書き込み) 転送の。
    -   指定、USBD\_開始\_ISO\_転送\_ASAP フラグ**UrbIsochronousTransfer**します。TransferFlags します。 フラグは、次の適切なフレームで、転送を送信する USB ドライバー スタックを指示します。 クライアント ドライバーは、このパイプ アイソクロナスの URB を送信する最初に、可能なとすぐに、ドライバー スタックは URB でアイソクロナス パケットを送信します。 USB ドライバー スタックは、そのパイプで後続の翻訳を使用する次のフレームを追跡します。 USBD を使用する後続の isochronous URB の送信に遅延がある場合\_開始\_ISO\_転送\_ASAP フラグ、ドライバー スタックが遅延するには、その URB の一部またはすべてのパケットを考慮して、ものは転送されませんパケット。

        USB ドライバー スタックのリセット、USBD\_開始\_ISO\_転送\_ASAP 開始フレーム追跡、スタックがそのパイプの前の URB を完了した後、アイソクロナス URB 1024 フレームを受信しない場合。 USBD を指定する代わりに\_開始\_ISO\_転送\_ASAP フラグは、開始フレームを指定することができます。 詳細については、「解説」を参照してください。

    -   転送バッファーとそのサイズを指定します。 ポインターを設定するには、バッファーに**UrbIsochronousTransfer.TransferBuffer**または[ **MDL** ](https://msdn.microsoft.com/library/windows/hardware/ff554414)でバッファーを記述する**UrbIsochronousTransfer.TransferBufferMDL**します。

        取得する、 [ **MDL** ](https://msdn.microsoft.com/library/windows/hardware/ff554414) WDF のクライアント ドライバーを呼び出すことができます、転送バッファーの[ **WdfRequestRetrieveOutputWdmMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff550021)または[ **WdfRequestRetrieveInputWdmMdl**](https://msdn.microsoft.com/library/windows/hardware/ff550016)転送の方向に応じて、します。

### <a href="" id="specify-the-details-of-each-isochronous-packet-in-the-transfer-"></a>手順 5:転送では、各アイソクロナス パケットの詳細を指定します。

USB ドライバー スタックは、新しい割り当て[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)各アイソクロナスのパケットが、パケットに含まれるデータではなく、情報を保持するのに十分な大きさである構造体。 **URB**構造、 **UrbIsochronousTransfer.IsoPacket**メンバーの配列は、 [ **USBD\_ISO\_パケット\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff539084)各 isochronous パケットを転送の詳細を説明します。 パケットは、連続している必要があります。 配列内の要素の数は、URB で指定された isochronous パケットの数である必要があります**UrbIsochronousTransfer.NumberOfPackets**メンバー。

高速転送では、配列内の各要素は microframe の 1 つで 1 つの isochronous パケットに関連付けます。 全体の速度、各要素は 1 つのフレームで isochronous パケットが転送された 1 つに関連付けます。

各要素に対して、要求の転送内容をすべてのバッファーの先頭からアイソクロナス各パケットのバイト オフセットを指定します。 その値を指定するを設定、 **UrbIsochronousTransfer.IsoPacket\[は\]します。オフセット**メンバー。 USB ドライバー スタックは、送信または受信するのにデータの量を追跡するために、指定した値を使用します。

**完全な高速転送のオフセットを設定**

例については、これらは、転送バッファーの配列エントリを最高速度で。 フル スピードは、クライアント ドライバーは、1,023 バイトまでの 1 つの isochronous パケットを転送する 1 つのフレームがあります。 25,575 バイトのバッファー転送では、各 1,023 バイト長、25 isochronous パケットを保持できます。 フレーム数が 25 の合計は、バッファー全体の必要があります。

``` syntax
Frame 1 IsoPacket [0].Offset = 0 (start address)
Frame 2 IsoPacket [1].Offset = 1023
Frame 3 IsoPacket [2].Offset = 2046
Frame 4 IsoPacket [3].Offset = 3069
...
Frame 25 IsoPacket [24].Offset = 24552

Total length transferred is 25,575 bytes.
```

**高速転送のオフセットを設定**

例については、高速転送バッファーの配列エントリのうちします。 例は、バッファーが 24,576 (バイト単位) と、クライアント ドライバーには、各 3, 072 バイト長、8 つ isochronous パケットを転送する 1 つのフレームが含まれていることを想定しています。

``` syntax
Microframe 1 IsoPacket [0].Offset = 0 (start address)
Microframe 2 IsoPacket [1].Offset = 3072
Microframe 3 IsoPacket [2].Offset = 6144
Microframe 4 IsoPacket [3].Offset = 9216
Microframe 5 IsoPacket [4].Offset = 12288
Microframe 6 IsoPacket [5].Offset = 15360
Microframe 7 IsoPacket [6].Offset = 18432
Microframe 8 IsoPacket [7].Offset = 21504

Total length transferred is 24,576 bytes.
```

**SuperSpeed 転送のオフセットを設定**

例については、SuperSpeed の配列オフセットです。 45,000 バイトまでの 1 つのフレームを転送することができます。 転送バッファーのサイズ 360,000 が 8 microframes 内に収まります。

``` syntax
Microframe 1 IsoPacket [0].Offset = 0 (start address)
Microframe 2 IsoPacket [1].Offset = 45000
Microframe 3 IsoPacket [2].Offset = 90000
Microframe 4 IsoPacket [3].Offset = 135000
Microframe 5 IsoPacket [4].Offset = 180000
Microframe 6 IsoPacket [5].Offset = 225000
Microframe 7 IsoPacket [6].Offset = 270000
Microframe 8 IsoPacket [7].Offset = 315000

Total length transferred is 360,000 bytes.
```

**UrbIsochronousTransfer.IsoPacket\[は\]** します。長さのメンバーでは、アイソクロナス URB の各パケットの長さは意味しません。 **IsoPacket\[は\]します。長さ**を実際のアイソクロナス内のデバイスから受信したバイト数を示すために、USB ドライバー スタックによって更新された転送。 転送をアイソクロナスで設定されている値はドライバー スタックには無視**IsoPacket\[は\]します。長さ**します。

<a name="remarks"></a>コメント
-------

**転送の開始の USB フレーム番号を指定します。**

**UrbIsochronousTransfer.StartFrame** URB のメンバーは、転送の開始の USB フレーム数を指定します。 クライアント ドライバーが、URB を送信する時間と USB ドライバー スタックが URB を処理する時間の間の待機時間は常にします。 そのため、クライアント ドライバーはドライバー URB を送信するときは、現在のフレームより後の開始フレームを常に指定する必要があります。 現在のフレーム数を取得するには、クライアント ドライバーが URB を送信できる\_関数\_取得\_現在\_フレーム\_USB ドライバー スタックへの要求の数 ([  **\_URB\_取得\_現在\_フレーム\_数**](https://msdn.microsoft.com/library/windows/hardware/ff540401))。

Isochronous 転送の場合、絶対パスは、現在のフレームの違い、 **StartFrame** USBD より小さい値があります\_ISO\_開始\_フレーム\_範囲。 適切な範囲内 StartFrame でない場合、USB ドライバー スタックの設定、**状態**URB ヘッダーのメンバー (を参照してください[  **\_URB\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/ff540409)) するUSBD\_状態\_不適切な\_開始\_フレームおよび全体の URB を破棄します。

**StartFrame** URB で指定された値は、最初のアイソクロナス URB パケットが転送されるフレーム数を示します。 以降のパケットのフレーム数は、バス スピードとエンドポイントの期間の値をポーリングに依存します。 などの高速転送では、最初のパケットで転送される**StartFrame**もう 1 つでパケットが転送される**StartFrame**+1、という具合です。 USB ドライバー スタックがフレームでのフル スピードのアイソクロナスのパケットを転送する方法が表示されます。

``` syntax
Frame (StartFrame)   IsoPacket [0]
Frame (StartFrame+1) IsoPacket [1]
Frame (StartFrame+2) IsoPacket [2]
Frame (StartFrame+3) IsoPacket [3]
...
```

間隔の値が 1 で高速のデバイスについては、フレーム番号は、すべての 8 番目 microframe を変更します。 USB ドライバー スタックがフレームでの高速の isochronous パケットを転送する方法が表示されます。

``` syntax
Frame (StartFrame) Microframe 1 IsoPacket [0]
...
Frame (StartFrame) Microframe 8 IsoPacket [7]
Frame (StartFrame+1) Microframe 1 IsoPacket [8]
...
Frame (StartFrame+1) Microframe 8 IsoPacket [15]
Frame (StartFrame+2) Microframe 1 IsoPacket [16]
...
Frame (StartFrame+2) Microframe 8 IsoPacket [23]
```

ときに URB、ドライバーのフレーム番号は URB 内のすべての isochronous パケットを破棄する USB ドライバー スタックのプロセスは、現在のフレーム数よりも低きます。 ドライバー スタックのセット、**状態**USBD に破棄されたパケットの各パケットの記述子のメンバー\_状態\_ISO\_NA\_遅れて\_し、USBPORT、USBD\_状態\_ISO\_いない\_アクセス\_BY\_ハードウェア、または USBD\_状態\_ISO\_いない\_アクセス\_遅延します。 ドライバー スタックがそれらのパケットのみを送信しようとした場合でも、URB でいくつかのパケットは破棄されますフレーム番号が、現在のフレーム数を超えています。

有効なためチェック**StartFrame** USB ドライバー スタックが高速の microframe; に各 isochronous パケットを読み込むため、メンバーがよりも若干複雑で高速な転送がただし、値**StartFrame** 1 ミリ秒 (完全な速度) フレーム番号、および microframe されませんを指します。 たとえば場合、 **StartFrame** URB で記録された値が 1 つ小さい、現在のフレームよりもドライバー スタックが 8 個までのパケットを破棄できます。 破棄されたパケットの正確な数は、アイソクロナス パイプに関連付けられている、ポーリング期間によって異なります。

## <a name="isochronous-transfer-example"></a>アイソクロナス転送の例


次のコード例では、フル_スピード、高速および SuperSpeed 伝送のアイソクロナスの転送、URB を作成する方法を示します。

```cpp
#define MAX_SUPPORTED_PACKETS_FOR_HIGH_OR_SUPER_SPEED 1024
#define MAX_SUPPORTED_PACKETS_FOR_FULL_SPEED 255

NTSTATUS CreateIsochURB  ( PDEVICE_OBJECT         DeviceObject,
                          PUSBD_PIPE_INFORMATION  PipeInfo,
                          ULONG                   TotalLength,
                          PMDL                    RequestMDL,
                          PURB                    Urb)
{  
    PDEVICE_EXTENSION        deviceExtension;
    ULONG                    numberOfPackets;
    ULONG                    numberOfFrames; 
    ULONG                    isochPacketSize = 0;
    ULONG                    transferSizePerFrame;
    ULONG                    currentFrameNumber;
    size_t                   urbSize;
    ULONG                    index;
    NTSTATUS                 ntStatus;  

    deviceExtension = (PDEVICE_EXTENSION) DeviceObject->DeviceExtension;

    isochPacketSize = PipeInfo->MaximumPacketSize;

    // For high-speed transfers
    if (deviceExtension->IsDeviceHighSpeed || deviceExtension->IsDeviceSuperSpeed) 
    {

        // Ideally you can pre-calculate numberOfPacketsPerFrame for the Pipe and 
        // store it in the pipe context.

        switch (PipeInfo->Interval) 
        {
        case 1:
            // Transfer period is every microframe (eight times a frame).
            numberOfPacketsPerFrame = 8;
            break;

        case 2:
            // Transfer period is every 2 microframes (four times a frame).
            numberOfPacketsPerFrame = 4;
            break;

        case 3:
            // Transfer period is every 4 microframes (twice in a frame).
            numperOfPacketsPerFrame = 2;
            break;

        case 4:
        default: 
            // Transfer period is every 8 microframes (once in a frame).
            numberOfPacketsPerFrame = 1;
            break;
        }


        //Calculate the number of packets.
        numberOfPackets = TotalLength / isochPacketSize;

        if (numberOfPackets > MAX_SUPPORTED_PACKETS_FOR_HIGH_OR_SUPER_SPEED) 
        {
            // Number of packets cannot be  greater than 1024.  
            ntStatus = STATUS_INVALID_PARAMETER;
            goto Exit;
        }

        if (numberOfPackets % numberOfPacketsPerFrame != 0) 
        {

            // Number of packets should be a multiple of numberOfPacketsPerFrame
            ntStatus = STATUS_INVALID_PARAMETER;
            goto Exit;
        }

    } 
    else if (deviceExtension->IsDeviceFullSpeed) 
    {
        //For full-speed transfers
        // Microsoft USB stack only supports bInterval value of 1 for
        // full-speed isochronous endpoints.


        //Calculate the number of packets.
        numberOfPacketsPerFrame = 1;

        numberOfPackets = TotalLength / isochPacketSize;

        if (numberOfPackets > MAX_SUPPORTED_PACKETS_FOR_FULL_SPEED) 
        {
            // Number of packets cannot be greater than 255. 
            ntStatus = STATUS_INVALID_PARAMETER;
            goto Exit;
        }

    }

    // Allocate an isochronous URB for the transfer
    ntStatus = USBD_IsochUrbAllocate (deviceExtension->UsbdHandle, 
        numberOfPackets, 
        &Urb);

    if (!NT_SUCCESS(ntStatus)) 
    {
        ntStatus = STATUS_INSUFFICIENT_RESOURCES;
        goto Exit;
    }

    urbSize = GET_ISO_URB_SIZE(numberOfPackets);

    Urb->UrbIsochronousTransfer.Hdr.Length = (USHORT) urbSize;
    Urb->UrbIsochronousTransfer.Hdr.Function = URB_FUNCTION_ISOCH_TRANSFER;
    Urb->UrbIsochronousTransfer.PipeHandle = PipeInfo->PipeHandle;

    if (USB_ENDPOINT_DIRECTION_IN(PipeInfo->EndpointAddress)) 
    {
        Urb->UrbIsochronousTransfer.TransferFlags = USBD_TRANSFER_DIRECTION_IN;
    }
    else
    {
        Urb->UrbIsochronousTransfer.TransferFlags = USBD_TRANSFER_DIRECTION_OUT;
    }

    Urb->UrbIsochronousTransfer.TransferBufferLength = TotalLength;
    Urb->UrbIsochronousTransfer.TransferBufferMDL = RequestMDL;
    Urb->UrbIsochronousTransfer.NumberOfPackets = numberOfPackets;
    Urb->UrbIsochronousTransfer.UrbLink = NULL;


    // Set the offsets for every packet for reads/writes

    for (index = 0; index < numberOfPackets; index++) 
    {
        Urb->UrbIsochronousTransfer.IsoPacket[index].Offset = index * isochPacketSize;
    } 

    // Length is a return value for isochronous IN transfers.  
    // Length is ignored by the USB driver stack for isochronous OUT transfers.

    Urb->UrbIsochronousTransfer.IsoPacket[index].Length = 0;
    Urb->UrbIsochronousTransfer.IsoPacket[index].Status = 0;

    // Set the USBD_START_ISO_TRANSFER_ASAP. The USB driver stack will calculate the start frame.
    // StartFrame value set by the client driver is ignored.
    Urb->UrbIsochronousTransfer.TransferFlags |= USBD_START_ISO_TRANSFER_ASAP;


Exit:

    return ntStatus;  
}  
```

## <a name="related-topics"></a>関連トピック
[USB I/O 操作](usb-device-i-o.md)  



