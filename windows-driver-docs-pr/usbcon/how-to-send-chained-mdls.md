---
Description: このトピックでは、USB ドライバースタックのチェーン MDLs 機能について、およびクライアントドライバーが MDL 構造体のチェーンとして転送バッファーを送信する方法について説明します。
title: チェーン化された MDL の送信方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75581208dab5c66926122ac6cf28662236e4177a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837545"
---
# <a name="how-to-send-chained-mdls"></a>チェーン化された MDL の送信方法


このトピックでは、USB ドライバースタックのチェーン MDLs 機能について、およびクライアントドライバーが[**MDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl)構造体のチェーンとして転送バッファーを送信する方法について説明します。

ほとんどの USB ホストコントローラーでは、転送バッファーが実質的に連続している必要があります。 実質的に連続しているは、ページ内のどこでもバッファーを開始および終了できるが、バッファーの残りの部分はページ境界で開始して終了する必要があることを意味します。 多くの USB クライアントドライバーは、その要件を満たすことができます。 ただし、特定のクライアントドライバー (特に、バッファーとの間で追加のデータを追加または削除する必要があるドライバー) については、転送バッファーに実質的に連続するメモリを割り当てることは推奨されません。

たとえば、3つのドライバー (ネットワークプロトコルドライバー、中間ドライバー、およびミニポートドライバー) のネットワークスタックを考えてみます。 プロトコルドライバーは転送を開始し、スタック内の次のドライバー (中間ドライバー) にパケットを送信します。 中間ドライバーは、(別のメモリブロックに含まれる) カスタムヘッダーをパケットに追加しようとしています。 中間ドライバーは、そのヘッダーと受信パケットをスタック内の次のドライバー (ミニポートドライバー) に送信します。 ミニポートドライバーは、USB ドライバースタックとのインターフェイスを持つため、実質的に連続する転送バッファーを準備する必要があります。 このようなバッファーを作成するために、ミニポートドライバーは大きなバッファーを割り当て、カスタムヘッダーを追加してから、ペイロードをコピーします。 ペイロードは通常は大きいため、ペイロード全体をコピーすると、パフォーマンスに大きな影響を与える可能性があります。

クライアントドライバーは、転送バッファーを*メモリ記述子リスト*(mdls) のチェーンとして送信することによって、パフォーマンスへの影響を克服できます。 Windows 8 の新しい USB ドライバースタックは、クライアントドライバーのチェーンされた MDL (「 [**mdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl)」を参照) を受け入れることができます。 チェーン化された MDL を指定することにより、クライアントドライバーは、余分なコピー操作を実行する代わりに、メモリ内の連続していないページを参照できます。 この機能により、バッファーの数、サイズ、およびアラインメントに関する制限がなくなり、転送バッファーを物理メモリに分割できるようになります。

チェーン MDLs を使用するには、クライアントドライバーは、Windows によって読み込まれた基になる USB ドライバースタックが機能をサポートしているかどうかを検出してから、適切な順序で MDLs のチェーンを構築する必要があります。

### <a name="prerequisites"></a>前提条件

チェーン化された MDL 機能は、一括、アイソクロナス、および割り込み転送でのみサポートされています。 チェーン化された MDL 機能に対してクエリを実行する前に、クライアントドライバーに、ドライバーの USB ドライバースタックへの登録用の USBD ハンドルがあることを確認してください。 USBD ハンドルを作成するには、 [**USBD\_CreateHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)を呼び出します。通常、クライアントドライバーは[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンで USBD ハンドルを作成します。

クライアントドライバーの IRP\_にあるチェーン化された MDL 機能に対してクエリを実行し、 [ **\_デバイスハンドラーを開始\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)か、後でいつでも開始できます。 クライアントドライバーは、 [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンでこの機能のクエリを実行することはできません。

<a name="instructions"></a>手順
------------

1.  [**USBD\_QueryUsbCapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))ルーチンを呼び出して、USB ドライバースタックがチェーン mdls 機能をサポートしているかどうかを確認します。 その機能を照会するには、GUID として UsbCapabilityChainedMdls を指定します。 *Outputbuffer*パラメーターを NULL に設定し、 *outputbuffer*パラメーターを0に設定します。
2.  [**USBD\_QueryUsbCapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))によって返された NTSTATUS 値を確認し、結果を評価します。 ルーチンが正常に完了した場合は、チェーン MDLs 機能がサポートされます。 それ以外の値は、機能がサポートされていないことを示します。
3.  MDLs のチェーンを作成します。 各[**mdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl)には、別の**Mdl**を指す**次**のポインターがあります。

    ドライバーは、**次**のポインターを手動で設定することによって、チェーン MDL を構築できます。

    前の例では、プロトコルドライバーはパケットを MDL として送信します。 中間ドライバーは、ヘッダーデータを使用してメモリブロックを参照する別の[**MDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl)を作成できます。 チェーンを作成するために、中間ドライバーは、プロトコルドライバーから受信した MDL へのヘッダー MDL の**次**のポインターを指すことができます。 その後、中間ドライバーは2つの MDLs のチェーンをミニポートドライバーに転送します。これは、要求の URB でチェーンされている MDL への参照を提供し、USB ドライバースタックに要求を送信します。 詳細については、「 [MDLs の使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-mdls)」を参照してください。

4.  チェーン MDLs を使用する i/o 要求の URB を構築するときに、関連付けられた[**urb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造の**transferbuffermdl**メンバーを設定します ( [ **\_urb\_一括\_、\_INTERRUPT\_TRANSFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_bulk_or_interrupt_transfer) 、 [ **\_URB\_\_ISOCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_isoch_transfer)をチェーン内の最初の MDL に転送) し、 **Transferbufferlength**に転送する合計バイト数を設定します。 データが、MDL チェーン内の複数の MDL エントリにまたがる場合があります。

    Windows 8 では、クライアントドライバーがデータ転送にチェーン MDLs を使用できるようにする、2つの新しい種類の URB 関数が追加されています。 この機能を使用する場合は、URB ヘッダーの**関数**メンバーが次の urb 関数のいずれかに設定されていることを確認してください。

    -   URB\_関数\_一括\_または\_中断\_\_のチェーン化\_を使用した\_の転送
    -   URB\_関数\_ISOCH\_TRANSFER\_\_を使用した転送

    これらの URB 関数の詳細については、「 [ **\_urb\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_header)」を参照してください。

<a name="remarks"></a>注釈
-------

基になる USB ドライバースタックに対してクエリを実行し、ドライバースタックがチェーン MDLs を受け入れることができるかどうかを判断するコード例については、「 [**USBD\_QueryUsbCapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))」を参照してください。

## <a name="related-topics"></a>関連トピック
[USB i/o 操作](usb-device-i-o.md)  



