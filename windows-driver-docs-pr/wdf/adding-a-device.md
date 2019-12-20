---
title: デバイスの追加
description: デバイスの追加
ms.assetid: 233e3315-3044-42d7-867c-0a9e153eb53b
keywords:
- ユーザーモードドライバーフレームワーク WDK、デバイスの追加
- UMDF WDK, デバイスの追加
- ユーザーモードドライバー WDK UMDF、デバイスの追加
- WDK、UMDF のデバイスのインストール
- デバイスの追加 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50a8fbb37db5bf3a8f6b9a65e6d8e79d1a4bbde2
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210050"
---
# <a name="adding-a-device"></a>デバイスの追加


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

フレームワークは、ドライバーホストプロセスに読み込まれた各デバイスのデバイスオブジェクトを追加します。 デバイスを追加するために、フレームワークはドライバーの[**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)メソッドを呼び出し、呼び出しで[Iwdfdriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver)インターフェイスと[iwdfdeviceinitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize)インターフェイスを渡します。 指定された**Iwdfdeviceinitialize**インターフェイスは、ドライバーが[**Iwdfdriver:: CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)を呼び出す前にのみ有効です。 ドライバーは、 **Iwdfdeviceinitialize**の次のメソッドを呼び出して、次の操作を実行できます。

-   ドライバーは[**Iwdfdeviceinitialize:: RetrieveDevicePropertyStore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-retrievedevicepropertystore)メソッドを呼び出して、デバイスプロパティストアの[Iwdfnamedpropertystore](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfnamedpropertystore)インターフェイスを取得します。 ドライバーは、 **Iwdfnamedpropertystore**を使用して、デバイスのプロパティを取得および設定できます。

-   ドライバーは[**Iwdfdeviceinitialize:: Setの constraint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setlockingconstraint)メソッドを呼び出して、そのコールバック関数がフレームワークによってどのように呼び出されるかを指定します。

-   ドライバーは[**Iwdfdeviceinitialize:: SetFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setfilter)メソッドを呼び出して、デバイスをフィルターデバイスとして有効にします。

ドライバーは[Iwdfdeviceinitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize)を使用してデバイスを初期化した後、Iwdfdriver [**:: CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)メソッドの呼び出しで**iwdfdeviceinitialize**へのポインターを渡して、デバイスの[UMDF デバイスオブジェクト](framework-device-object.md)を作成します。 フレームワークデバイスオブジェクトが作成されると、ドライバーは[**Iwdfdevice:: CreateIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)メソッドを呼び出して、読み取りおよび書き込みの i/o キューを作成します。 これらの**Iwdfdevice:: CreateIoQueue**呼び出しでは、ドライバーは i/o キューからの要求を受信する方法を識別する必要があります。 詳細については、「 [I/o キューのディスパッチモードの構成](configuring-dispatch-mode-for-an-i-o-queue.md)」を参照してください。

 

 





