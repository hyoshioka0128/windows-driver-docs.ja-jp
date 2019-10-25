---
title: フレームワーク オブジェクトの階層
description: フレームワーク オブジェクトの階層
ms.assetid: ffacca8f-4083-4998-83d2-7c31544eb497
keywords:
- UMDF オブジェクト WDK、階層
- フレームワークオブジェクト WDK UMDF、階層
- 階層 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 216574d417b252560588f8e414be9d93c3032226
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843119"
---
# <a name="framework-object-hierarchy"></a>フレームワーク オブジェクトの階層


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

次の図は、親子フレームワークオブジェクト階層を示しています。

![umdf 親子オブジェクト階層](images/umdfhierarchy.gif)

フレームワークオブジェクトの有効期間のスコープは、階層内の場所とオブジェクトの作成方法によって決まります。 フレームワークオブジェクトの有効期間のスコープは、次のいずれかのカテゴリに分類されます。

-   フレームワークは、オブジェクトの作成と破棄を制御します。

    このフレームワークは、システムイベントに応答して、[ドライバーオブジェクト](framework-driver-object.md)や[デバイスオブジェクト](framework-device-object.md)などのオブジェクトを作成し、破棄します。 ユーザーモードドライバーが[**Iwdfdriver:: CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)メソッドを呼び出してデバイスオブジェクトを作成すると、デバイスオブジェクトが破棄される前に、必要に応じて、フレームワークによって通知されるようにドライバーを登録できます。

-   フレームワークによってオブジェクトが作成されます。ただし、ドライバーはオブジェクトが解放されるタイミングを制御します。

    I/o[要求オブジェクト](framework-i-o-request-object.md)は、ドライバーに i/o が表示されるときに、このパターンに従います。 フレームワークは要求オブジェクトを作成します。要求オブジェクトの有効期間は、ドライバーが[**IWDFIoRequest:: Complete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete)メソッドを呼び出すまで有効です。

-   ドライバーはオブジェクトを作成し、オブジェクトを別のフレームワークオブジェクトに関連付けます。

    一部のフレームワークオブジェクトは、有効期間管理の目的でオブジェクトが関連付けられる親フレームワークオブジェクトインスタンスによって公開されるメソッドによって作成されます。 このパターンの例として、 [**Iwdfdevice:: CreateIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)メソッドがあります。 **Iwdfdevice:: CreateIoQueue**への呼び出しが成功すると、新しく作成された i/o キューは、 [iwdfdevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice)インターフェイスが表すデバイスインスタンスに関連付けられます。 親オブジェクトが破棄されると、フレームワークは子インスタンスを自動的にクリーンアップします。 ドライバーがフレームワークに適切なコールバック関数を登録すると、これらのイベントが通知されます。

 

 





