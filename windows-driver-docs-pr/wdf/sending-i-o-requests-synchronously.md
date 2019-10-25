---
title: I/O 要求の同期送信
description: I/O 要求の同期送信
ms.assetid: e7e9f2d2-afc5-439b-8a04-72d117114fae
keywords:
- 一般的な i/o は、WDK KMDF をターゲットにし、i/o 要求をに送信します。
- i/o 要求の送信 (WDK KMDF)
- 送信 i/o 要求 WDK KMDF、同期
- i/o 要求を同期的に送信する WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e87d84e7adb4ed20f10c330eb5f1a8469b417dd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842194"
---
# <a name="sending-io-requests-synchronously"></a>I/O 要求の同期送信





次の表は、i/o ターゲットに対して i/o 要求を同期的に送信するためにドライバーが呼び出すことができる i/o ターゲットオブジェクトのメソッドを示しています。 これらのメソッドの使用方法の詳細については、メソッドのリファレンスページを参照してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メソッド</th>
<th align="left">目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously" data-raw-source="[&lt;strong&gt;WdfIoTargetSendReadSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously)"><strong>WdfIoTargetSendReadSynchronously</strong></a></p></td>
<td align="left"><p>読み取り要求を送信します</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendwritesynchronously" data-raw-source="[&lt;strong&gt;WdfIoTargetSendWriteSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendwritesynchronously)"><strong>WdfIoTargetSendWriteSynchronously</strong></a></p></td>
<td align="left"><p>書き込み要求を送信します</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously" data-raw-source="[&lt;strong&gt;WdfIoTargetSendIoctlSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously)"><strong>WdfIoTargetSendIoctlSynchronously</strong></a></p></td>
<td align="left"><p>デバイスコントロール要求を送信します</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlsynchronously" data-raw-source="[&lt;strong&gt;WdfIoTargetSendInternalIoctlSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlsynchronously)"><strong>Wdfiotargetsend、同期的に</strong></a></p></td>
<td align="left"><p>内部デバイスコントロール要求を送信します</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlotherssynchronously" data-raw-source="[&lt;strong&gt;WdfIoTargetSendInternalIoctlOthersSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlotherssynchronously)"><strong>WdfIoTargetSendInternalIoctlOthersSynchronously</strong></a></p></td>
<td align="left"><p>非標準の内部デバイスコントロール要求を送信します</p></td>
</tr>
</tbody>
</table>

 

また、 [**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を呼び出すことによって、要求を同期的に送信することもできますが、要求は、「 [I/o 要求を非同期に送信](sending-i-o-requests-asynchronously.md)する」で説明されている規則に従って最初に書式設定する必要があります。

I/o 要求を同期的に i/o ターゲットに送信することは、i/o 要求を[非同期](sending-i-o-requests-asynchronously.md)的に送信するよりも簡単にプログラムすることができます。 ただし、同期 i/o がドライバーに適しているかどうかを判断する際には、次のガイドラインを参考にしてください。

-   ドライバーが各 i/o 要求の完了を待機するために、ドライバーが大量の i/o 要求を送信しない場合や、システムまたはデバイスのパフォーマンスが低下しない場合は、同期 i/o を使用できます。

-   ドライバーが短時間に多数の i/o 要求を処理する必要がある場合、ドライバーが要求を完了するまで待機してから次の要求を送信することはできません。 そうしないと、ドライバーによってデータが失われたり、デバイス (場合によってはシステム全体) のパフォーマンスが低下したりする可能性があります。 このような場合、非同期 i/o の方が適している可能性があります。

-   同期 i/o は、追加の同時実行アクティビティなしで開始および終了する必要がある操作を処理する場合に便利です。 このような操作には、USB パイプのリセットや、デバイスレジスタの読み取りなどがあります。

-   ほとんどの場合、i/o 要求を同期的に送信するオブジェクトメソッドを呼び出すときに、ドライバーでタイムアウト値を指定する必要があります。 ドライバーでタイムアウト値が指定されておらず、デバイスまたは下位レベルのドライバーが応答しない場合は、ドライバーが停止する可能性があります。 その結果、ユーザーは応答していないアプリケーションを体験できます。 さらに、ドライバーがリリースしていない場合、他のドライバーが[作業項目](using-framework-work-items.md)などのシステムリソースを取得できない可能性があります。

-   スタックに含まれている以上のドライバーで操作を同期的に実行する必要がある場合、ドライバーは同期 i/o を使用する必要があります。 そのため、ドライバースタックに存在する可能性がある他のドライバーの要件について理解しておく必要があります。

次の例は、同期 i/o 制御 (IOCTL) 要求を送信する方法を示しています。

```cpp
NTSTATUS                status;
    WDF_MEMORY_DESCRIPTOR   inputDesc, outputDesc;
    PWDF_MEMORY_DESCRIPTOR  pInputDesc = NULL, pOutputDesc = NULL;
    ULONG_PTR               bytesReturned;

    UNREFERENCED_PARAMETER(FileObject);

    if (InputBuffer) {
        WDF_MEMORY_DESCRIPTOR_INIT_BUFFER(&inputDesc,
                                    InputBuffer,
                                    InputBufferLength);
        pInputDesc = &inputDesc;
    }

    if (OutputBuffer) {
        WDF_MEMORY_DESCRIPTOR_INIT_BUFFER(&outputDesc,
                                    OutputBuffer,
                                    OutputBufferLength);
        pOutputDesc = &outputDesc;
    }

    status = WdfIoTargetSendIoctlSynchronously(
                        IoTarget,
                        WDF_NO_HANDLE, // Request
                        IoctlControlCode,
                        pInputDesc,
                        pOutputDesc,
                        NULL, // PWDF_REQUEST_SEND_OPTIONS
                        &bytesReturned);
    if (!NT_SUCCESS(status)) {
         DEBUGP(MP_ERROR,
        ("WdfIoTargetSendIoctlSynchronously failed 0x%x\n",
          status));
    }

    *BytesReadOrWritten = (ULONG)bytesReturned;
```

 

 





