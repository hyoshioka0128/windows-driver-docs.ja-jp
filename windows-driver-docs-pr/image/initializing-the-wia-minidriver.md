---
title: WIA ミニドライバーの初期化
description: WIA ミニドライバーの初期化
ms.assetid: 9ccb136b-41f7-438a-9e07-1fd7c8971417
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3920242e4c98a4e7067e53376c1c237b6fea95e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840818"
---
# <a name="initializing-the-wia-minidriver"></a>WIA ミニドライバーの初期化





[IWiaMiniDrv インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)を実装するための最初の手順は、ミニドライバーを初期化し、ドライバー項目の階層ツリーを作成することです。 これを行うために、WIA サービスは、クライアントアプリケーションがデバイスを使用するたびに[**IWiaMiniDrv::D rvinitializewia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)メソッドを呼び出します。 デバイスを同時に使用しているアプリケーションが2つ以上ある場合、WIA サービスはアプリケーションごとにこのメソッドを呼び出します。 このメソッドでは、ミニドライバーは通常、次のことを行います。

1.  WIA サービスから渡されたパラメーターを初期化します。

2.  *Parp デバイス*が指す STI デバイスインターフェイスを保存します。 これにより、 [**IUnLockDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-lockdevice)メソッドを使用して、WIA デバイス[](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-unlockdevice)のロックまたはロック解除を行うことができるようになります。

3.  他のメソッドで使用できるように、 *Bstrdeviceid*と*bstrRootFullItemName*をメンバー変数にキャッシュします。

4.  デバイスへのハンドルを開きます。 (USB、SCSI、1394などの非共有ポートでは、この手順をお勧めします)。

5.  「 [WIA ドライバー項目ツリーの作成](creating-the-wia-driver-item-tree.md)」で説明されているように、項目ツリーを構築します。

**IWiaMiniDrv::D rvinitializewia**メソッドを使用して、ドライバーが使用する動的な配列および構造体を作成し、初期化することもできます。 たとえば、 [**IWiaMiniDrv::D rvgetcapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)メソッドで後で使用するために、ドライバーがサポートするコマンドとイベントの配列を作成できます。

[**IWiaMiniDrv::D rvgetcapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)メソッドは、 **IWiaMiniDrv::d rvinitializewia**が呼び出される前に呼び出される場合があることに**注意**してください  。 これは、デバイスを使用するアプリケーションが存在する前に、WIA サービスがイベント情報を照会する必要がある場合に発生する可能性があります。 **IWiaMiniDrv::D rvinitializewia**メソッドは、アプリケーションがデバイスを使用することを目的としている場合にのみ呼び出されます。

 

### <a name="keeping-track-of-application-connections"></a>アプリケーション接続の追跡

前述のように、アプリケーションが WIA デバイスと通信する場合、WIA サービスは適切なドライバーの[**IWiaMiniDrv::D rvinitializewia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)メソッドを呼び出します。 アプリケーションがデバイスで終了し、それに対するすべての WIA 参照が解放されると、WIA サービスは適切なドライバーの[**IWiaMiniDrv::D rvuninitializewia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvuninitializewia)メソッドを呼び出します。 WIA では、複数の同時アプリケーション接続がサポートされていることに注意してください。 これは、2つ以上のアプリケーションが同じデバイスに関連付けられた WIA インターフェイスを要求できることを意味します。 ただし、ドライバーが同時要求を処理する必要があることを意味するわけではありません。WIA サービスにより、一度に1つの要求だけがドライバーに送信されるようになります。 ただし、WIA サービスでは、 **IWiaMiniDrv::D rvuninitializewia**メソッドを呼び出す前に、 **IWiaMiniDrv::d rvinitializewia**メソッドを複数回呼び出すことができます。

この情報が役に立つのはなぜですか。 多くの場合、WIA ドライバーの項目ツリー、イメージのフィルター処理ライブラリなど、アプリケーションが使用するときにドライバーが必要とするリソースがあります。 これらのリソースは大量のメモリを占有する可能性があるため、不要になったときにアンロードすることをお勧めします。

**IWiaMiniDrv::D rvinitializewia**メソッドと**IWiaMiniDrv::d**メソッドを使用して、アプリケーション接続のみを**記録**するように   します。 最初に**IWiaMiniDrv::D rvinitializewia**を呼び出さなくても、wia サービスは他のドライバーメソッドを呼び出すことができます。つまり、完了時には、必ずしも**IWiaMiniDrv::d rvuninitializewia**を呼び出すことはありません。 呼び出されるメソッドは、 [**IWiaMiniDrv::D rvgetcapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)や[**IWiaMiniDrv::d RVGETWIAFORMATINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo)など、WIA 項目を必要としない情報メソッドです。

 

このセクションでは、次のトピックについて説明します。

[ミニドライバー Functions の呼び出し順序](calling-order-for-minidriver-functions.md)

[WIA ミニドライバーの読み込みとアンロード](loading-and-unloading-a-wia-minidriver.md)

[WIA アプリケーションの接続と切断](connecting-and-disconnecting-a-wia-application.md)

[WIA ミニドライバーの状態の報告](reporting-wia-minidriver-status.md)

 

 




