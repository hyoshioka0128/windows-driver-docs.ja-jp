---
title: UMDF DDI プログラミング モデル
description: UMDF DDI プログラミング モデル
ms.assetid: d4bf0791-d2c4-4504-84ad-020880124363
keywords:
- UMDF オブジェクト WDK、DDI
- オブジェクトは、フレームワークの WDK の UMDF DDI
- UMDF DDI WDK
- DDI WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2085af1a240daa48edc265cd4a40d2ddf3d4cd99
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372302"
---
# <a name="umdf-ddi-programming-model"></a>UMDF DDI プログラミング モデル


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

フレームワークと UMDF ドライバー UMDF DDI 経由で通信します。 UMDF DDI は COM をベースにする点を除いて、UMDF DDI は KMDF DDI に似ています そのため、KMDF 慣れてドライバー開発者は、UMDF を理解できます。

Framework のオブジェクトの種類ごと、UMDF はオブジェクトのインスタンスを操作するためのインターフェイスを定義します。 各インターフェイスには、メソッドとプロパティがサポートしています。 メソッドは、オブジェクトの代わりに実行できるアクションを定義し、プロパティを設定およびオブジェクトの特性を取得します。 一部のインターフェイスは、フレームワークによって実装され、他のユーザーは、ドライバーによって実装します。 Framework オブジェクトによって公開されるインターフェイスはフォーム IWDF&lt;オブジェクト&gt;はの形式は、ドライバーによって公開されるイベントのコールバック インターフェイス&lt;オブジェクト&gt;&lt;アクション&gt;、場所&lt;オブジェクト&gt;表しますキュー、要求、および、および&lt;アクション&gt;インターフェイスの動作を示します。 コールバック インターフェイスのメソッドは、"On"で始まります。

UMDF ドライバーは、メソッド、プロパティを通じて、framework のオブジェクトと通信します。 フレームワークは、イベント通知は、特定のイベントのドライバーに通知するために、フレームワークを呼び出すことができるコールバック関数を使ってドライバーと通信します。 コールバック関数を登録するドライバーが呼び出すには、たとえば、framework オブジェクトの次のメソッドへのポインターを渡すことができます、 **IUnknown**されるコールバック関数には、すべてのインターフェイスに関連付けられているインターフェイス ドライバーサポートされています。

-   [**IWDFDevice::CreateIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)

-   [**IWDFDriver::CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)

-   [**IWDFDriver::CreateWdfObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createwdfobject)

フレームワークの通信をドライバーの例は、デバイスの既定の I/O キューのオブジェクトについて考えてみます。 ドライバーはなどのメソッドを呼び出すことができます[ **IWDFIoQueue::GetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfioqueue-getstate)I/O キューに関するステータス情報を取得する、または[ **IWDFIoQueue::RetrieveNextRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfioqueue-retrievenextrequest) I/O キューからの要求を取得します。 呼び出すことによって、ドライバーは I/O キュー上の通知の要求もできる、 [ **IWDFDevice::CreateIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)メソッドなど、コールバック インターフェイスを登録する[IQueueCallbackRead](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iqueuecallbackread)と[IQueueCallbackWrite](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iqueuecallbackwrite)します。 これらのインターフェイスのメソッドは、アプリケーションに送信される読み取りときに、その後、フレームワークによって呼び出されますおよび書き込み要求。

フレームワークは、ドライバーのコールバック メソッドで必要なすべての同期を提供します。 既定では、フレームワークをデバイス オブジェクト レベルで同期します。つまり、フレームワークは同時に呼び出しませんイベント デバイス オブジェクトのレベル以下でコールバック メソッド。 ドライバーは、同期を要求しないによってこの既定をオーバーライドできます。 詳細については、次を参照してください。[コールバックの同期モードを指定する](specifying-a-callback-synchronization-mode.md)します。

 

 





