---
title: ミニドライバー関数の順序の呼び出し
description: ミニドライバー関数の順序の呼び出し
ms.assetid: 0e51d29c-964d-44d5-86be-095601286f94
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbc6cbe8d6b0c0d4c3bede04f548ca67f926f4c7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366742"
---
# <a name="calling-order-for-minidriver-functions"></a>ミニドライバー関数の順序の呼び出し





ミニドライバーが開始されると、そのなどの呼び出し、古い STI エントリ ポイントのいくつか[ **IStiUSD::Initialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-initialize)、および[ **IStiUSD::GetStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getstatus). WIA サービスを呼び出す最初のアプリケーションがデバイスと通信しようとすると、すぐ[ **IWiaMiniDrv::drvInitializeWia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)します。 この関数では、ミニドライバーが項目のツリーを構築する必要があります。

WIA サービスの [次へ] 呼び出し[ **IWiaMiniDrv::drvInitItemProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinititemproperties)ツリー内の各項目にします。 ミニドライバーのすべてのプロパティをアイテムに関連する作成する必要があります。 状況によっては、空のプロパティを作成し、後でそのデータを入力する方が良い場合があります。 たとえば、パフォーマンスの向上のためのカメラで画像のサムネイルもお読みください WIA サービスは、具体的には、場合にのみ以下に示すよう。

呼び出される次の関数は、アプリケーションとデバイスの種類によって異なります。 通常、アプリケーションの最も一般的な操作ではデータを転送しています。 スキャナーの場合、アプリケーションは、まず、デバイスから取得したいイメージを定義するプロパティ (たとえば、データ型とエクステント) を設定します。 サービス呼び出しで WIA [ **IWiaMiniDrv::drvValidateItemProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)アプリケーションが任意のプロパティを変更する場合。 ミニドライバーは、必要な場合に、デバイスと通信するプロパティが有効である確認する必要があります。 ミニドライバー避ける必要があります一般に、この関数で、プロパティを設定別のアプリケーションは、データ転送が発生する前に、ごとに異なる値のプロパティを設定でしたので。

データを WIA サービスの呼び出しを転送する[ **IWiaMiniDrv::drvLockWiaDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvlockwiadevice)、 [ **IWiaMiniDrv::drvWriteItemProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties)、 [**IWiaMiniDrv::drvAcquireItemData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)、および[ **IWiaMiniDrv::drvUnLockWiaDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvunlockwiadevice)点で、注文します。 ロックし、デバイスのロック解除の呼び出しでは、他のアプリケーションにアクセスしないこと、デバイス、転送中を保証します。 スキャナーの**IWiaMiniDrv::drvWriteItemProperties**位置、エクステント、および解像度などのプロパティをデバイスに送信する必要があります。 カメラのドライバーは通常、任意のプロパティをデバイスに送信する必要はありません。 **IWiaMiniDrv::drvAcquireItemData**デバイスから画像データを取得し、WIA サービス経由でアプリケーションに送信する必要がありますを使用して、 [IWiaMiniDrvCallback COM インターフェイス](iwiaminidrvcallback-com-interface.md)します。

カメラ、アプリケーションは、画像のサムネイルを表示する必要がある場合、WIA サービス呼び出し[ **IWiaMiniDrv::drvReadItemProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties)各イメージにします。 ミニドライバーは、サムネイルをその時点で読み取りし、ドライバーのコンテキスト アイテムにキャッシュする必要があります。 複数のアプリケーションが複数の呼び出しでその結果、サムネイルのメッセージが表示するため、サムネイルをキャッシュする重要なは**IWiaMiniDrv::drvReadItemProperties**します。 ミニドライバーは、アプリケーションで求められるたびに、サムネイルを読み取り、パフォーマンスが低下します。

カメラの他の特別な配慮を 1 つは、(たとえばシャッター スピード) カメラの設定に影響を与えるルート項目のプロパティです。 WIA サービスを呼び出すとき、アプリケーションでは、これらのプロパティを変更、 [ **IWiaMiniDrv::drvValidateItemProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)します。 必要に応じて、プロパティの設定を検証する場合、ミニドライバーは、カメラと通信できます。 ただし、この関数は、別のアプリケーションはまた、プロパティを変更できるので、カメラの設定を変更する最適な場所にはありません。 ミニドライバーは、すべてのルート項目のプロパティからカメラの設定を更新する必要があるときに、 [ **IWiaMiniDrv::drvDeviceCommand** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdevicecommand)関数が呼び出され、新しいイメージをキャプチャします。

 

 




