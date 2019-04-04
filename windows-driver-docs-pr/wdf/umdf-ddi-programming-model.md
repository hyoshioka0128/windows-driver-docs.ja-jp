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
ms.openlocfilehash: c62b667615518103553ccb598809c312f01b219a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571301"
---
# <a name="umdf-ddi-programming-model"></a>UMDF DDI プログラミング モデル


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

フレームワークと UMDF ドライバー UMDF DDI 経由で通信します。 UMDF DDI は COM をベースにする点を除いて、UMDF DDI は KMDF DDI に似ています そのため、KMDF 慣れてドライバー開発者は、UMDF を理解できます。

Framework のオブジェクトの種類ごと、UMDF はオブジェクトのインスタンスを操作するためのインターフェイスを定義します。 各インターフェイスには、メソッドとプロパティがサポートしています。 メソッドは、オブジェクトの代わりに実行できるアクションを定義し、プロパティを設定およびオブジェクトの特性を取得します。 一部のインターフェイスは、フレームワークによって実装され、他のユーザーは、ドライバーによって実装します。 Framework オブジェクトによって公開されるインターフェイスはフォーム IWDF&lt;オブジェクト&gt;はの形式は、ドライバーによって公開されるイベントのコールバック インターフェイス&lt;オブジェクト&gt;&lt;アクション&gt;、場所&lt;オブジェクト&gt;表しますキュー、要求、および、および&lt;アクション&gt;インターフェイスの動作を示します。 コールバック インターフェイスのメソッドは、"On"で始まります。

UMDF ドライバーは、メソッド、プロパティを通じて、framework のオブジェクトと通信します。 フレームワークは、イベント通知は、特定のイベントのドライバーに通知するために、フレームワークを呼び出すことができるコールバック関数を使ってドライバーと通信します。 コールバック関数を登録するドライバーが呼び出すには、たとえば、framework オブジェクトの次のメソッドへのポインターを渡すことができます、 **IUnknown**されるコールバック関数には、すべてのインターフェイスに関連付けられているインターフェイス ドライバーサポートされています。

-   [**IWDFDevice::CreateIoQueue**](https://msdn.microsoft.com/library/windows/hardware/ff557020)

-   [**IWDFDriver::CreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff558899)

-   [**IWDFDriver::CreateWdfObject**](https://msdn.microsoft.com/library/windows/hardware/ff558906)

フレームワークの通信をドライバーの例は、デバイスの既定の I/O キューのオブジェクトについて考えてみます。 ドライバーはなどのメソッドを呼び出すことができます[ **IWDFIoQueue::GetState**](https://msdn.microsoft.com/library/windows/hardware/ff558959)I/O キューに関するステータス情報を取得する、または[ **IWDFIoQueue::RetrieveNextRequest**](https://msdn.microsoft.com/library/windows/hardware/ff558967) I/O キューからの要求を取得します。 呼び出すことによって、ドライバーは I/O キュー上の通知の要求もできる、 [ **IWDFDevice::CreateIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff557020)メソッドなど、コールバック インターフェイスを登録する[IQueueCallbackRead](https://msdn.microsoft.com/library/windows/hardware/ff556872)と[IQueueCallbackWrite](https://msdn.microsoft.com/library/windows/hardware/ff556882)します。 これらのインターフェイスのメソッドは、アプリケーションに送信される読み取りときに、その後、フレームワークによって呼び出されますおよび書き込み要求。

フレームワークは、ドライバーのコールバック メソッドで必要なすべての同期を提供します。 既定では、フレームワークをデバイス オブジェクト レベルで同期します。つまり、フレームワークは同時に呼び出しませんイベント デバイス オブジェクトのレベル以下でコールバック メソッド。 ドライバーは、同期を要求しないによってこの既定をオーバーライドできます。 詳細については、[コールバックの同期モードを指定する](specifying-a-callback-synchronization-mode.md)を参照してください。

 

 





