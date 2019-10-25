---
Description: このトピックでは、USB デバイスでアイソクロナスエンドポイントとの間でデータを転送するために、クライアントドライバーで USB 要求ブロック (URB) を作成する方法について説明します。
title: USB 等時性エンドポイントへのデータの転送方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d586ab2251a957c305980424bfd7e09532d05f7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824164"
---
# <a name="how-to-transfer-data-to-usb-isochronous-endpoints"></a>USB 等時性エンドポイントへのデータの転送方法


このトピックでは、USB デバイスでアイソクロナスエンドポイントとの間でデータを転送するために、クライアントドライバーで USB 要求ブロック (URB) を作成する方法について説明します。

ユニバーサルシリアルバス (USB) デバイスでは、オーディオ/ビデオストリーミングなど、時間に依存するデータを安定した速度で転送するために、アイソクロナスエンドポイントをサポートできます。 データを転送するために、クライアントドライバーは、アイソクロナスエンドポイントに対してデータの読み取りまたは書き込みを行う要求を発行します。 その結果、ホストコントローラーは、デバイスを定期的にポーリングすることによってデータを送受信するアイソクロナス転送を開始します。

高速および高速のデバイスの場合、ポーリングは (IN/OUT) トークンパケットを使用して行われます。 エンドポイントがデータを送信する準備ができたら、デバイスはデータを送信することによって、トークンパケット内のいずれかに応答します。 デバイスに書き込むには、ホストコントローラーは、OUT トークンパケットの後にデータパケットを送信します。 ホストコントローラーまたはデバイスでハンドシェイクパケットが送信されないため、保証された配信が行われません。 ホストコントローラーは転送を再試行しないため、エラーが発生するとデータが失われる可能性があります。

アイソクロナス転送の場合、ホストコントローラーは特定の期間をバスに予約します。 アイソクロナスエンドポイントの予約時間を管理するには、時間を連続する論理 chucks に分割して、*バス間隔*と呼びます。 バス間隔の単位はバス速度によって異なります。

完全な速度の場合、バス間隔は*フレーム*です。 フレームの長さは1ミリ秒です。

高速および SuperSpeed の場合、バス間隔はマイクロフレームです。 マイクロフレームの長さは125マイクロ秒です。 8個の連続するマイクロフレームは、1つの高速または SuperSpeed フレームを構成します。

アイソクロナス転送はパケットベースです。 このトピックの「*アイソクロナスパケット*とは」という用語は、1つのバス間隔で転送されるデータの量を指します。 エンドポイントの特性によって、各パケットのサイズが固定され、エンドポイントの特性によって決定されます。

クライアントドライバーは、要求の URB を作成し、USB ドライバースタックに URB を送信することによって、アイソクロナス転送を開始します。 要求は、USB ドライバースタック内の下位のドライバーのいずれかによって処理されます。 USB ドライバースタックは、URB を受け取ると、一連の検証を実行し、要求のトランザクションをスケジュールします。 全速度で、各バス間隔で転送されるアイソクロナスパケットは、ネットワーク上の1つのトランザクションに含まれます。 特定の高速デバイスでは、バス間隔で複数のトランザクションを許可します。 この場合、クライアントドライバーは、1つの要求 (URB) で、アイソクロナスパケット内のデータをさらに送受信できます。 SuperSpeed デバイスでは、複数のトランザクションとバースト転送がサポートされているため、バス間隔ごとにさらに多くのバイトを利用できます。 バースト転送の詳細については、「USB 3.0 仕様ページ9-42」を参照してください。

### <a name="prerequisites"></a>前提条件

アイソクロナス転送の要求を作成する前に、アイソクロナスエンドポイント用に開かれているパイプに関する情報が必要です。

Windows Driver Model (WDM) ルーチンを使用するクライアントドライバーには、 [**USBD\_インターフェイス\_LIST\_ENTRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_usbd_interface_list_entry)配列の[**USBD\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)構造のいずれかにパイプ情報が含まれています。 クライアントドライバーは、デバイスの構成またはインターフェイスを選択するために、ドライバーの前の要求でその配列を取得します。

Windows Driver Framework (WDF) クライアントドライバーは、フレームワークのターゲットパイプオブジェクトへの参照を取得し、 [**WdfUsbTargetPipeGetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation)を呼び出して[**WDF\_USB\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_pipe_information)のパイプ情報を取得する必要があります。データ.

パイプ情報に基づいて、次の情報セットを決定します。

