---
title: 全二重 I/O 要求
description: SPI などのいくつかのバスは、全二重バスの転送をサポートします。
ms.assetid: C80FE3F2-6659-4DE8-8F77-F77EDA60400F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66abe8a1222f15e8346de162c011836be2c753e9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373766"
---
# <a name="full-duplex-io-requests"></a>全二重 I/O 要求


SPI などのいくつかのバスは、全二重バスの転送をサポートします。 これらの転送では、同時にデータをデバイスに書き込むと、同じデバイスからデータを読み取るで I/O のパフォーマンスが向上します。 全二重バスの転送をサポートするために、[シンプルな周辺機器のバス](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))(SPB) [I/O 要求インターフェイス](https://docs.microsoft.com/previous-versions/hh698224(v=vs.85))定義、 [ **IOCTL\_SPB\_完全\_双方向**](https://msdn.microsoft.com/library/windows/hardware/hh974774) I/O 制御コード (IOCTL)。

サポート、 **IOCTL\_SPB\_完全\_双方向**IOCTL は省略可能です。 のみ[SPB コント ローラー ドライバー](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-controller-drivers)バスのハードウェアに全二重の転送を実装するコント ローラーがこの IOCTL をサポートします。 このドライバーはすべて失敗 SPB のコント ローラー ドライバーが全二重の転送をサポートしていない場合**IOCTL\_SPB\_完全\_双方向**要求を受信およびエラーの状態コードの完了ステータス\_いない\_サポートされています。

## <a name="transfer-list"></a>一覧を転送します。


形式、 **IOCTL\_SPB\_完全\_双方向**要求は、に似ていますが、 [ **IOCTL\_SPB\_EXECUTE\_シーケンス**](https://msdn.microsoft.com/library/windows/hardware/hh450857)要求。 両方の要求を使用して、 [ **SPB\_転送\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spb/ns-spb-spb_transfer_list)読み取りの一覧を記述して、書き込み要求の転送に構造体。 転送の一覧、 **IOCTL\_SPB\_EXECUTE\_シーケンス**要求は、任意の組み合わせのバッファーの読み取りおよび書き込みバッファーを持つことができます。 これに対しの一覧で、転送、 **IOCTL\_SPB\_完全\_双方向**要求が正確に 1 つの読み取りバッファーと 1 つの書き込みバッファーが常に必要です。 書き込みバッファーは転送の一覧で最初のバッファーでは常に、読み取りバッファーが 2 つ目。

に対する追加の要件、 **IOCTL\_SPB\_完全\_双方向**要求は、 **DelayInUs**メンバーがゼロで常にあります、 [ **SPB\_転送\_一覧\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spb/ns-spb-spb_transfer_list_entry)読み取りバッファーおよび書き込みバッファーを記述する構造体。

次のコード例は、SPB 周辺機器のデバイスのドライバーが転送のリストを構築する方法を示しています、 **IOCTL\_SPB\_完全\_双方向**要求。

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

上記のコード例では、 [ **SPB\_転送\_一覧\_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spb/nf-spb-spb_transfer_list_init)と[ **SPB\_転送\_リスト\_エントリ\_INIT\_単純**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spb/nf-spb-spb_transfer_list_entry_init_simple)ヘッダーとエントリ、転送を初期化するために関数が一覧表示します。 **SPB\_転送\_一覧\_AND\_エントリ**Spb.h ヘッダー ファイルで定義されているマクロは、転送リストの宣言を簡略化します。 このマクロを定義、`seq`変数を格納する構造体、 **SPB\_転送\_一覧**構造と**SPB\_転送\_ボックスの一覧\_エントリ**2 つの要素の配列。

## <a name="full-duplex-bus-transfers"></a>全二重 Bus 転送


応答、 **IOCTL\_SPB\_完全\_双方向**SPB 周辺機器のデバイス ドライバーの場合からの要求 SPB コント ローラーのドライバー、バス上の全二重転送を開始します。 書き込みバッファーの最初のバイトは、デバイスから、読み取りバッファーの最初のバイトを読み取るをバス クロックのと同じティックでデバイスに書き込まれます。

読み取りバッファーの書き込みバッファーを使用して、 **IOCTL\_SPB\_完全\_双方向**要求が同じ長さにする必要はありません。 書き込みバッファーが読み取りバッファーよりも小さい場合は、デバイスに書き込みバッファーの内容を書き込むバッファーは空になりますが、読み取りバッファーがいっぱいになるまでには引き続き SPB コント ローラーのドライバーを停止します。 同様に、読み取りバッファーが書き込みバッファーよりも小さい場合は、読み取りバッファーがいっぱいでは、バッファーが空にするまで、書き込みバッファーの内容をデバイスに書き込みが続行されます後の情報を入力、SPB コント ローラー用ドライバーを停止します。

## <a name="example-kmdf-driver"></a>以下に例を示します。KMDF ドライバー


SPB の周辺機器のカーネル モード ドライバー Foundation (KMDF) ドライバーなどのメソッドの呼び出し[ **WdfIoTargetSendIoctlSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously) SPB コント ローラーに IOCTL 要求を送信します。 このメソッドは*InputBuffer*と*OutputBuffer*パラメーター。 一部の種類のデバイス ドライバーは、これら 2 つのパラメーターを使用して、IOCTL 要求のそれぞれに、書き込みバッファーや読み取りバッファーを指定する場合があります。 ただし、SPB コント ローラーに IOCTL 要求を送信する SPB の周辺機器のデバイス ドライバ設定、 *InputBuffer*パラメーターが指すメモリ記述子を**SPB\_転送\_リスト**構造体。 構造体が、書き込みバッファーと (この順序で) で読み取りバッファーの両方を記述するなど、 **IOCTL\_SPB\_完全\_双方向**要求。 ドライバーのセット、 *OutputBuffer*パラメーターを NULL にします。

次のコード例は、 **WdfIoTargetSendIoctlSynchronously**送信呼び出しを**IOCTL\_SPB\_完全\_双方向**SPB の周辺機器への要求デバイスです。 `seq`この例では変数でのコード例で定義されている転送リスト[転送リスト](#transfer-list)します。

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

上記のコード例で、`MemoryDescriptor`変数は、framework のメモリの記述子。 [ **WDF\_メモリ\_記述子\_INIT\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_buffer)マクロが、構造のコンテナーとして機能するには、この記述子を初期化します含まれている、`seq`変数。 呼び出しで、 **WdfIoTargetSendIoctlSynchronously**メソッド、`SpbIoTarget`変数は、バス上のターゲットの周辺機器への前に開かれたハンドル。 *InputBuffer*このメソッドのパラメーターは、メモリ記述子へのポインター。 *OutputBuffer*パラメーターが NULL です。

**WdfIoTargetSendIoctlSynchronously**でこれを呼び出して設定するコード例、 `BytesTransferred` (書き込まれたバイト数と読み取られたバイト) に転送された合計バイト数を変数。 たとえば、要求が 1 バイトの書き込みバッファーと、4 バイトの読み取りバッファーと、呼び出しは成功しますが、 `BytesTransferred` 5 を指定する必要があります。

## <a name="example-umdf-driver"></a>以下に例を示します。UMDF ドライバー


SPB の周辺機器デバイスのユーザー モード ドライバー Foundation (UMDF) ドライバーなどのメソッドの呼び出し[ **IWDFIoTarget::FormatRequestForIoctl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl) I/O 制御操作の I/O 要求の書式を設定します。 このメソッドは*pInputMemory*と*pOutputMemory*パラメーター。 一部の種類のデバイス ドライバーは、これら 2 つのパラメーターを使用して、読み取りバッファーと IOCTL 要求の書き込みバッファーを指す可能性があります。 ただし、SPB コント ローラーに IOCTL 要求を送信する SPB の周辺機器のデバイス ドライバ設定、 *pInputMemory*パラメーターを格納しているメモリ オブジェクトを指す、 **SPB\_転送\_一覧**構造体。 構造体が、書き込みバッファーとの読み取りバッファーの両方を記述するなど、 **IOCTL\_SPB\_完全\_双方向**要求。 ドライバーのセット、 *pOutputMemory*パラメーターを NULL にします。

次のコード例に示す、 **IWDFIoTarget::FormatRequestForIoctl**形式を呼び出し、 **IOCTL\_SPB\_完全\_双方向**SPB への要求周辺機器です。 `seq`この例では変数でのコード例で定義されている転送リスト[転送リスト](#transfer-list)します。

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

上記のコード例では、次のオブジェクト ポインターを使用します。

-   `pWdfMemory`変数は、framework の以前に割り当てられたメモリへのポインター ([**IWDFMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory)) オブジェクト。 周辺機器のデバイス ドライバーで転送リスト用のコンテナーとしてこのオブジェクトを使用して、`seq`変数。
-   `pWdfRemoteTarget`パラメーターは、以前に開かれてリモート I/O ターゲットへのポインター ([**IWDFRemoteTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfremotetarget)) オブジェクト。 このオブジェクトは、周辺機器のデバイスへの周辺機器のデバイス ドライバーの接続を表します。
-   `pWdfIoRequest`変数が以前に作成したフレームワーク要求へのポインター ([**IWDFIoRequest2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiorequest2)) オブジェクト。 周辺機器のデバイス ドライバーのコンテナーとしてこのオブジェクトを使用して、 **IOCTL\_SPB\_完全\_双方向**要求。

上記のコード例は、次のこと。

1.  呼び出し、 [ **IWDFMemory::SetBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfmemory-setbuffer)メソッドによって示されるメモリ オブジェクトを再利用`pWdfMemory`転送リストのコンテナーとして機能します。
2.  **FormatRequestForIoctl**呼び出しによって示される要求オブジェクトを再利用`pWdfIoRequest`のコンテナーとして機能する、 **IOCTL\_SPB\_完全\_双方向**要求。 *PInputMemory*このメソッドにパラメーターが転送リストを格納しているメモリ オブジェクトへのポインター。 *POutputMemory*パラメーターが NULL です。
3.  呼び出し、 [ **IWDFIoRequest::Send** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)メソッドは、デバイスに、I/O 要求を送信します。 この呼び出しは同期的にし、SPB のコント ローラー ドライバーが、要求を完了した後を返します。
4.  呼び出し、 [ **IWDFIoRequest::GetCompletionParams** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getcompletionparams)メソッド要求の完了パラメーターを取得します。
5.  呼び出し、 [ **IWDFRequestCompletionParams::GetInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfrequestcompletionparams-getinformation)メソッドの取得、*情報*完了パラメーターからの値 (、 **情報**状態の I/O ブロック フィールド)。 この値は (書き込まれたバイト数と読み取られたバイト) に転送されたバイトの合計数は、 **IOCTL\_SPB\_完全\_双方向**要求。

 

 




