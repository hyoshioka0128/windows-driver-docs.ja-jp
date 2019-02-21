---
title: ミニドライバー関数の順序を呼び出す
description: ミニドライバー関数の順序を呼び出す
ms.assetid: 0e51d29c-964d-44d5-86be-095601286f94
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31bd38f8d3139dc32cf1b2c7b8f4adceed7e968b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529067"
---
# <a name="calling-order-for-minidriver-functions"></a>ミニドライバー関数の順序を呼び出す





ミニドライバーが開始されると、そのなどの呼び出し、古い STI エントリ ポイントのいくつか[ **IStiUSD::Initialize**](https://msdn.microsoft.com/library/windows/hardware/ff543824)、および[ **IStiUSD::GetStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff543823). WIA サービスを呼び出す最初のアプリケーションがデバイスと通信しようとすると、すぐ[ **IWiaMiniDrv::drvInitializeWia**](https://msdn.microsoft.com/library/windows/hardware/ff544986)します。 この関数では、ミニドライバーが項目のツリーを構築する必要があります。

WIA サービスの [次へ] 呼び出し[ **IWiaMiniDrv::drvInitItemProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff544989)ツリー内の各項目にします。 ミニドライバーのすべてのプロパティをアイテムに関連する作成する必要があります。 状況によっては、空のプロパティを作成し、後でそのデータを入力する方が良い場合があります。 たとえば、パフォーマンスの向上のためのカメラで画像のサムネイルもお読みください WIA サービスは、具体的には、場合にのみ以下に示すよう。

呼び出される次の関数は、アプリケーションとデバイスの種類によって異なります。 通常、アプリケーションの最も一般的な操作ではデータを転送しています。 スキャナーの場合、アプリケーションは、まず、デバイスから取得したいイメージを定義するプロパティ (たとえば、データ型とエクステント) を設定します。 サービス呼び出しで WIA [ **IWiaMiniDrv::drvValidateItemProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff545017)アプリケーションが任意のプロパティを変更する場合。 ミニドライバーは、必要な場合に、デバイスと通信するプロパティが有効である確認する必要があります。 ミニドライバー避ける必要があります一般に、この関数で、プロパティを設定別のアプリケーションは、データ転送が発生する前に、ごとに異なる値のプロパティを設定でしたので。

データを WIA サービスの呼び出しを転送する[ **IWiaMiniDrv::drvLockWiaDevice**](https://msdn.microsoft.com/library/windows/hardware/ff544995)、 [ **IWiaMiniDrv::drvWriteItemProperties**](https://msdn.microsoft.com/library/windows/hardware/ff545020)、 [**IWiaMiniDrv::drvAcquireItemData**](https://msdn.microsoft.com/library/windows/hardware/ff543956)、および[ **IWiaMiniDrv::drvUnLockWiaDevice**](https://msdn.microsoft.com/library/windows/hardware/ff545012)点で、注文します。 ロックし、デバイスのロック解除の呼び出しでは、他のアプリケーションにアクセスしないこと、デバイス、転送中を保証します。 スキャナーの**IWiaMiniDrv::drvWriteItemProperties**位置、エクステント、および解像度などのプロパティをデバイスに送信する必要があります。 カメラのドライバーは通常、任意のプロパティをデバイスに送信する必要はありません。 **IWiaMiniDrv::drvAcquireItemData**デバイスから画像データを取得し、WIA サービス経由でアプリケーションに送信する必要がありますを使用して、 [IWiaMiniDrvCallback COM インターフェイス](iwiaminidrvcallback-com-interface.md)します。

カメラ、アプリケーションは、画像のサムネイルを表示する必要がある場合、WIA サービス呼び出し[ **IWiaMiniDrv::drvReadItemProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff545005)各イメージにします。 ミニドライバーは、サムネイルをその時点で読み取りし、ドライバーのコンテキスト アイテムにキャッシュする必要があります。 複数のアプリケーションが複数の呼び出しでその結果、サムネイルのメッセージが表示するため、サムネイルをキャッシュする重要なは**IWiaMiniDrv::drvReadItemProperties**します。 ミニドライバーは、アプリケーションで求められるたびに、サムネイルを読み取り、パフォーマンスが低下します。

カメラの他の特別な配慮を 1 つは、(たとえばシャッター スピード) カメラの設定に影響を与えるルート項目のプロパティです。 WIA サービスを呼び出すとき、アプリケーションでは、これらのプロパティを変更、 [ **IWiaMiniDrv::drvValidateItemProperties**](https://msdn.microsoft.com/library/windows/hardware/ff545017)します。 必要に応じて、プロパティの設定を検証する場合、ミニドライバーは、カメラと通信できます。 ただし、この関数は、別のアプリケーションはまた、プロパティを変更できるので、カメラの設定を変更する最適な場所にはありません。 ミニドライバーは、すべてのルート項目のプロパティからカメラの設定を更新する必要があるときに、 [ **IWiaMiniDrv::drvDeviceCommand** ](https://msdn.microsoft.com/library/windows/hardware/ff543967)関数が呼び出され、新しいイメージをキャプチャします。

 

 