-   ホストコントローラーが各パケットのパイプに送信できるデータの量。

    クライアントドライバーが要求で送信できるデータの量は、ホストコントローラーがエンドポイントから送受信できる最大バイト数を超えることはできません。 最大バイト数は、 [**USBD\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)と[**WDF\_USB\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_pipe_information)構造体の**MaximumPacketSize**メンバーによって示されます。 USB ドライバースタックは、選択構成または選択インターフェイスの要求中に、 **MaximumPacketSize**値を設定します。

    全速度のデバイスの場合、 **MaximumPacketSize**はエンドポイント記述子の**wMaxPacketSize**フィールドの最初の11ビットから派生します。これは、エンドポイントがトランザクションで送受信できる最大バイト数を示します。 全速度のデバイスの場合、コントローラーはバス間隔ごとに1つのトランザクションを送信します。

    高速のアイソクロナス転送では、ホストコントローラーは、エンドポイントで許可されている場合、追加のトランザクションをバス間隔で送信できます。 追加トランザクションの数はデバイスによって設定され、 **wMaxPacketSize**のビット 12.. 11 で示されます。 この数値には、0、1、または2を指定できます。 12.. 11 が0を示す場合、マイクロフレームあたりの追加トランザクションは、エンドポイントでサポートされていません。 この数値が1の場合、ホストコントローラーは追加のトランザクション (マイクロフレームあたり2つのトランザクションの合計) を送信できます。2 2 つの追加トランザクション (マイクロフレームあたり3トランザクションの合計) を示します。 USB ドライバースタックによって設定される**MaximumPacketSize**値には、追加のトランザクションで送信できるバイト数が含まれます。

    SuperSpeed アイソクロナス転送の場合、USB\_SUPERSPEED\_エンドポイント\_コンパニオン\_記述子の特定の値 (Usbspec を参照) が重要です。 USB ドライバースタックは、これらの値を使用して、バス間隔の最大バイト数を計算します。

    -   エンドポイントコンパニオン記述子の**Mult**フィールド。 SuperSpeed アイソクロナス転送では、追加のトランザクション (高速デバイスと同様) がバーストトランザクションと呼ばれます。 **Mult**値は、エンドポイントがサポートするバーストトランザクションの最大数を示します。 サービス間隔には、最大3つのバーストトランザクション (インデックス 0 ~ 2) を指定できます。
    -   エンドポイントコンパニオン記述子の**Bmaxburst**フィールド。 この値は、1つのバーストトランザクション内に存在できる**wMaxPacketSize**のチャンクの数を示します。 バーストトランザクションでは、最大16個のチャンク (インデックス0から 15) を使用できます。
    -   **Wbytesperinterval**は、ホストがバス間隔で送信または受信できるバイトの合計数を示します。 バス間隔あたりの最大バイト数は、(**Bmaxburst**+ 1) \* (**Mult**+ 1) \* **wMaxPacketSize**として計算できますが、USB 3.0 仕様では**wbytesperinterval**値を使用することをお勧めします。 **Wbytesperinterval**値は、その計算値以下である必要があります。

    **重要** クライアントドライバーの場合は、上記で説明した値のみが情報に使用されます。 ドライバーは、常にエンドポイント記述子の**MaximumPacketSize**値を使用して、転送バッファーのレイアウトを決定する必要があります。



-   エンドポイントは、どのくらいの頻度でデータを送受信します。

    **Interval**メンバーは、エンドポイントがデータを送受信する頻度を決定するために使用されます。 デバイスはその値を設定し、クライアントドライバーは変更できません。 USB ドライバースタックでは、別の数値を使用して、データストリームにアイソクロナスパケットを挿入する頻度を決定します。ポーリング期間は、**間隔**の値から派生します。

    高速転送の場合、**間隔**とポーリング期間の値は常に1です。USB ドライバースタックでは、他の値は無視されます。

    次の表に、高速転送と SuperSpeed 転送の**間隔**と計算されたポーリング期間を示します。

    | 間隔 | ポーリング期間 (2Interval-1)                      |
    |----------|---------------------------------------------------|
    | 1        | 1データはバス間隔ごとに転送されます。        |
    | 2        | 3データは、2番目のバス間隔ごとに転送されます。 |
    | 3        | 4/44番目のバス間隔ごとにデータが転送されます。 |
    | ホーム フォルダーが置かれているコンピューターにアクセスできない        | 8データは、8番目のバス間隔ごとに転送されます。 |



