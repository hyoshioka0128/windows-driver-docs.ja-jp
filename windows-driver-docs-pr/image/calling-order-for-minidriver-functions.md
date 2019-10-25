---
title: ミニドライバー関数の順序の呼び出し
description: ミニドライバー関数の順序の呼び出し
ms.assetid: 0e51d29c-964d-44d5-86be-095601286f94
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dfd74f30c8acd813a9fbe736fe6a81f00d0d75d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840884"
---
# <a name="calling-order-for-minidriver-functions"></a>ミニドライバー関数の順序の呼び出し





ミニドライバーが開始されると、 [**IGetStatus:: Initialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)や[**i Usd::** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getstatus)など、古い一部の STI エントリポイントが呼び出されます。 最初のアプリケーションがデバイスと通信しようとすると、その時点で、WIA サービスは[**IWiaMiniDrv::D rvinitializewia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)を呼び出します。 この関数は、ミニドライバーが項目ツリーを構築する必要があることを示します。

次に、WIA サービスは、ツリー内の各項目に対して[**IWiaMiniDrv::D rvinititemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinititemproperties)を呼び出します。 ミニドライバーは、アイテムに関連するすべてのプロパティを作成する必要があります。 場合によっては、空のプロパティを作成し、後でそのデータを入力するのが賢明です。 たとえば、パフォーマンスを向上させるには、以下で説明するように、WIA サービスが明示的に要求したときにのみ、カメラのイメージサムネイルを読み取る必要があります。

次に呼び出される関数は、アプリケーションとデバイスの種類によって異なります。 通常、アプリケーションの最も一般的な操作は、データの転送です。 スキャナーの場合、アプリケーションはまず、デバイスから取得するイメージを定義するプロパティ (データ型やエクステントなど) を設定します。 アプリケーションがプロパティを変更すると、WIA サービスは[**IWiaMiniDrv::D rvvalidateitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)を呼び出します。 ミニドライバーは、プロパティが有効であること、およびデバイスと通信する必要があるかどうかを確認する必要があります。 データ転送が行われる前に別のアプリケーションによってプロパティが異なる値に設定される可能性があるため、ミニドライバーでは通常、その機能のプロパティを設定しないようにする必要があります。

データを転送するために、WIA サービスは[**IWiaMiniDrv::D rvlockwiadevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvlockwiadevice)、 [**IWiaMiniDrv::d rvwriteitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties)、 [**IWiaMiniDrv::d Rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)、 [**IWiaMiniDrv::d rvunlockwiadevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvunlockwiadevice)をこの順序で呼び出します。 デバイスをロックおよびロック解除する呼び出しは、転送中に他のアプリケーションがデバイスにアクセスしないことを保証します。 スキャナーの場合、 **IWiaMiniDrv::D rvwriteitemproperties**は、位置、範囲、解決などのプロパティをデバイスに送信する必要があります。 カメラドライバーは、通常、デバイスにプロパティを送信する必要はありません。 **IWiaMiniDrv::D rvacquireitemdata**は、 [IWiaMiniDrvCallback COM インターフェイス](iwiaminidrvcallback-com-interface.md)を使用して、デバイスから画像データを取得して、WIA サービス経由でアプリケーションに送り返す必要があります。

カメラの場合、アプリケーションでイメージのサムネイルを表示するには、各イメージで[**IWiaMiniDrv::D rvreaditemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties)を呼び出します。 ミニドライバーは、その時点でサムネイルを読み取り、ドライバー項目コンテキストにキャッシュする必要があります。 複数のアプリケーションでサムネイルが要求される可能性があるため、サムネイルをキャッシュすることが重要です。その結果、 **IWiaMiniDrv::D rvreaditemproperties**が複数回呼び出されます。 ミニドライバーがアプリケーションに要求するたびにサムネイルが読み込まれると、パフォーマンスが低下します。

カメラに関するその他の特別な考慮事項の1つは、カメラの設定に影響を与えるルート項目のプロパティです (シャッター速度など)。 アプリケーションがこれらのプロパティを変更すると、WIA サービスは[**IWiaMiniDrv::D rvvalidateitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)を呼び出します。 ミニドライバーは、必要に応じて、プロパティ設定を検証するためにカメラと通信できます。 ただし、この関数はカメラの設定を変更するのに最適な場所ではありません。これは、別のアプリケーションもプロパティを変更できるためです。 ミニドライバーは、 [**IWiaMiniDrv::D rvdevicecommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdevicecommand)関数を呼び出して新しいイメージをキャプチャするときに、ルート項目のプロパティからすべてのカメラ設定を更新する必要があります。

 

 




