---
title: WIA ミニドライバーの初期化
description: WIA ミニドライバーの初期化
ms.assetid: 9ccb136b-41f7-438a-9e07-1fd7c8971417
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ebe3adeaf9f9026d8d216fa6ef3b1d48d1cc0d8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366024"
---
# <a name="initializing-the-wia-minidriver"></a>WIA ミニドライバーの初期化





実装するには、まず、 [IWiaMiniDrv インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff545027)ミニドライバーを初期化し、ドライバーの項目の階層ツリーを作成します。 これは、WIA サービスの呼び出しを行う、 [ **IWiaMiniDrv::drvInitializeWia** ](https://msdn.microsoft.com/library/windows/hardware/ff544986)たびに、クライアント アプリケーションがデバイスを使用するメソッド。 2 つ以上のアプリケーションは、デバイスを使用して同時に、WIA サービスはアプリケーションごとにこのメソッドを呼び出します。 このメソッドで、ミニドライバー通常は、次の。

1.  WIA サービスから渡されたパラメーターを初期化します。

2.  によって示される、STI デバイス インターフェイス保存*pStiDevice します。* これは、ように、 [ **IStiDevice::LockDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff543756)と[ **IStiDevice::UnLockDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff543770)ロックまたはアンロック、WIA メソッドを使用できますデバイスです。

3.  キャッシュ*bstrDeviceID*と*bstrRootFullItemName*メンバー変数で、その他の方法で使用できるようにします。

4.  デバイスを識別するハンドルを開きます。 (この手順は、USB、SCSI、1394 などの非共有のポートの推奨が)。

5.  」の説明に従って、項目のツリーを構築[WIA ドライバーの項目のツリーを作成する](creating-the-wia-driver-item-tree.md)します。

**IWiaMiniDrv::drvInitializeWia**メソッドでくことも作成し、動的配列と、ドライバーを使用する構造体を初期化します。 たとえば、コマンドとイベントの後で使用して、ドライバーがサポートを作成できますが配列、 [ **IWiaMiniDrv::drvGetCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff543977)メソッド。

**注**   、 [ **IWiaMiniDrv::drvGetCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff543977)メソッドの前に呼び出す可能性があります**IWiaMiniDrv::drvInitializeWia**が呼び出されます。 これは、WIA サービスは、デバイスを使用して、アプリケーションが存在する前にイベント情報を照会する必要がある場合に発生します。 **IWiaMiniDrv::drvInitializeWia**アプリケーション通知デバイスを使用して目的を示す場合にのみ、メソッドが呼び出されます。

 

### <a name="keeping-track-of-application-connections"></a>アプリケーションの接続の管理

WIA サービスが、適切なドライバーを呼び出す前に述べた、アプリケーション、WIA デバイスと通信するときに、 [ **IWiaMiniDrv::drvInitializeWia** ](https://msdn.microsoft.com/library/windows/hardware/ff544986)メソッド。 WIA サービスが、適切なドライバーを呼び出すアプリケーションは、デバイスが終了し、して WIA への参照をすべて解放、 [ **IWiaMiniDrv::drvUnInitializeWia** ](https://msdn.microsoft.com/library/windows/hardware/ff545010)メソッド。 注 WIA を複数サポートしているアプリケーションの同時接続。 これは、2 つまたは複数のアプリケーションが同じデバイスに関連付けられた WIA インターフェイスを要求することを意味します。 必ずしも、ただし、ドライバーが同時要求を処理する必要があります。WIA サービスにより、その 1 つだけ要求は、一度にドライバーに送信されます。 ただし、WIA サービスを呼び出すことができます、 **IWiaMiniDrv::drvInitializeWia**メソッドを複数回呼び出す前に、 **IWiaMiniDrv::drvUnInitializeWia**メソッド。

この情報が便利な理由 多くの場合、アプリケーションが使用して、WIA ドライバーの項目のツリー、イメージのフィルター処理ライブラリ、およびその他のユーザーなどのドライバーが必要なリソースがあります。 これらのリソースは、大量のメモリを占有できます、ために、不要な場合は、それらをアンロードすることをお勧めします。

**注**   、 **IWiaMiniDrv::drvInitializeWia**と**IWiaMiniDrv::drvUnInitializeWia**メソッドを使用して、アプリケーションの接続のみのドライバーに通知します。 最初に呼び出さずには、その他のドライバー メソッドを呼び出すことができます、WIA サービス**IWiaMiniDrv::drvInitializeWia**、WIA サービスが必ずしも呼び出していないことを意味**IWiaMiniDrv::drvUnInitializeWia**ときに行われます。 呼び出されるメソッドは情報提供メソッドを必要としない、WIA 項目など[ **IWiaMiniDrv::drvGetCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff543977)と[ **IWiaMiniDrv::drvGetWiaFormatInfo**](https://msdn.microsoft.com/library/windows/hardware/ff543986).

 

このセクションでは、次のトピックについて説明します。

[ミニドライバー関数の順序を呼び出す](calling-order-for-minidriver-functions.md)

[読み込みとアンロード WIA ミニドライバー](loading-and-unloading-a-wia-minidriver.md)

[接続と切断の WIA アプリケーション](connecting-and-disconnecting-a-wia-application.md)

[WIA ミニドライバーの状態を報告](reporting-wia-minidriver-status.md)

 

 