-   各バス速度のパケット数の制限は何ですか。

    URB では、最大255のアイソクロナスパケットを送信できるのは、全速度のデバイスに対してのみです。1024高速および SuperSpeed デバイスでの URB 内のパケット数。 URB で送信するパケットの数は、各フレームのパケット数の倍数である必要があります。

    | ポーリング期間 | 高速/SuperSpeed のパケット数 |
    |----------------|---------------------------------------------|
    | 1              | 8の倍数                               |
    | 2              | 4の倍数                               |
    | 3              | 2の倍数                               |
    | ホーム フォルダーが置かれているコンピューターにアクセスできない              | 任意                                         |



**WMaxPacketSize**が1023の高速エンドポイントの例を考えてみましょう。 この例では、アプリケーションによって25575バイトのバッファーが提供されています。 このバッファーの転送には、25台のアイソクロナスパケット (25575/1023) が必要です。

エンドポイント記述子に示されている次の特性を持つ高速エンドポイントの例を考えてみましょう。

-   **wMaxPacketSize**は1024です。
-   Bits 12.. 11 では、2つのトランザクションが追加で示されます。
-   **間隔**は1です。

クライアントドライバーによって構成が選択されると、MaximumPacketSize パイプのは3072バイト (\* トランザクション総数は**wMaxPacketSize**) を示します。 追加のトランザクションを使用すると、クライアントドライバーはすべてのマイクロフレームで3072バイト、1フレームで合計24576バイトを転送できます。 次の図は、高速転送のために1つのマイクロフレームでアイソクロナスパケットが転送される頻度を示しています。

![アイソクロナス転送](images/iso-packets.png)

エンドポイントおよび SuperSpeed エンドポイントコンパニオン記述子に示されている以下の特性を持つ SuperSpeed エンドポイントの例を考えてみましょう。

-   **wMaxPacketSize**は1024です。
-   **Bmaxburst**は15です。
-   **間隔**は1です。
-   **Mult**は2です。
-   **Wbytesperinterval**は45000です。

前の例では、最大バイト数を**wMaxPacketSize** \* (**bmaxburst** + 1) \* (**Mult** + 1) として計算し、49152バイトにすることができましたが、デバイスは**wbytesperinterval**に値を制限します。45000バイトの値。 この値は、 **MaximumPacketSize** 45000 にも反映されます。 クライアントドライバーは、 **MaximumPacketSize**値のみを使用する必要があります。 この例では、要求を3つのバーストトランザクションに分割できます。 最初の2つのバーストトランザクションには、 **wMaxPacketSize**の16個のチャンクが含まれています。 最後のバーストトランザクションには、残りのバイトを保持する12個のチャンクが含まれています。 このイメージは、SuperSpeed 伝送のために、ポーリング間隔とアイソクロナスパケット経由で転送されたバイト数を示します。

![superspeed アイソクロナス](images/iso-packets-superspeed.png)

次の手順では、アイソクロナス転送の要求を作成する方法について説明します。

