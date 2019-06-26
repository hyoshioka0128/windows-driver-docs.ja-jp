---
title: IOCTL_SPB_FULL_DUPLEX 要求の処理
description: SPI などのいくつかのバスは、読み取りを有効にし、書き込み、バス コント ローラーと、バス上のデバイス間で同時に発生する転送。
ms.assetid: B200461F-9F9C-43A7-BA78-0864FD58C64E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3c535226f6e57ad27718b01537ea4fd438ca0c9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385229"
---
# <a name="handling-ioctlspbfullduplex-requests"></a>処理の IOCTL\_SPB\_完全\_双方向の要求


SPI などのいくつかのバスは、読み取りを有効にし、書き込み、バス コント ローラーと、バス上のデバイス間で同時に発生する転送。 これらの全二重転送をサポートするために、シンプルな周辺機器バス (SPB) I/O 要求インターフェイスの定義が含まれている、オプションとして、 [ **IOCTL\_SPB\_完全\_双方向**](https://msdn.microsoft.com/library/windows/hardware/hh974774) I/O 制御コード (IOCTL)。 ハードウェアの全二重の転送を実装するバス コント ローラーの SPB コント ローラー ドライバーのみをサポートする必要があります、 **IOCTL\_SPB\_完全\_双方向**IOCTL します。

SPB コント ローラーのドライバーでは、全二重転送の I/O 要求をサポートする場合、ドライバーを使用する必要があります、 **IOCTL\_SPB\_完全\_双方向**これらの IOCTL を要求して、従う必要があります、このトピックで説明されている実装ガイドラインです。 次のガイドラインの目的は、サポートするすべてのハードウェア プラットフォーム間で一貫した動作を奨励する**IOCTL\_SPB\_完全\_双方向**要求。 周辺機器の SPB 接続用のドライバーはことができますし、それらを実行するどのようなプラットフォームに関係なく同じような結果を生成するためにこれらの要求に依存します。

## <a name="buffer-requirements"></a>バッファーの要件


[ **IOCTL\_SPB\_完全\_双方向**](https://msdn.microsoft.com/library/windows/hardware/hh974774)と同じ要求の形式が、 [ **IOCTL\_SPB\_EXECUTE\_シーケンス**](https://msdn.microsoft.com/library/windows/hardware/hh450857)要求が、これらの制約。

-   [ **SPB\_転送\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spb/ns-spb-spb_transfer_list)要求内の構造が正確に 2 つのエントリを含める必要があります。 最初のエントリには、デバイスに書き込むデータを格納しているバッファーがについて説明します。 2 番目のエントリには、デバイスから読み取られるデータを保持するために使用されるバッファーがについて説明します。
-   各[ **SPB\_転送\_一覧\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spb/ns-spb-spb_transfer_list_entry)転送リスト内の構造を指定する必要があります、 **DelayInUs**ゼロの値。

読み取りと書き込みの転送は、全二重転送中に同時に開始します。 データの書き込みの最初のバイトは、読み取りデータの最初のバイトとして同時に、バス経由で送信されます。

書き込みと読み取りバッファー、 **IOCTL\_SPB\_完全\_双方向**要求が同じ長さにする必要はありません。

読み取りバッファーが書き込みバッファーよりも短い場合は、書き込みバッファーの内容全体がデバイスに書き込まれるまで、全二重 bus 転送が続行されます。 読み取りバッファーがいっぱい後バス コント ローラーは、全二重 bus 転送が完了するまでに、デバイスから受信したすべての追加データを破棄します。

書き込みバッファーが読み取りバッファーよりも短い場合は、読み取りバッファーがいっぱいになるまで、全二重 bus 転送が続行されます。 書き込みバッファーの内容全体がデバイスに書き込まれると、バス コント ローラーは、全二重 bus 転送が完了するまで、デバイスにゼロを書き込みます。

場合、 **IOCTL\_SPB\_完全\_双方向**要求が正常に完了した SPB コント ローラーのドライバー セット、**状態**I/O 状態ブロックの状態のメンバー\_成功した場合、およびセット、**情報**合計バイト数へのメンバーは全二重転送中に (バイトの読み取りと書き込みバイト数) を転送します。 カウント値、**情報**メンバーは、読み取りバッファーのサイズと、書き込みバッファー サイズの合計を超えることはありません必要があります。

読み取りバッファーが書き込みバッファーよりも短い場合は、カウント値、**情報**メンバーを含めないでくださいバス コント ローラー、デバイスから読み取ります (と破棄) するデータのバイトの読み取り後にバッファーがいっぱいです。 たとえばが 1 バイトの書き込みバッファーと 4 バイトの全二重転送がバッファーが正常に完了を読み取る場合数の値を 5、いない 8 する必要があります。 同様に、書き込みバッファーが読み取りバッファーよりも短い場合は、数の値は書き込みバッファーが空になった後に、デバイスに書き込まれるゼロは含まれません。

## <a name="parameter-checking"></a>パラメーターのチェック


ただし、 [ **IOCTL\_SPB\_EXECUTE\_シーケンス**](https://msdn.microsoft.com/library/windows/hardware/hh450857)と**IOCTL\_SPB\_完全\_双方向**要求と同様の形式、SPB フレームワーク拡張機能 (SpbCx) によって異なる方法で処理されます。 **IOCTL\_SPB\_EXECUTE\_シーケンス**要求、SpbCx は、要求内のパラメーター値を検証し、要求の送信元のプロセスのコンテキストでは、要求のバッファーをキャプチャします。 SpbCx 渡します**IOCTL\_SPB\_EXECUTE\_シーケンス**SPB コント ローラーを使用してドライバー、ドライバーの要求[ *EvtSpbControllerIoSequence*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nc-spbcx-evt_spb_controller_sequence)コールバック関数は、これらの要求をささげます。

これに対し、SpbCx が扱われます、 **IOCTL\_SPB\_完全\_双方向**IOCTL、ドライバーの定義済みのカスタム要求として要求します。 SpbCx 渡します**IOCTL\_SPB\_完全\_双方向**SPB コント ローラーを使用してドライバー、ドライバーの要求[ *EvtSpbControllerIoOther*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nc-spbcx-evt_spb_controller_other)も、ドライバーがサポートする任意のカスタムの IOCTL 要求を処理するコールバック関数。 SpbCx には、これらの要求パラメーターをチェックまたはバッファーのキャプチャは行われません。 ドライバーは、パラメーターのチェック、または、IOCTL に必要なバッファーのキャプチャ要求を介して、ドライバーが受け取るその*EvtSpbControllerIoOther*関数。 バッファーのキャプチャを有効にするドライバーを指定する必要があります、 [ *EvtIoInCallerContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)コールバック関数、ドライバーの登録時にその*EvtSpbControllerIoOther*関数。 詳細については、次を参照してください。[を使用して、 **SPB\_転送\_一覧**カスタム Ioctl 構造](https://docs.microsoft.com/windows-hardware/drivers/spb/using-the-spb-transfer-list-structure)します。




通常、SPB コント ローラーのドライバーが内のパラメーター値を検証、 **IOCTL\_SPB\_完全\_双方向**で要求、 *EvtSpbControllerIoOther*関数ではなく、 *EvtIoInCallerContext*関数。 次のコード例では、ドライバーからパラメーターのチェックが実装する方法を示します。 この例では、ドライバーは、次のパラメーターの要件が満たされていることを確認します。

-   要求の転送の一覧には、正確に 2 つのエントリが含まれています。
-   転送リストの最初のエントリは、書き込みバッファーされ、2 つ目は、読み取りバッファー。
-   **DelayInUs**両方のエントリの値は 0 です。

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

上記のコード例ドライバー内部の呼び出しルーチンの名前付きパラメーターの値を確認するには後、 `MyDriverPerformFullDuplexTransfer`、全二重 I/O の転送を開始します。

 

 




