---
title: フレームワーク オブジェクトの階層
description: フレームワーク オブジェクトの階層
ms.assetid: ffacca8f-4083-4998-83d2-7c31544eb497
keywords:
- UMDF オブジェクト WDK、階層
- framework オブジェクト WDK UMDF、階層
- WDK UMDF 階層
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c702ca7570dba48b1808f99b3fdb98f113cbbdd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382860"
---
# <a name="framework-object-hierarchy"></a>フレームワーク オブジェクトの階層


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

次の図は、親と子 framework のオブジェクト階層を示します。

![umdf 親-子オブジェクトの階層](images/umdfhierarchy.gif)

Framework のオブジェクトの有効期間の範囲は、階層と、オブジェクトの作成方法、場所によって決まります。 Framework のオブジェクトの有効期間の範囲は、次のカテゴリのいずれかに分類されます。

-   フレームワークは、作成と、オブジェクトの破棄を制御します。

    フレームワークを作成しなどのオブジェクトを破棄、[ドライバー オブジェクト](framework-driver-object.md)と[デバイス オブジェクト](framework-device-object.md)、システム イベントに応答します。 ユーザー モード ドライバーを呼び出すと、 [ **IWDFDriver::CreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)ドライバーがデバイス オブジェクトは、前に、フレームワークによって通知を登録できます必要に応じて、デバイスを作成するメソッドがオブジェクト破棄されます。

-   フレームワークは、オブジェクトを作成します。ただし、オブジェクトが解放されるときに、ドライバーを制御します。

    [I/O 要求オブジェクト](framework-i-o-request-object.md)ドライバーに I/O が表示されるときにこのパターンに従います。 フレームワークは、要求オブジェクトを作成し、ドライバー呼び出されるまで、要求オブジェクトの有効期間が有効な[ **IWDFIoRequest::Complete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-complete)メソッド。

-   ドライバーは、オブジェクトを作成し、オブジェクトを別のフレームワーク オブジェクトに関連付けます。

    一部のフレームワーク オブジェクトは、有効期間管理のために関連付けられるオブジェクトは、親フレームワークのオブジェクト インスタンスによって公開されるメソッドによって作成されます。 [ **IWDFDevice::CreateIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)メソッドは、このパターンの例を示します。 呼び出し**IWDFDevice::CreateIoQueue**成功すると、新しく作成された I/O キューが関連付けられているデバイス インスタンスが、 [IWDFDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdevice)インターフェイスが表現されます。 親オブジェクトが破棄されるときに、フレームワークは子インスタンスを自動的にクリーンアップします。 ドライバーは、ドライバー、フレームワークで適切なコールバック関数を登録する場合、これらのイベントの通知されます。

 

 





