---
title: I/O 要求の同期送信
description: I/O 要求の同期送信
ms.assetid: e7e9f2d2-afc5-439b-8a04-72d117114fae
keywords:
- 一般的な I/O ターゲット WDK KMDF への I/O 要求を送信します。
- WDK KMDF を要求する I/O を送信します。
- 送信 I/O WDK KMDF、同期を要求します。
- WDK KMDF の I/O 要求を同期的に送信します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c2df1beb7b971cea9ca326e29c1d9afb2f632df
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325144"
---
# <a name="sending-io-requests-synchronously"></a>I/O 要求の同期送信





次の表では、I/O のターゲットに同期的に I/O 要求を送信するには、ドライバーを呼び出すことができる I/O ターゲット オブジェクトのメソッドを示します。 これらのメソッドを使用する方法の詳細については、メソッドのリファレンス ページを参照してください。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548669" data-raw-source="[&lt;strong&gt;WdfIoTargetSendReadSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548669)"><strong>WdfIoTargetSendReadSynchronously</strong></a></p></td>
<td align="left"><p>読み取り要求を送信します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548672" data-raw-source="[&lt;strong&gt;WdfIoTargetSendWriteSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548672)"><strong>WdfIoTargetSendWriteSynchronously</strong></a></p></td>
<td align="left"><p>書き込み要求を送信します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548660" data-raw-source="[&lt;strong&gt;WdfIoTargetSendIoctlSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548660)"><strong>WdfIoTargetSendIoctlSynchronously</strong></a></p></td>
<td align="left"><p>デバイスの制御要求を送信します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548656" data-raw-source="[&lt;strong&gt;WdfIoTargetSendInternalIoctlSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548656)"><strong>WdfIoTargetSendInternalIoctlSynchronously</strong></a></p></td>
<td align="left"><p>内部デバイス制御の要求を送信します</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548651" data-raw-source="[&lt;strong&gt;WdfIoTargetSendInternalIoctlOthersSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548651)"><strong>WdfIoTargetSendInternalIoctlOthersSynchronously</strong></a></p></td>
<td align="left"><p>非標準の内部デバイス制御要求を送信します。</p></td>
</tr>
</tbody>
</table>

 

同期的には呼び出すことによっても要求を送信することができます[ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)、要求を最初に説明されている規則に従って書式設定する必要しますが、 [I/O 要求の送信非同期的に](sending-i-o-requests-asynchronously.md)します。

I/O 要求を送信するよりも簡単にプログラムが同期的に I/O のターゲットに I/O 要求を送信する[非同期的に](sending-i-o-requests-asynchronously.md)します。 ただし、同期 I/O は、ドライバーの適切なかどうかを判断するのに役立つ、次のガイドラインを使用する必要があります。

-   ドライバーは多くの I/O 要求を送信しない場合は、同期 I/O を使用することができ、各 I/O 要求が完了するのには、ドライバーが待機するため、システムまたはデバイスのパフォーマンスが減らない場合。

-   ドライバーする必要があります多くの I/O 要求短い期間を処理する場合は、ドライバー、次の要求を送信する前に完了するには、各要求を待機する可能性があります許可できません。 それ以外の場合、ドライバーはデータが失われるまたはそのデバイス (および、場合によっては、システム全体) のパフォーマンスが低下する可能性があります。 このような場合は、非同期 I/O には優れた選択肢可能性があります。

-   同期 I/O は、操作を開始し、同時アクティビティを追加せずに終了する必要がありますを処理するために役立ちます。 このような操作は、USB パイプをリセットするか、デバイス登録の読み取りなどがあります。

-   ほとんどの場合、同期的に、I/O 要求を送信するオブジェクトのメソッドを呼び出すときに、ドライバーでタイムアウト値を指定する必要があります。 ドライバーが、タイムアウト値を指定しない場合、デバイスの場合、下位レベルのドライバーが応答できないには、ドライバーが停止することができます。 その結果、ユーザーが応答しないアプリケーションを発生することができます。 さらに、その他のドライバーで可能性がありますなどのシステム リソースを取得できません。[作業項目](using-framework-work-items.md)、ドライバーは、それらを解放しない場合は、します。

-   スタックの上と下、自分のドライバーには、演算を同期的に実行が必要とする場合、ドライバーは、同期 I/O を使用してください。 そのため、他のドライバーをドライバー スタックに存在する場合の要件の詳細について習得の必要性します。

次の例では、同期 I/O 制御 (IOCTL) 要求を送信する方法を示します。

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

 

 





