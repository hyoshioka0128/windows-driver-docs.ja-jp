---
title: アプリケーションで WIA デバイスを解放する方法
description: アプリケーションで WIA デバイスを解放する方法
ms.assetid: 694daed4-d794-4835-a052-27cc498baa10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56cf85562128ad23f02b6efbd77f78a8562de52a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840832"
---
# <a name="how-the-application-releases-the-wia-device"></a>アプリケーションで WIA デバイスを解放する方法





アプリケーションで WIA デバイスが不要になった場合は、 **Iwiaitem:: Release**メソッドが呼び出されます (Microsoft Windows SDK のドキュメントを参照してください)。 WIA 項目への最後の参照が解放されると、WIA サービスは[**IWiaMiniDrv::D rvuninitializewia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvuninitializewia)メソッドを呼び出します。 WIA ミニドライバーは、主に、接続されているすべてのアプリケーションに関連付けられたリソースの管理にこの方法を使用する必要があります。 アプリケーションを閉じると、その項目ツリーに関連付けられているリソースは不要になります。 WIA ミニドライバーは、 [**IWiaMiniDrv::D rvinitializewia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)の参照カウンターをインクリメントし、 **IWiaMiniDrv::d rvuninitializewia**でその参照カウンターをデクリメントすることで、接続されているすべてのアプリケーションを追跡する必要があります。 この時点でリソースを解放すると、接続されている他のアプリケーションで問題が発生する可能性があります。 参照カウンターが0になると、WIA ミニドライバーに接続されているアプリケーションがなくなります。 ミニドライバーは、アプリケーション接続中に取得した割り当て済みリソースをクリーンアップする必要があります。

**注**  * * * * **IWiaMiniDrv::d rvuninitializewia**メソッドはドライバーをアンロードしません。 イベントを処理するために、またはアプリケーションが通信するときに、ドライバーを再度呼び出すことができます。 このメソッドを呼び出すと、すべてのクライアントが切断されているわけではありません。 クライアント接続ごとに1回の呼び出しを行う必要があります。
**IWiaMiniDrv::D rvuninitializewia**メソッドへの各呼び出しは、 **IWiaMiniDrv::d rvinitializewia**メソッドへの対応する呼び出しとペアにする必要があります。

アプリケーションが現在接続され*ていない*と判断した場合を除いて、WIA ドライバーでは、このメソッド呼び出しのドライバーリソース*を解放しないでください*。

現在のアプリケーション接続数を特定するには、WIA ドライバーでクラスメンバー変数を参照カウンターとしてインクリメントして、 **IWiaMiniDrv::D rvinitializewia** (カウンターのインクリメント) と**IWiaMiniDrv:: のメソッド呼び出しを追跡します。drvUnInitializeWia** (カウンターをデクリメントする)。

 

**IWiaMiniDrv::D rvuninitializewia**メソッドの実装例を次に示します。

```cpp
HRESULT _stdcall CWIADevice::drvUnInitializeWia(BYTE *pWiasContext)
{
  //
  // If the caller did not pass in the correct parameters,
  // then fail the call with E_INVALIDARG.
  //

  if (!pWiasContext) {
      return E_INVALIDARG;
  }

  InterlockedDecrement(&m_lClientsConnected);

  //
  // make sure we never decrement below zero (0)
  //

  if(m_lClientsConnected < 0){
      m_lClientsConnected = 0;
  return S_OK;
  }

  //
  // check for connected applications.
  //

  if(m_lClientsConnected == 0){

      //
      // There are no application clients connected to this WIA driver
      //

  }

  return S_OK;
}
```

 

 




