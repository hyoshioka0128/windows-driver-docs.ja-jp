---
Description: このトピックでは、チェーンの MDLs 機能、USB ドライバー スタックと、クライアント ドライバーが MDL 構造体のチェーンとして転送バッファーを送信する方法の詳細について学びます。
title: チェーン化された MDL の送信方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 851907228b3fe2ed8075224181cd3773da15a936
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363878"
---
# <a name="how-to-send-chained-mdls"></a>チェーン化された MDL の送信方法


このトピックでは、USB ドライバー スタック、およびクライアント ドライバーがのチェーンとして転送バッファーを送信する方法では、チェーンの MDLs 機能について学習[ **MDL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_mdl)構造体。

ほとんどの USB ホスト コント ローラーには、実質的に連続して転送バッファーが必要です。 連続する事実上は、バッファーの開始し、ページがバッファーの残りの部分で任意の場所を終了できることを意味する必要があります起動し、ページの境界で終了します。 多くの USB クライアント ドライバーでは、その要件を満たすことができます。 ただし、特定のクライアント ドライバーが特に必要とする内容を追加または削除するか、バッファーから追加のデータの転送バッファーのほぼ連続したメモリの割り当てはことをお勧めします。

たとえば、次の 3 つのドライバー、ネットワーク プロトコルのドライバー、中間ドライバーでは、およびミニポート ドライバーのネットワーク スタックを検討してください。 プロトコル ドライバーの転送を開始して、スタック内の次のドライバーにパケットを送信します。 中間ドライバー。 中間のドライバーは、パケットにカスタム ヘッダー (メモリの個別ブロックに含まれる) を追加する場合します。 中間ドライバー ヘッダーと、受信したパケットの場合をスタック内の次のドライバーに送信されます: ミニポート ドライバー。 ミニポート ドライバーでは、USB ドライバー スタックとのインターフェイスし、そのため、実質的に連続する転送バッファーを準備する必要があります。 そのようなバッファーを作成するには、ミニポート ドライバーは、大きなバッファーを割り当てます。 カスタム ヘッダーを追加し、ペイロードをコピーします。 ペイロードは通常、大規模なため、ペイロード全体をコピーすると、パフォーマンスに大きな影響があります。

クライアント ドライバーのチェーンとして転送バッファーを送信してそのパフォーマンスに与える影響を克服できます*メモリ記述子のリスト*(MDLs)。 Windows 8 の新しい USB ドライバー スタックは連鎖 MDL を受信できる (を参照してください[ **MDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_mdl))、クライアント ドライバーから。 クライアント ドライバーは連鎖 MDL を指定することによって、余分なコピー操作を実行する代わりに、メモリ内の不連続のページを参照できます。 機能は、数、サイズ、および物理メモリのセグメント化の転送バッファーの許可、バッファーの配置に関する制約を削除します。

連鎖 MDLs を使用するにはクライアント ドライバーは、Windows によって読み込まれる、基になる USB ドライバー スタックは、機能をサポートするかどうかを検出し、MDLs の適切な順序でのチェーンを構築しする必要があります。

### <a name="prerequisites"></a>前提条件

連鎖 MDL 機能は一括でアイソクロナス、のみサポートされており、割り込みを転送します。 連鎖 MDL 機能のクエリを実行する前に、クライアント ドライバーがドライバーの登録は USB ドライバー スタックと USBD ハンドルを確認します。 USBD ハンドルを作成するには[ **USBD\_CreateHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_createhandle)します。通常、クライアント ドライバーは USBD のハンドルを作成します。 その[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチン。

クライアント ドライバーの連鎖 MDL 機能を照会できます[ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)ハンドラーまたはそれ以降いつでもできます。 クライアント ドライバーかでこの機能を照会する必要があります、 [ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチン。

<a name="instructions"></a>手順
------------

1.  呼び出す、 [ **USBD\_QueryUsbCapability** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))ルーチンを USB ドライバー スタックが連鎖 MDLs 機能をサポートするかどうかを確認します。 その機能を照会するには、GUID として UsbCapabilityChainedMdls を指定します。 設定、 *OutputBuffer*パラメーターを NULL と*OutputBufferSize*パラメーターを 0 にします。
2.  によって返される NTSTATUS 値をチェックして[ **USBD\_QueryUsbCapability** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))し、結果を評価します。 ルーチンが正常に完了すると、連鎖 MDLs 機能はサポートされています。 その他の値は、機能がサポートされていないことを示します。
3.  MDLs のチェーンを作成します。 各[ **MDL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_mdl)が、**次**別を指すポインター **MDL**します。

    手動で設定して、ドライバーが MDL のチェーンの構築、**次**ポインター。

    前の例では、プロトコル ドライバーには、MDL として、パケットを送信します。 中間のドライバーを作成[ **MDL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_mdl)ヘッダー データを使用してメモリのブロックを参照します。 チェーンを作成する中間のドライバーがヘッダー MDL をポイントできます**次**プロトコル ドライバーから受信した MDL へのポインター。 中間のドライバーは、ミニポート ドライバーで要求の URB 連鎖 MDL への参照を提供し、USB ドライバー スタックに要求を送信する 2 つの MDLs のチェーンを転送できます。 詳細については、次を参照してください。[を使用して MDLs](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-mdls)します。

4.  設定を使用する I/O 要求チェーン MDLs 向け、URB の作成に、中に、 **TransferBufferMDL** 、関連付けられているメンバー [ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)構造 (など[ **\_URB\_一括\_OR\_INTERRUPT\_転送**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_bulk_or_interrupt_transfer)または[  **\_URB\_アイソクロナス\_転送**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_isoch_transfer)) にチェーン、およびセットの最初の MDL、 **TransferBufferLength**に転送するバイトの合計数。 データは、MDL チェーン内の 1 つ以上の MDL エントリにまたがる可能性があります。

    Windows 8 で 2 つの新しい種類の URB 関数が追加されましたデータ転送のチェーン MDLs を使用するクライアント ドライバーを有効にします。 この機能を使用する場合は、設定されていることを確認する、**関数**URB ヘッダーのメンバー URB 関数を次のいずれかに設定されます。

    -   URB\_関数\_一括\_または\_INTERRUPT\_転送\_USING\_連結された\_MDL
    -   URB\_関数\_アイソクロナス\_転送\_USING\_連結された\_MDL

    これらの URB 関数については、次を参照してください。 [  **\_URB\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_header)します。

<a name="remarks"></a>注釈
-------

ドライバー スタックが連鎖 MDLs を受け入れるかどうかを判断する基礎となる USB ドライバー スタックのクエリを実行するコード例では、次を参照してください。 [ **USBD\_QueryUsbCapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))します。

## <a name="related-topics"></a>関連トピック
[USB I/O 操作](usb-device-i-o.md)  



