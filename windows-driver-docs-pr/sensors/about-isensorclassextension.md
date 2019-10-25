---
title: ISensorClassExtension について
description: ISensorClassExtension について
ms.assetid: 1f55f28a-796a-40e5-9995-e6a28761b9a4
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 49ac14606ed8161e19ad23d7e87b4b6adae8a2c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824301"
---
# <a name="about-isensorclassextension"></a>ISensorClassExtension について


センサードライバーは、ISensorClassExtension を使用して、センサークラス拡張の初期化と unitialize、イベントの発生、WPD 入力/出力制御コード (Ioctl) の処理、および UMDF ファイルハンドルの正常な終了を行います。

## <a name="methods-to-manage-object-lifetime"></a>オブジェクトの有効期間を管理するメソッド

クラス拡張を初期化するために、PnP ベースのハードウェアセンサードライバーは、 [**IPnpCallbackHardware:: OnISensorClassExtension hardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)の UMDF によって呼び出されたときに、 [ **:: initialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-initialize)を呼び出します。 この手順では、ドライバーの main クラスへのポインターと、クラス拡張オブジェクトによって発生するイベントを処理するコールバックインターフェイスを実装するクラスに、クラス拡張オブジェクトを提供します。 [**IPnpCallbackHardware:: OnReleaseHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onreleasehardware)の UMDF によってドライバーが呼び出された場合、 [**ISensorClassExtension::** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-uninitialize)を呼び出し、クラス拡張オブジェクトを解放する必要があります。 センサーの種類によっては、クラス拡張の初期化と初期化解除が異なるタイミングで必要になる場合があることに注意してください。

## <a name="methods-to-raise-events"></a>イベントを発生させるメソッド

ドライバーは、 [**ISensorClassExtension::P oststatechange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)を呼び出して[**ISensorClassExtension::P ostevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-postevent)と状態情報のイベントを呼び出すことによって、さまざまな種類のセンサーイベント (通常はセンサーデータを含む) を発生させることができます。 センサードライバーでのイベントの動作の詳細については、「[センサードライバーのイベントについ](about-sensor-driver-events.md)て」を参照してください。

## <a name="methods-to-manage-ioctls-and-handles"></a>Ioctl とハンドルを管理するメソッド

センサードライバーは、次の2種類の UMDF 呼び出しをクラス拡張に転送します。

-   [**IQueueCallbackDeviceIoControl:: OnDeviceIoControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol)を通じて受信される i/o 制御コードの処理を要求します。 I/o 要求をクラス拡張に転送して処理するには、ドライバーは[**ISensorClassExtension::P rocessiocontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-processiocontrol)を呼び出す必要があります。

-   [**IFileCallbackCleanup:: OnCleanupFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile)を通じて受信されたファイルハンドルを閉じるクライアントに関する通知。 I/o 要求のキャンセルを転送するには、ドライバーは[**ISensorClassExtension:: CleanupFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-cleanupfile)を呼び出す必要があります。

 

 




