---
title: 全二重 I/O 要求
description: SPI などの一部のバスでは、全二重バス転送がサポートされています。
ms.assetid: C80FE3F2-6659-4DE8-8F77-F77EDA60400F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c6c9054a0fc18acc01cbeaa842220f10d64d392
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826169"
---
# <a name="full-duplex-io-requests"></a>全二重 I/O 要求


SPI などの一部のバスでは、全二重バス転送がサポートされています。 これらの転送により、デバイスにデータを同時に書き込み、同じデバイスからデータを読み取ることで、i/o のパフォーマンスが向上します。 全二重のバス転送をサポートするために、[シンプルな周辺機器バス](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))(Spb) [i/o 要求インターフェイス](https://docs.microsoft.com/previous-versions/hh698224(v=vs.85))では、完全\_双方向 I/O 制御コード (Ioctl) [ **\_、ioctl\_SPB**](https://msdn.microsoft.com/library/windows/hardware/hh974774)が定義されています。

**Ioctl\_SPB\_完全\_二重**ioctl のサポートはオプションです。 ハードウェアでの全二重転送を実装するバスコントローラー用の[SPB コントローラードライバー](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-controller-drivers)のみが、この IOCTL をサポートしています。 SPB コントローラードライバーが全二重転送をサポートしていない場合、このドライバーはすべての**IOCTL\_SPB\_完全\_双**方向の要求を受信し、エラー状態コードの状態では\_なく、エラー状態コードの\_状態で完了します。さ.

## <a name="transfer-list"></a>転送リスト


**Ioctl\_spb\_完全\_双**方向要求の形式は、 [ **\_シーケンス要求の実行\_ioctl\_SPB**](https://msdn.microsoft.com/library/windows/hardware/hh450857)の形式に似ています。 どちらの要求でも、 [**SPB\_転送\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spb/ns-spb-spb_transfer_list)構造を使用して、要求の読み取りおよび書き込み転送の一覧を記述します。 **\_シーケンス要求を実行\_IOCTL\_SPB**の転送リストには、読み取りバッファーと書き込みバッファーの任意の組み合わせを含めることができます。 これに対して、 **IOCTL\_SPB\_完全\_双**方向要求の転送リストには、常に1つの読み取りバッファーと1つの書き込みバッファーが必要です。 書き込みバッファーは常に転送リストの最初のバッファーで、読み取りバッファーは2番目のバッファーです。

**IOCTL\_spb\_完全\_双**方向要求の追加の要件としては、\_の\_を記述した[**エントリ構造\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/spb/ns-spb-spb_transfer_list_entry)で、 **delayinus**メンバーが常に0である必要があります。読み取りバッファーと書き込みバッファー。

次のコード例では、SPB 周辺機器のドライバーが、 **IOCTL\_spb\_完全\_双方向**要求の転送リストを構築する方法を示します。

```cpp
const ULONG transfers = 2;

SPB_TRANSFER_LIST_AND_ENTRIES(transfers) seq;
SPB_TRANSFER_LIST_INIT(&(seq.List), transfers);

{
    ULONG index = 0;
    seq.List.Transfers[index] = SPB_TRANSFER_LIST_ENTRY_INIT_SIMPLE(
        SpbTransferDirectionToDevice,
        0,
        pWriteBuffer,
        writeBufferLength);

    seq.List.Transfers[index + 1] = SPB_TRANSFER_LIST_ENTRY_INIT_SIMPLE(
        SpbTransferDirectionFromDevice,
        0,
        pReadBuffer,
        readBufferLength);
}
```

前のコード例では、 [**SPB\_transfer\_list\_init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spb/nf-spb-spb_transfer_list_init)および\_spb を使用して\_[**list\_ENTRY\_init\_単純な**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spb/nf-spb-spb_transfer_list_entry_init_simple)関数を転送し、転送リストヘッダーを初期化し、entries. Spb. h ヘッダーファイルで定義されている **\_LIST\_および\_ENTRIES マクロの\_転送**は、転送リストの宣言を簡略化します。 このマクロは、`seq` 変数を定義します。この構造体は、 **sp 1\_transfer\_list**構造体\_と、2つの要素の**エントリ配列\_一覧の転送\_リスト**に格納されます。

## <a name="full-duplex-bus-transfers"></a>全二重バス転送


Spb の周辺機器ドライバーからの**完全\_双方向要求\_IOCTL\_spb**に応答して、spb コントローラードライバーはバス上で全二重転送を開始します。 書き込みバッファーの最初のバイトは、読み取りバッファーの最初のバイトがデバイスから読み取られるバスクロックの同じ目盛りでデバイスに書き込まれます。

**完全\_双方向要求\_IOCTL\_SPB**の読み取りバッファーと書き込みバッファーは、同じ長さである必要はありません。 書き込みバッファーが読み取りバッファーより小さい場合、SPB コントローラードライバーはバッファーが空になった後も書き込みバッファーの内容の書き込みを停止しますが、バッファーがいっぱいになるまでは読み取りバッファーにデータを格納し続けます。 同様に、読み取りバッファーが書き込みバッファーよりも小さい場合、SPB コントローラードライバーは、読み取りバッファーがいっぱいになった後も書き込みバッファーの内容の書き込みを停止しますが、バッファーが空になるまでは書き込みバッファーの内容をデバイスに書き込み続けます。

## <a name="example-kmdf-driver"></a>例: KMDF ドライバー


SPB 周辺機器のカーネルモードドライバー基盤 (KMDF) ドライバーは、 [**Wdfiotargetsendioctlsynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously)のメソッドを同期的に呼び出して、IOCTL 要求を spb コントローラーに送信します。 このメソッドには、 *InputBuffer*パラメーターと*outputbuffer*パラメーターがあります。 一部の種類のデバイスのドライバーでは、これら2つのパラメーターを使用して、IOCTL 要求の書き込みバッファーと読み取りバッファーをポイントすることがあります。 ただし、IOCTL 要求を SPB コントローラーに送信するために、SPB 周辺機器ドライバーは、 *InputBuffer*パラメーターを設定して、 **spb\_転送\_リスト**構造を指すメモリ記述子をポイントします。 たとえば、この構造体は、 **IOCTL\_SPB\_完全\_双方向**要求に対する書き込みバッファーと読み取りバッファーの両方を記述します (この順序で)。 ドライバーは*Outputbuffer*パラメーターを NULL に設定します。

次のコード例は、i/o **\_spb\_完全\_双**方向の要求を spb 周辺機器に送信する**Wdfiotargetsendioctlsynchronously**呼び出しを示しています。 この例の `seq` 変数は、[転送](#transfer-list)リストのコード例で定義されている転送リストです。

```cpp
ULONG_PTR BytesTransferred = 0;
NTSTATUS Status;
  
WDF_MEMORY_DESCRIPTOR MemoryDescriptor;
WDF_MEMORY_DESCRIPTOR_INIT_BUFFER(
                            &MemoryDescriptor,  
                            &seq,  
                            sizeof(seq));

Status = WdfIoTargetSendIoctlSynchronously(
                            SpbIoTarget,
                            NULL,
                            IOCTL_SPB_FULL_DUPLEX,
                            &MemoryDescriptor,  // InputBuffer
                            NULL,               // OutputBuffer
                            NULL,
                            &BytesTransferred);
```

前のコード例では、`MemoryDescriptor` 変数はフレームワークメモリ記述子です。 [**WDF\_MEMORY\_descriptor\_INIT\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_buffer)マクロは、この記述子を初期化して、`seq` 変数に格納されている構造体のコンテナーとして機能します。 **Wdfiotargetsendioctlsynchronously**メソッドの呼び出しでは、`SpbIoTarget` 変数は、バス上のターゲット周辺機器への以前に開かれたハンドルです。 このメソッドの*InputBuffer*パラメーターは、メモリ記述子へのポインターです。 *Outputbuffer*パラメーターが NULL です。

このコード例では、 **Wdfiotargetsendioctlsynchronously**呼び出しによって、`BytesTransferred` 変数が、転送されたバイト数の合計 (書き込みバイト数 + 読み取りバイト数) に設定されます。 たとえば、要求に1バイトの書き込みバッファーと4バイトの読み取りバッファーがあり、呼び出しが成功した場合、`BytesTransferred` 値は5になります。

## <a name="example-umdf-driver"></a>例: UMDF ドライバー


SPB 周辺機器のユーザーモードドライバー基盤 (UMDF) ドライバーは、 [**Iwdfiotarget:: FormatRequestForIoctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl)などのメソッドを呼び出して、i/o 制御操作の i/o 要求をフォーマットします。 このメソッドには、 *Pinputmemory*パラメーターと*poutputmemory*パラメーターがあります。 一部の種類のデバイスのドライバーでは、これら2つのパラメーターを使用して、読み取りバッファーと IOCTL 要求の書き込みバッファーをポイントする場合があります。 ただし、spb コントローラーに IOCTL 要求を送信するために、SPB 周辺機器ドライバーは、 *Pinputmemory*パラメーターを、 **spb\_TRANSFER\_LIST**構造体を含むメモリオブジェクトを指すように設定します。 たとえば、この構造体は、IOCTL\_SPB の書き込みバッファーと読み取りバッファーの両方 **\_完全\_双方向**要求に記述します。 ドライバーは*Poutputmemory*パラメーターを NULL に設定します。

次のコード例は、 **Iwdfiotarget:: FormatRequestForIoctl**呼び出しを示しています。この呼び出しでは、 **IOCTL\_spb\_完全\_双**方向の要求を、spb 周辺機器に設定します。 この例の `seq` 変数は、[転送](#transfer-list)リストのコード例で定義されている転送リストです。

```cpp
ULONG_PTR BytesTransferred = 0;
HRESULT hr;

pWdfMemory->SetBuffer(seq, sizeof(seq));

hr = pWdfRemoteTarget->FormatRequestForIoctl( 
                         pWdfIoRequest,
                         IOCTL_SPB_FULL_DUPLEX,
                         NULL,
                         pWdfMemory,  // pInputMemory
                         NULL,        // pOutputMemory 
                         NULL,
                         NULL);

if (FAILED(hr))
{
    goto exit;
}

hr = pWdfIoRequest->Send(pRemoteTarget,
                         WDF_REQUEST_SEND_OPTION_SYNCHRONOUS,
                         0);

if (FAILED(hr))
{
    goto exit;
}

{
    IWDFRequestCompletionParams* pWdfParams = 0;

    pWdfIoRequest->GetCompletionParams(&pWdfParams);
    hr = pWdfParams->GetCompletionStatus();
    if (SUCCEEDED(hr))
    {
        BytesTransferred = pWdfParams->GetInformation();
    }
    SAFE_RELEASE(pWdfParams);
}
```

前のコード例では、次のオブジェクトポインターを使用しています。

-   `pWdfMemory` 変数は、以前に割り当てられたフレームワークメモリ ([**Iwdfmemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfmemory)) オブジェクトへのポインターです。 周辺機器ドライバーは、このオブジェクトを `seq` 変数の転送リストのコンテナーとして使用します。
-   `pWdfRemoteTarget` パラメーターは、既に開かれているリモート i/o ターゲット ([**Iwdfremotetarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfremotetarget)) オブジェクトへのポインターです。 このオブジェクトは、周辺機器ドライバーが周辺機器に接続していることを表します。
-   `pWdfIoRequest` 変数は、以前に作成されたフレームワーク要求 ([**IWDFIoRequest2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest2)) オブジェクトへのポインターです。 周辺機器ドライバーは、このオブジェクトを IOCTL\_SPB のコンテナーとして使用し **\_完全\_双**方向の要求を行います。

上記のコード例では、次のことを行います。

1.  [**Iwdfmemory:: SetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfmemory-setbuffer)メソッドを呼び出すと、`pWdfMemory` が指すメモリオブジェクトが再利用され、転送リストのコンテナーとして機能します。
2.  **Formatrequestforioctl**呼び出しは、`pWdfIoRequest` が指す要求オブジェクトを再利用し、 **IOCTL\_SPB\_完全\_双**方向要求のコンテナーとして機能します。 このメソッドの*Pinputmemory*パラメーターは、転送リストを含むメモリオブジェクトへのポインターです。 *Poutputmemory*パラメーターが NULL です。
3.  [**IWDFIoRequest:: Send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)メソッドを呼び出すと、i/o 要求がデバイスに送信されます。 この呼び出しは同期的であり、SPB コントローラードライバーが要求を完了した後に戻ります。
4.  [**IWDFIoRequest:: Getcompletion params**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getcompletionparams)メソッドの呼び出しでは、要求から完了パラメーターを取得します。
5.  [**Iwdfrequestcompletion params:: GetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfrequestcompletionparams-getinformation)メソッドを呼び出すと、完了パラメーター (i/o 状態ブロックの**情報**フィールド) から*情報*値が取得されます。 この値は、 **IOCTL\_SPB\_完全\_双**方向要求によって転送されたバイト数の合計 (書き込みバイト数 + 読み取りバイト数) です。

 

 




