---
title: UMDF で i/o 要求をキャンセルしています
description: UMDF で i/o 要求をキャンセルしています
ms.assetid: 4f69903b-00ef-4b47-a564-aaa7d076481b
keywords:
- I/o 要求 WDK UMDF、キャンセル
- 要求の処理 WDK UMDF、要求の取り消し
- i/o 要求を取り消す WDK UMDF
- フライト中の要求 WDK UMDF
- I/o 要求 WDK UMDF、状態
- 要求処理 WDK UMDF、状態
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f25ad6977b67668ec22c5ba6c63a6db0bc93d353
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843651"
---
# <a name="canceling-io-requests-in-umdf"></a>UMDF で i/o 要求をキャンセルしています


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

デバイスの進行中の i/o 操作 (ディスクからの複数のブロックの読み取り要求など) は、アプリケーション、システム、またはドライバーによって取り消されることがあります。 デバイスの i/o 操作が取り消された場合、i/o マネージャーは i/o 操作に関連付けられているすべての未処理 i/o 要求をキャンセルしようとします。 I/o マネージャーが i/o 要求をキャンセルしようとしたときに、デバイスのドライバーが通知を受け取るように登録できます。また、ドライバーは、\_WIN32 (エラー\_操作\_中止された) からの HRESULT\_の完了ステータスを使用[して、所有している](completing-i-o-requests.md)要求をキャンセルできます。

フレームワークは、フレームワークベースのドライバーのキャンセル作業の一部を処理します。 デバイスの i/o 操作が取り消された場合、フレームワークは、\_WIN32 (エラー\_操作\_中止) からの HRESULT\_として、キャンセルされた操作に関連付けられている次の i/o 要求を完了します。

-   フレームワークがドライバーの既定の i/o キューに配置した、配信されていない i/o 要求。

-   ドライバーが[**Iwdfioqueue:: ConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfioqueue-configurerequestdispatching)を呼び出したため、フレームワークが別のキューに転送した、配信されていない i/o 要求。

これらの要求は、フレームワークによってキャンセルされるため、ドライバーには配信されません。

フレームワークがドライバーに i/o 要求を送信した後、ドライバーは要求を所有しており、フレームワークはその要求を取り消すことができません。 この時点では、ドライバーのみが i/o 要求をキャンセルできますが、フレームワークは、要求をキャンセルする必要があることをドライバーに通知する必要があります。 ドライバーは、 [**Irequestcallback cancel:: OnCancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackcancel-oncancel) callback 関数を提供することによって、この通知を受信します。

場合によっては、ドライバーは i/o キューから i/o 要求を受信しますが、要求を処理するのではなく、ドライバーは要求を同じまたは別の i/o キューにキューして、後で処理することができます。 たとえば、フレームワークは、ドライバーの要求ハンドラーの1つに i/o 要求を配信し、後で[**IWDFIoRequest:: ForwardToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-forwardtoioqueue)を呼び出して、別のキューまたは[**IWDFIoRequest2:: キューへに要求を配置する場合があります。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-requeue)要求を同じキューに戻します。

このような場合は、要求が i/o キューにあるため、フレームワークは i/o 要求を取り消すことができます。 ただし、ドライバーが要求が存在する i/o キューのコールバック関数を登録している場合、関連付けられている i/o 操作が取り消されるときに、フレームワークは要求をキャンセルする代わりにコールバック関数を呼び出します。 フレームワークがドライバーのコールバック関数を呼び出す場合、ドライバーは要求をキャンセルする必要があります。

要約すると、i/o 操作が取り消された場合、フレームワークは、ドライバーにまだ配信されていないすべての関連付けられた i/o 要求を常にキャンセルします。 ドライバーが要求を受信してキューすると、ドライバーが i/o キューのコールバック関数を提供しない限り、フレームワークは要求をキャンセルします (要求がキューにある場合)。

### <a name="calling-markcancelable"></a>MarkCancelable 可能の呼び出し

ドライバーは[**IWDFIoRequest:: Markcancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-markcancelable)を呼び出して、 [**irequestcallback Cancel:: OnCancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackcancel-oncancel) callback 関数を登録できます。 ドライバーが**markcancelable**を呼び出し、要求に関連付けられている i/o 操作が取り消された場合、フレームワークはドライバーの**OnCancel** callback 関数を呼び出して、ドライバーが i/o 要求をキャンセルできるようにします。

ドライバーは、比較的長い時間要求を所有している場合は**Markcancelable**を呼び出す必要があります。 たとえば、ドライバーは、デバイスが応答するのを待機する必要がある場合や、ドライバーが1つの要求を受信したときに作成された要求のセットをドライバーが完了するまで待機する必要がある場合があります。

ドライバーが**markcancelable**を呼び出さない場合、またはドライバーが**markcancelable**を呼び出した後に[**IWDFIoRequest:: unmarkmarkを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-unmarkcancelable)呼び出す場合、ドライバーはキャンセルを認識しないため、通常の場合と同様に要求を処理します。

### <a name="calling-iscanceled"></a>IsCanceled を呼び出しています

ドライバーが**Markcancelable**を呼び出して**OnCancel**コールバック関数を登録していない場合は、 [**IWDFIoRequest2:: iscanceled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-iscanceled)を呼び出して、i/o マネージャーが i/o 要求をキャンセルしようとしたかどうかを判断できます。 **Iscanceled**が**TRUE**を返した場合、ドライバーは要求をキャンセルする必要があります。

たとえば、大規模な読み取り要求または書き込み要求をいくつかの小さな要求に分割して受信するドライバーは、ドライバーが**Markcancelable**を呼び出していない場合、ドライバーの i/o ターゲットが各小さい要求を完了した後に**iscanceled**を呼び出すことがあります。受信した要求の。

### <a name="canceling-the-request"></a>要求を取り消しています

I/o 要求を取り消すには、次のいずれかが関係している可能性があります。

-   進行中の i/o 操作を停止しています。

-   I/o ターゲットに要求を転送しません。

-   [**IWDFIoRequest:: 中断要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-cancelsentrequest)を呼び出して、ドライバーが以前に i/o ターゲットに送信した要求をキャンセルしようとしています。

ドライバーが、フレームワークから受信した要求オブジェクトの i/o 要求をキャンセルしている場合、ドライバーは常に[**IWDFIoRequest:: complete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete)または[**IWDFIoRequest:: completewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation)を呼び出して、要求を完了する必要があります。これ*には、* \_WIN32 から (エラー\_操作\_中断された)\_HRESULT が返されます。 (ドライバーが[**Iwdfdevice:: CreateRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createrequest)という名前の要求オブジェクトを作成する場合、ドライバーは要求を完了するのではなく、 [**Iwdfdevice::D eletewdfobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)を呼び出します)。

 

 





