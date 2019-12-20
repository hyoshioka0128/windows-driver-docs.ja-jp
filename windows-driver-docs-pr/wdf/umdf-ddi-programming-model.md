---
title: UMDF DDI プログラミング モデル
description: UMDF DDI プログラミング モデル
ms.assetid: d4bf0791-d2c4-4504-84ad-020880124363
keywords:
- UMDF オブジェクト WDK、DDI
- フレームワークオブジェクト WDK UMDF、DDI
- UMDF DDI WDK
- DDI WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e91e356650727c870cd8fb6c88bb8787d82733a9
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209852"
---
# <a name="umdf-ddi-programming-model"></a>UMDF DDI プログラミング モデル


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

フレームワークと UMDF ドライバーは、UMDF DDI を介して通信します。 UMDF ddi は KMDF DDI に似ていますが、UMDF DDI は COM に基づいている点が異なります。 そのため、KMDF に精通しているドライバーライターは、UMDF を理解します。

UMDF は、フレームワークオブジェクトの種類ごとに、オブジェクトのインスタンスを操作するためのインターフェイスを定義します。 各インターフェイスは、メソッドとプロパティをサポートしています。 メソッドは、オブジェクトの代わりに実行できるアクションと、オブジェクトの特性を設定および取得するプロパティを定義します。 一部のインターフェイスは、フレームワークによって実装され、他のインターフェイスはドライバーによって実装されます。 フレームワークオブジェクトによって公開されるインターフェイスは、IWDF&lt;object&gt;という形式になっています。一方、ドライバーによって公開されるイベントコールバックインターフェイスは、I&lt;オブジェクト&gt;&lt;アクション&gt;、&lt;オブジェクト&gt; がキューや要求などを表し、&lt;アクション&gt; がインターフェイスの動作を示します。 コールバックインターフェイスのメソッドは、"On" で始まります。

UMDF ドライバーは、メソッドとプロパティを通じて、フレームワークのオブジェクトと通信します。 フレームワークは、イベント通知を使用してドライバーと通信します。これは、フレームワークが特定のイベントについてドライバーに通知するために呼び出すことができるコールバック関数です。 コールバック関数を登録するために、ドライバーは、たとえば次のフレームワークオブジェクトメソッドを呼び出すことができ、ドライバーがサポートするコールバック関数のすべてのインターフェイスに関連付けられた**IUnknown**インターフェイスへのポインターを渡すことができます。

-   [**IWDFDevice::CreateIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)

-   [**IWDFDriver:: CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)

-   [**IWDFDriver::CreateWdfObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createwdfobject)

ドライバーからフレームワークへの通信の例として、デバイスの既定の i/o キューオブジェクトについて考えてみましょう。 ドライバーは、 [**Iwdfioqueue:: GetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfioqueue-getstate)などのメソッドを呼び出して、i/o キューに関する状態情報を取得したり、 [**Iwdfioqueue:: RetrieveNextRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfioqueue-retrievenextrequest)を呼び出して i/o キューから要求を取得したりできます。 また、 [Iqueuecallbackread](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackread)や[Iqueuecallbackwrite](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackwrite)などのコールバックインターフェイスを登録するために、 [**Iwdfdevice:: CreateIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)メソッドを呼び出して、i/o キューでの通知を要求することもできます。 これらのインターフェイスのメソッドは、アプリケーションが読み取り要求と書き込み要求を送信するときに、フレームワークによって呼び出されます。

フレームワークは、ドライバーコールバックメソッド間で必要な同期を提供します。 既定では、フレームワークはデバイスのオブジェクトレベルで同期します。つまり、フレームワークは、デバイスオブジェクトレベル以下のイベントコールバックメソッドを同時に呼び出すことはありません。 ドライバーは、同期を要求することによって、この既定値を上書きできます。 詳細については、「[コールバック同期モードの指定](specifying-a-callback-synchronization-mode.md)」を参照してください。

 

 





