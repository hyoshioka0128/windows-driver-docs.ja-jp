---
title: IOCTL_SPB_FULL_DUPLEX 要求の処理
description: SPI などの一部のバスでは、バスコントローラーとバス上のデバイスの間で同時に読み取りと書き込みの転送を行うことができます。
ms.assetid: B200461F-9F9C-43A7-BA78-0864FD58C64E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50d22ffe83193f03c36d258383ef8fd00b17d7fe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843370"
---
# <a name="handling-ioctl_spb_full_duplex-requests"></a>完全\_双方向要求\_IOCTL\_SPB の処理


SPI などの一部のバスでは、バスコントローラーとバス上のデバイスの間で同時に読み取りと書き込みの転送を行うことができます。 これらの全二重転送をサポートするために、シンプルな周辺機器バス (SPB) i/o 要求インターフェイスの定義には、 [**ioctl\_SPB\_完全\_双**](https://msdn.microsoft.com/library/windows/hardware/hh974774)方向 i/o 制御コード (ioctl) が含まれます。 ハードウェアで全二重転送を実装するバスコントローラー用の SPB コントローラードライバーのみが、 **ioctl\_SPB\_完全\_双方向**ioctl をサポートする必要があります。

SPB コントローラードライバーで、全二重転送の i/o 要求がサポートされている場合、ドライバーは、これらの要求に対して**完全\_二重 ioctl\_ioctl\_SPB**を使用する必要があります。また、「」に記載されている実装ガイドラインに従う必要があります。このトピックを参照してください。 これらのガイドラインの目的は、すべてのハードウェアプラットフォームにおいて、**完全\_双方向の要求\_IOCTL\_SPB**をサポートするような、一貫した動作を奨励することです。 SPB が接続されている周辺機器のドライバーは、これらの要求に依存して、実行されているプラットフォームに関係なく同様の結果を生成することができます。

## <a name="buffer-requirements"></a>バッファー要件


[**完全\_双方向要求\_ioctl\_spb**](https://msdn.microsoft.com/library/windows/hardware/hh974774)は、 [ **\_シーケンス**](https://msdn.microsoft.com/library/windows/hardware/hh450857)要求を実行するのと\_同じような形式になりますが、次の制約があります。\_

-   要求の[**SPB\_TRANSFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spb/ns-spb-spb_transfer_list)構造体には、2つのエントリが含まれている必要があります。 最初のエントリは、デバイスに書き込むデータを格納するバッファーを表します。 2番目のエントリは、デバイスから読み取られたデータを保持するために使用されるバッファーを表します。
-   転送リスト内の各[**SPB\_transfer\_list\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spb/ns-spb-spb_transfer_list_entry)構造には、 **delayinus**値0を指定する必要があります。

全二重転送中は、読み取りと書き込みの転送が連携して開始されます。 書き込みデータの最初のバイトは、読み取りデータの最初のバイトと同時にバスを介して送信されます。

IOCTL\_SPB の書き込みバッファーと読み取りバッファー **\_完全\_双方向**要求の長さは同じである必要はありません。

読み取りバッファーが書き込みバッファーより短い場合、完全な双方向バス転送は、書き込みバッファーの内容全体がデバイスに書き込まれるまで続行されます。 読み取りバッファーがいっぱいになると、完全な双方向バス転送が完了するまで、デバイスから受信したすべての追加データがバスコントローラーによって破棄されます。

書き込みバッファーが読み取りバッファーより短い場合、全二重バス転送は読み取りバッファーがいっぱいになるまで続行されます。 書き込みバッファーの内容全体がデバイスに書き込まれると、バスコントローラーは、完全な双方向バス転送が完了するまで、デバイスにゼロを書き込みます。

**完全\_双方向要求\_IOCTL\_spb**が正常に完了した場合、spb コントローラードライバーは i/o 状態ブロックの**状態**メンバーを "成功"\_"状態" に設定し、**情報**メンバーを全二重転送中に転送された合計バイト数 (読み取りバイト数と書き込みバイト数)。 **情報**メンバーの count 値は、読み取りバッファーサイズと書き込みバッファーサイズの合計を超えることはできません。

読み取りバッファーが書き込みバッファーより短い場合、**情報**メンバーの count 値には、バスコントローラーがデバイスから読み取るデータのバイト数 (および、読み取りバッファーがいっぱいになった後に破棄される) を含めないでください。 たとえば、1バイトの書き込みバッファーと4バイトの読み取りバッファーを使用した全二重転送が正常に完了した場合、カウント値は8ではなく5になります。 同様に、書き込みバッファーが読み取りバッファーより短い場合、書き込みバッファーが空になった後にデバイスに書き込まれたゼロをカウント値に含めることはできません。

## <a name="parameter-checking"></a>パラメーターチェック


[**Ioctl\_spb は\_シーケンス**](https://msdn.microsoft.com/library/windows/hardware/hh450857)および IOCTL\_SPB を実行\_ますが、**完全\_双**方向の要求の形式は同じですが、Spb フレームワーク拡張 (spbcx) によって処理されます。\_ **IOCTL\_SPB**の場合は\_シーケンス要求を実行\_、SpbCx は要求のパラメーター値を検証し、要求の発信元のプロセスコンテキストで要求のバッファーをキャプチャします。 SpbCx は、これらの要求専用のドライバーの[*EvtSpbControllerIoSequence*](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_sequence) callback 関数を介して、spb コントローラードライバーに **\_シーケンス要求を実行\_、IOCTL\_spb**に渡します。

これに対し、SpbCx では、 **ioctl\_SPB\_完全\_双方向**要求が、ドライバーで定義されたカスタム ioctl 要求として扱われます。 SpbCx は、ドライバーの EvtSpbControllerIoOther callback 関数によって、ドライバーがサポートしているすべてのカスタム IOCTL 要求を処理し、ドライバーの[](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_other)コールバック関数を介して、spb コントローラードライバーへの**完全\_双方向要求\_、IOCTL\_spb**に渡します。 SpbCx は、これらの要求に対してパラメーターチェックもバッファーキャプチャも行いません。 ドライバーは、ドライバーが*EvtSpbControllerIoOther*関数を通じて受信する IOCTL 要求で必要になる可能性があるパラメーターチェックまたはバッファーキャプチャを行います。 バッファーキャプチャを有効にするには、ドライバーが*EvtSpbControllerIoOther*関数を登録するときに、ドライバーが[*Evtioincallercontext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)コールバック関数を提供する必要があります。 詳細については、「 [ **SPB\_TRANSFER\_** カスタム ioctl のリスト構造を使用する](https://docs.microsoft.com/windows-hardware/drivers/spb/using-the-spb-transfer-list-structure)」を参照してください。




通常、SPB コントローラードライバーは、 *Evtioincallercontext*関数ではなく、 *EvtSpbControllerIoOther*関数で、 **IOCTL\_SPB\_完全\_双方向**要求のパラメーター値を検証します。 次のコード例は、ドライバーがパラメーターチェックを実装する方法を示しています。 この例では、ドライバーは次のパラメーター要件が満たされていることを確認します。

-   要求の転送リストには、2つのエントリが含まれています。
-   転送リストの最初のエントリは書き込みバッファー用で、もう1つは読み取りバッファー用です。
-   両方のエントリの**Delayinus**値が0です。

```cpp
//
// Validate the transfer count.
//

SPB_REQUEST_PARAMETERS params;
SPB_REQUEST_PARAMETERS_INIT(&params);
SpbRequestGetParameters(SpbRequest, &params);

if (params.SequenceTransferCount != 2)
{
    //
    // The full-duplex request must have 
    // exactly two transfer descriptors.
    //
    
    status = STATUS_INVALID_PARAMETER;        
    goto exit;
}

//
// Retrieve the write and read transfer descriptors.
//

const ULONG fullDuplexWriteIndex = 0;
const ULONG fullDuplexReadIndex = 1;

SPB_TRANSFER_DESCRIPTOR writeDescriptor;
SPB_TRANSFER_DESCRIPTOR readDescriptor;
PMDL pWriteMdl;
PMDL pReadMdl;

SPB_TRANSFER_DESCRIPTOR_INIT(&writeDescriptor);
SPB_TRANSFER_DESCRIPTOR_INIT(&readDescriptor);

SpbRequestGetTransferParameters(
    SpbRequest, 
    fullDuplexWriteIndex, 
    &writeDescriptor,
    &pWriteMdl);

SpbRequestGetTransferParameters(
    SpbRequest, 
    fullDuplexReadIndex, 
    &readDescriptor,
    &pReadMdl);
    
//
// Validate the transfer direction of each descriptor.
//

if ((writeDescriptor.Direction != SpbTransferDirectionToDevice) ||
    (readDescriptor.Direction != SpbTransferDirectionFromDevice))
{
    //
    // For full-duplex I/O, the direction of the first transfer
    // must be SpbTransferDirectionToDevice, and the direction
    // of the second must be SpbTransferDirectionFromDevice.
    //
    
    status = STATUS_INVALID_PARAMETER;
    goto exit;
}

//
// Validate the delay for each transfer descriptor.
//

if ((writeDescriptor.DelayInUs != 0) || (readDescriptor.DelayInUs != 0))
{
    //
    // The write and read buffers for full-duplex I/O are transferred
    // simultaneously over the bus. The delay parameter in each transfer
    // descriptor must be set to 0.
    //
    
    status = STATUS_INVALID_PARAMETER;
    goto exit;
}

MyDriverPerformFullDuplexTransfer(
    pDevice, 
    pRequest,
    writeDescriptor,
    pWriteMdl,
    readDescriptor,
    pReadMdl);
```

パラメーター値を確認した後、上記のコード例では、`MyDriverPerformFullDuplexTransfer`という名前のドライバー内部ルーチンを呼び出して、全二重の i/o 転送を開始します。

 

 