1.  各アイソクロナスパケットのサイズを取得します。
2.  フレームあたりのアイソクロナスパケット数を決定します。
3.  転送バッファー全体を保持するために必要なアイソクロナスパケットの数を計算します。
4.  転送の詳細を説明するために、 [**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造体を割り当てます。
5.  パケットオフセットなど、各アイソクロナスパケットの詳細を指定します。

アイソクロナス転送要求の送信に関する完全なコード例については、USBSAMP をご覧ください。

このトピックのこの例では、USBSAMP のアイソクロナス転送の実装を簡略化します。 このサンプルでは、転送に必要な合計フレーム数を計算します。 フレームで送信できるデータの量に基づいて、転送バッファーはより小さなチャンクサイズのバイトに分割されます。

次の手順では、前の手順を詳述し、クライアントドライバーが高速のアイソクロナスエンドポイントのアイソクロナス転送要求を作成して送信するために使用できる計算とルーチンを示します。 このプロシージャで使用される値は、前に説明したエンドポイントの特性の例に基づいています。

<a name="instructions"></a>手順
------------

### <a href="" id="get-the-size-of-an-isochronous-packet--"></a>手順 1: アイソクロナスパケットのサイズを取得します。

パイプの**MaximumPacketSize**値を調べることによって、アイソクロナスパケットのサイズを決定します。

高速転送では、アイソクロナスパケットのサイズは1つのフレームで転送可能なバイト数です。 高速伝送と SuperSpeed 転送の場合、1つのマイクロフレームで転送できる合計バイト数は、アイソクロナスパケットのサイズです。 これらの値は、パイプの**MaximumPacketSize**に示されます。

この例では、 **MaximumPacketSize**はフレームあたり1023バイト (全速度) です。マイクロフレームあたり3072バイト (高速);マイクロフレームあたり45000バイト (SuperSpeed)。

**メモ** **MaximumPacketSize**値は、アイソクロナスパケットの最大許容サイズを示します。 クライアントドライバーは、各アイソクロナスパケットのサイズを**MaximumPacketSize**値よりも小さい値に設定できます。



### <a href="" id="determine-the-number-of-isochronous-packets-per-frame-"></a>手順 2: フレームあたりのアイソクロナスパケット数を決定します。

高速転送では、各フレームで1つのアイソクロナスパケットを転送します。

高速伝送と SuperSpeed 転送の場合、この値は Interval 値から派生する必要があります。 この例では、Interval は1です。 そのため、アイソクロナスパケットの数はフレームあたり8個である必要があります。 その他の間隔の値については、「前提条件」セクションの表を参照してください。

### <a href="" id="calculate-the-number-of-isochronous-packets-that-are-required-to-hold-the-entire-transfer-buffer-"></a>手順 3: 転送バッファー全体を保持するのに必要なアイソクロナスパケットの数を計算します。

バッファー全体を転送するために必要なアイソクロナスパケットの数を計算します。 この値は、転送バッファーの長さをアイソクロナスパケットのサイズで割ることによって計算できます。

この例では、各アイソクロナスパケットのサイズが**MaximumPacketSize**で、転送バッファーの長さが**MaximumPacketSize**値の倍数であると想定しています。

たとえば、フルスピード転送の場合、指定されたバッファーの25575バイトには25個のアイソクロナスパケット (25575/1023) が必要です。 高速転送の場合、サイズが24576のバッファーは、転送用に8つのアイソクロナスパケット (24576/3072) に分割されます。 SuperSpeed の場合、サイズが36万バイトのバッファーは8つのアイソクロナスパケット (360000/45000) に収まります。

クライアントドライバーは、次の要件を検証する必要があります。

-   アイソクロナスパケットの数は、フレームあたりのパケット数の倍数である必要があります。
-   完全な速度のデバイスでは、転送に必要なアイソクロナスパケットの最大数が255を超えないようにする必要があります。高速または SuperSpeed デバイスの場合は1024。

### <a href="" id="allocate-an-urb-structure-to-describe-the-details-of-the-transfer-"></a>手順 4: 転送の詳細を説明するために、URB 構造体を割り当てます。

1.  非ページプールに[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造体を割り当てます。

    クライアントドライバーが WDM ルーチンを使用している場合、windows 8 用の Windows Driver Kit (WDK) がある場合、ドライバーは[**USBD\_IsochUrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_isochurballocate)を呼び出す必要があります。 クライアントドライバーは、このルーチンを使用して、windows Vista 以降のバージョンの Windows オペレーティングシステムを対象にすることができます。 Windows 8 用の WDK がない場合、またはクライアントドライバーが以前のバージョンのオペレーティングシステムを対象としている場合は、 [**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)を呼び出して、その構造をスタックまたは非ページプールに割り当てることができます。

    WDF クライアントドライバーは、 [**WdfUsbTargetDeviceCreateIsochUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateisochurb)メソッドを呼び出して、 [**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造体にメモリを割り当てることができます。

2.  [**Urb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造体の**UrbIsochronousTransfer**メンバーは、アイソクロナス転送の詳細を記述する[ **\_URB\_ISOCH\_TRANSFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_isoch_transfer)構造体を指します。 次の**UrbIsochronousTransfer**メンバーを次のように初期化します。
    -   **UrbIsochronousTransfer**メンバーに URB のサイズを設定します。 URB のサイズを取得するには、 [**get\_ISO\_urb\_size**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-get_iso_urb_size)マクロを呼び出し、パケットの数を指定します。
    -   **UrbIsochronousTransfer**メンバーを `URB_FUNCTION_ISOCH_TRANSFER`に設定します。
    -   **UrbIsochronousTransfer**のメンバーに、アイソクロナスパケットの数を設定します。
    -   UrbIsochronousTransfer を、エンドポイントに関連付けられているパイプの不透明ハンドルに設定し**ます。** パイプハンドルが、Universal Serial Bus (USB) ドライバースタックで使用される USBD パイプハンドルであることを確認します。

        USBD パイプハンドルを取得するために、WDF client ドライバーは[**WdfUsbTargetPipeWdmGetPipeHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipewdmgetpipehandle)メソッドを呼び出し、フレームワークのパイプオブジェクトへの WDFUSBPIPE ハンドルを指定できます。 WDM クライアントドライバーは、 [**USBD\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)構造体の**PipeHandle**メンバーで取得したものと同じハンドルを使用する必要があります。

    -   転送の方向を指定します。 UrbIsochronousTransfer を USBD に設定して、(デバイスからの) アイソクロナス転送の場合は、で\_を\_\_転送**します**。USBD\_転送では、(デバイスへの書き込み) アイソクロナス転送に対して\_方向\_送信します。
    -   **UrbIsochronousTransfer**で USBD\_START\_ISO\_転送\_ASAP フラグを指定します。TransferFlags。 フラグは、次の適切なフレームで転送を送信するように USB ドライバースタックに指示します。 クライアントドライバーがこのパイプのアイソクロナスの URB を初めて送信する場合、ドライバースタックは可能な限り早く、URB 内のアイソクロナスパケットを送信します。 USB ドライバースタックは、そのパイプの後続の URBs に使用する次のフレームを追跡します。 USBD\_を使用するその後のアイソクロナス URB の送信で遅延が発生した場合、\_ASAP フラグの転送\_ISO\_転送を開始します。ドライバースタックは、その URB の一部またはすべてのパケットが遅延していると見なし、それらのパケットを転送しません。

        USB ドライバースタックは、そのパイプの前の URB を完了した後、スタックが1024フレームに対してアイソクロナスの URB を受信しない場合、USBD\_START\_ISO\_TRANSFER\_ASAP start フレーム追跡をリセットします。 USBD\_START\_ISO\_転送\_ASAP フラグを指定する代わりに、開始フレームを指定できます。 詳細については、「解説」を参照してください。

    -   転送バッファーとそのサイズを指定します。 **UrbIsochronousTransfer**のバッファーへのポインター、または**UrbIsochronousTransfer**内のバッファーを記述する[**MDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl)を設定できます。

        転送バッファーの[**MDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl)を取得するために、WDF クライアントドライバーは、転送の方向に応じて[**WdfRequestRetrieveOutputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)または[**WdfRequestRetrieveInputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)を呼び出すことができます。

### <a href="" id="specify-the-details-of-each-isochronous-packet-in-the-transfer-"></a>手順 5: 転送における各アイソクロナスパケットの詳細を指定します。

USB ドライバースタックは、パケットに含まれるデータではなく、各アイソクロナスパケットに関する情報を保持するのに十分な大きさの新しい[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造を割り当てます。 **URB**構造体では、 **UrbIsochronousTransfer の IsoPacket**メンバーは、転送中の各アイソクロナスパケットの詳細を示す[**USBD\_ISO\_パケット\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_iso_packet_descriptor)の配列です。 パケットは連続している必要があります。 配列内の要素の数は、URB の**UrbIsochronousTransfer**メンバーに指定されているアイソクロナスパケットの数である必要があります。

高速転送の場合、配列内の各要素は1つのマイクロフレーム内の1つのアイソクロナスパケットに関連付けられます。 全スピードでは、各要素が1つのフレームで転送された1つのアイソクロナスパケットに関連付けられます。

各要素について、要求の転送バッファー全体の先頭からの各アイソクロナスパケットのバイトオフセットを指定します。 この値は、\]\[を設定することによって指定できます。 **オフセット**メンバー。 USB ドライバースタックは、指定された値を使用して、送信または受信するデータの量を追跡します。

**フルスピード転送のオフセットの設定**

この例では、転送バッファーの配列エントリは完全に高速です。 クライアントドライバーは、最大で1023バイトまでの1つのアイソクロナスパケットを転送する1つのフレームを備えています。 25575バイトの転送バッファーでは、1023バイトごとに25個のアイソクロナスパケットを保持できます。 バッファー全体には、合計25フレームが必要です。

``` syntax
Frame 1 IsoPacket [0].Offset = 0 (start address)
Frame 2 IsoPacket [1].Offset = 1023
Frame 3 IsoPacket [2].Offset = 2046
Frame 4 IsoPacket [3].Offset = 3069
...
Frame 25 IsoPacket [24].Offset = 24552

Total length transferred is 25,575 bytes.
```

**高速転送のオフセットの設定**

この例では、転送バッファーの配列エントリが高速です。 この例では、バッファーが24576バイトであることを前提としています。クライアントドライバーは、8つのアイソクロナスパケット (3072 バイト) を転送するためのフレームを1つ持ちます。

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

**SuperSpeed 転送のオフセットの設定**

この例では、SuperSpeed の配列オフセットです。 最大45000バイトを1つのフレームに転送できます。 サイズ36万の転送バッファーは8マイクロフレーム内に収まります。

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

**\]\[UrbIsochronousTransfer** 。Length メンバーは、アイソクロナスの URB の各パケットの長さを意味しません。 **IsoPacket\[\]。長さ**は、USB ドライバースタックによって更新され、転送中のアイソクロナスのデバイスから実際に受信したバイト数を示します。 アイソクロナス出力転送の場合、ドライバースタックは、IsoPacket\[i\]で設定されている値を無視**します。長さ**。

<a name="remarks"></a>注釈
-------

**転送の開始 USB フレーム番号を指定します**

URB の UrbIsochronousTransfer メンバーは、転送の開始 USB フレーム番号を指定します **。** クライアントドライバーが URB を送信してから、USB ドライバースタックが URB を処理するまでの間には常に待機時間があります。 したがって、クライアントドライバーは、ドライバーが URB を送信するときに、常に最新のフレームよりも後の開始フレームを指定する必要があります。 現在のフレーム番号を取得するには、クライアントドライバーが URB\_関数を送信して\_現在の\_FRAME\_NUMBER 要求を USB ドライバースタックに取得\_ます ([ **\_urb\_\_現在の\_フレームを取得します。\_番号**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_get_current_frame_number))。

アイソクロナス転送の場合、現在のフレームと**Startframe**の値の絶対差は、USBD\_ISO\_\_フレーム\_範囲を開始する必要があります。 StartFrame が適切な範囲内にない場合、USB ドライバースタックは、URB ヘッダーの**status**メンバー ( [ **\_urb\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_header)を参照) を USBD\_\_status に設定します。これは、正しくない\_開始\_フレームであり、urb 全体を破棄します。

URB に指定された**startframe**値は、urb の最初のアイソクロナスパケットが転送されるフレーム番号を示します。 後続のパケットのフレーム番号は、エンドポイントのバス速度とポーリング期間の値によって異なります。 たとえば、高速転送の場合、最初のパケットは**Startframe**で転送されます。2番目のパケットは、 **Startframe**+ 1 のように転送されます。 USB ドライバースタックが、フレーム内のアイソクロナスパケットを完全に転送する方法は、次のようになります。

``` syntax
Frame (StartFrame)   IsoPacket [0]
Frame (StartFrame+1) IsoPacket [1]
Frame (StartFrame+2) IsoPacket [2]
Frame (StartFrame+3) IsoPacket [3]
...
```

間隔の値が1の高速デバイスの場合、フレーム番号は8フレームごとに変更されます。 USB ドライバーのスタックがパケットを高速に転送する方法は、次のようになります。

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

USB ドライバースタックが URB を処理すると、ドライバーは、フレーム番号が現在のフレーム番号よりも小さい、URB 内のすべてのアイソクロナスパケットを破棄します。 ドライバースタックは、破棄された各パケットのパケット記述子の**status**メンバーを USBD\_STATUS\_ISO\_NA\_遅延\_usbport、USBD\_STATUS\_iso\_\_アクセスされていません @no__\_HW、または USBD\_状態\_ISO\_、\_にアクセスされていないことを。 URB 内の一部のパケットが破棄されても、ドライバースタックは、フレーム番号が現在のフレーム番号よりも大きいパケットだけを送信しようとします。

有効な**startframe**メンバーのチェックは、USB ドライバースタックが各アイソクロナスパケットを高速マイクロフレームに読み込むため、高速転送では若干複雑になります。ただし、 **Startframe**の値はマイクロフレームではなく、1ミリ秒 (全速度) のフレーム番号を表します。 たとえば、URB に記録された**Startframe**の値が現在のフレームよりも1小さい場合、ドライバースタックは最大8個のパケットを破棄できます。 破棄されたパケットの正確な数は、アイソクロナスパイプに関連付けられているポーリング期間によって異なります。

## <a name="isochronous-transfer-example"></a>アイソクロナス転送の例


次のコード例では、全速度、高速、SuperSpeed 伝送のために、アイソクロナス転送の URB を作成する方法を示します。

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
[USB i/o 操作](usb-device-i-o.md)  



