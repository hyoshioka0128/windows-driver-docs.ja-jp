---
title: デバイスの追加
description: デバイスの追加
ms.assetid: 233e3315-3044-42d7-867c-0a9e153eb53b
keywords:
- ユーザー モード ドライバー フレームワーク WDK は、デバイスの追加
- UMDF WDK、デバイスの追加
- ユーザー モード ドライバー WDK UMDF、デバイスの追加
- デバイス、WDK UMDF をインストールします。
- WDK UMDF デバイスを追加します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47e2c805630faa1c7a2d80ce7adf23438a637f20
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573627"
---
# <a name="adding-a-device"></a>デバイスの追加


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

フレームワークは、各デバイス ドライバーのホスト プロセスで読み込まれるデバイス オブジェクトを追加します。 デバイスを追加するには、フレームワークは、ドライバーを呼び出します[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)メソッドを呼び出し、 [IWDFDriver](https://msdn.microsoft.com/library/windows/hardware/ff558893)と[IWDFDeviceInitialize。](https://msdn.microsoft.com/library/windows/hardware/ff556965)インターフェイスの呼び出しで。 指定された**IWDFDeviceInitialize**インターフェイスは、ドライバーの呼び出しの前に有効なのみ[ **IWDFDriver::CreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff558899)します。 ドライバーは、次のメソッドを呼び出すことができます**IWDFDeviceInitialize**次の操作を実行します。

-   ドライバーの呼び出し、 [ **IWDFDeviceInitialize::RetrieveDevicePropertyStore** ](https://msdn.microsoft.com/library/windows/hardware/ff556982)を取得するメソッド、 [IWDFNamedPropertyStore](https://msdn.microsoft.com/library/windows/hardware/ff560164)デバイス プロパティのインターフェイスストア。 ドライバーを使用して**IWDFNamedPropertyStore**を取得して、デバイスのプロパティを設定します。

-   ドライバーの呼び出し、 [ **IWDFDeviceInitialize::SetLockingConstraint** ](https://msdn.microsoft.com/library/windows/hardware/ff556991)フレームワークによってそのコールバック関数の呼び出し方法を指定します。

-   ドライバーの呼び出し、 [ **IWDFDeviceInitialize::SetFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff556985)メソッド フィルター デバイスとしてデバイスを有効にします。

ドライバーは使用後[IWDFDeviceInitialize](https://msdn.microsoft.com/library/windows/hardware/ff556965)デバイスを初期化するために、ドライバーがへのポインターを渡す**IWDFDeviceInitialize**への呼び出しで、 [ **IWDFDriver:。CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff558899)を作成する方法、 [UMDF デバイス オブジェクト](framework-device-object.md)デバイス。 ドライバーへの呼び出しは、フレームワークのデバイス オブジェクトが作成された後、 [ **IWDFDevice::CreateIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff557020)メソッドを作成、読み取りと書き込みの I/O キュー。 これらの**IWDFDevice::CreateIoQueue** I/O キューからの要求の受信呼び出し、ドライバーを識別する必要があります。 詳細については、次を参照してください。 [I/O キューのディスパッチ モードを構成する](configuring-dispatch-mode-for-an-i-o-queue.md)します。

 

 





