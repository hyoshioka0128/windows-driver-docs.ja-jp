---
title: WIA ミニドライバーの初期化
description: WIA ミニドライバーの初期化
ms.assetid: 9ccb136b-41f7-438a-9e07-1fd7c8971417
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3af688c22e8e686bd1362a440e9fe315776ca96a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378941"
---
# <a name="initializing-the-wia-minidriver"></a>WIA ミニドライバーの初期化





実装するには、まず、 [IWiaMiniDrv インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)ミニドライバーを初期化し、ドライバーの項目の階層ツリーを作成します。 これは、WIA サービスの呼び出しを行う、 [ **IWiaMiniDrv::drvInitializeWia** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)たびに、クライアント アプリケーションがデバイスを使用するメソッド。 2 つ以上のアプリケーションは、デバイスを使用して同時に、WIA サービスはアプリケーションごとにこのメソッドを呼び出します。 このメソッドで、ミニドライバー通常は、次の。

1.  WIA サービスから渡されたパラメーターを初期化します。

2.  によって示される、STI デバイス インターフェイス保存*pStiDevice します。* これは、ように、 [ **IStiDevice::LockDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-lockdevice)と[ **IStiDevice::UnLockDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-unlockdevice)ロックまたはアンロック、WIA メソッドを使用できますデバイスです。

3.  キャッシュ*bstrDeviceID*と*bstrRootFullItemName*メンバー変数で、その他の方法で使用できるようにします。

4.  デバイスを識別するハンドルを開きます。 (この手順は、USB、SCSI、1394 などの非共有のポートの推奨が)。

5.  」の説明に従って、項目のツリーを構築[WIA ドライバーの項目のツリーを作成する](creating-the-wia-driver-item-tree.md)します。

**IWiaMiniDrv::drvInitializeWia**メソッドでくことも作成し、動的配列と、ドライバーを使用する構造体を初期化します。 たとえば、コマンドとイベントの後で使用して、ドライバーがサポートを作成できますが配列、 [ **IWiaMiniDrv::drvGetCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)メソッド。

**注**   、 [ **IWiaMiniDrv::drvGetCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)メソッドの前に呼び出す可能性があります**IWiaMiniDrv::drvInitializeWia**が呼び出されます。 これは、WIA サービスは、デバイスを使用して、アプリケーションが存在する前にイベント情報を照会する必要がある場合に発生します。 **IWiaMiniDrv::drvInitializeWia**アプリケーション通知デバイスを使用して目的を示す場合にのみ、メソッドが呼び出されます。

 

### <a name="keeping-track-of-application-connections"></a>アプリケーションの接続の管理

WIA サービスが、適切なドライバーを呼び出す前に述べた、アプリケーション、WIA デバイスと通信するときに、 [ **IWiaMiniDrv::drvInitializeWia** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)メソッド。 WIA サービスが、適切なドライバーを呼び出すアプリケーションは、デバイスが終了し、して WIA への参照をすべて解放、 [ **IWiaMiniDrv::drvUnInitializeWia** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvuninitializewia)メソッド。 注 WIA を複数サポートしているアプリケーションの同時接続。 これは、2 つまたは複数のアプリケーションが同じデバイスに関連付けられた WIA インターフェイスを要求することを意味します。 必ずしも、ただし、ドライバーが同時要求を処理する必要があります。WIA サービスにより、その 1 つだけ要求は、一度にドライバーに送信されます。 ただし、WIA サービスを呼び出すことができます、 **IWiaMiniDrv::drvInitializeWia**メソッドを複数回呼び出す前に、 **IWiaMiniDrv::drvUnInitializeWia**メソッド。

この情報が便利な理由 多くの場合、アプリケーションが使用して、WIA ドライバーの項目のツリー、イメージのフィルター処理ライブラリ、およびその他のユーザーなどのドライバーが必要なリソースがあります。 これらのリソースは、大量のメモリを占有できます、ために、不要な場合は、それらをアンロードすることをお勧めします。

**注**   、 **IWiaMiniDrv::drvInitializeWia**と**IWiaMiniDrv::drvUnInitializeWia**メソッドを使用して、アプリケーションの接続のみのドライバーに通知します。 最初に呼び出さずには、その他のドライバー メソッドを呼び出すことができます、WIA サービス**IWiaMiniDrv::drvInitializeWia**、WIA サービスが必ずしも呼び出していないことを意味**IWiaMiniDrv::drvUnInitializeWia**ときに行われます。 呼び出されるメソッドは情報提供メソッドを必要としない、WIA 項目など[ **IWiaMiniDrv::drvGetCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)と[ **IWiaMiniDrv::drvGetWiaFormatInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo).

 

このセクションでは、次のトピックについて説明します。

[ミニドライバー関数の順序を呼び出す](calling-order-for-minidriver-functions.md)

[読み込みとアンロード WIA ミニドライバー](loading-and-unloading-a-wia-minidriver.md)

[接続と切断の WIA アプリケーション](connecting-and-disconnecting-a-wia-application.md)

[WIA ミニドライバーの状態を報告](reporting-wia-minidriver-status.md)

 

 




