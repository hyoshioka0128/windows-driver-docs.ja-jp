---
title: アプリケーションで WIA デバイスを解放する方法
description: アプリケーションで WIA デバイスを解放する方法
ms.assetid: 694daed4-d794-4835-a052-27cc498baa10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f183d4e1b6996e6be4f6f9179e4449dbcc886b2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578521"
---
# <a name="how-the-application-releases-the-wia-device"></a>アプリケーションで WIA デバイスを解放する方法





アプリケーションに WIA デバイスの必要がない場合は、呼び出し、 **IWiaItem::Release**メソッド (Microsoft Windows SDK のドキュメントで説明)。 WIA アイテムには、最後の参照が解放されるときに、WIA サービスの呼び出し、 [ **IWiaMiniDrv::drvUnInitializeWia** ](https://msdn.microsoft.com/library/windows/hardware/ff545010)メソッド。 WIA ミニドライバーは、接続されているすべてのアプリケーションに関連付けられているリソースを管理するには、主に、このメソッドを使用する必要があります。 アプリケーションを閉じるときに、その項目のツリーに関連付けられているリソースは必要なくなりました。 WIA ミニドライバーはの追跡接続されているすべてのアプリケーションでの参照カウンターをインクリメントして[ **IWiaMiniDrv::drvInitializeWia** ](https://msdn.microsoft.com/library/windows/hardware/ff544986)およびでカウンターを参照するデクリメント**IWiaMiniDrv::drvUnInitializeWia**します。 この時点でリソースを解放すると、接続されている他のアプリケーションの問題が生じる場合があります。 参照カウンターがゼロに達するほかのアプリケーションに接続されます WIA ミニドライバー。 ミニドライバーは、アプリケーションの接続中に取得した、割り当てられたリソースをクリーンアップする必要があります。

**注**  * * *、 **IWiaMiniDrv::drvUnInitializeWia**メソッドは、ドライバーをアンロードしません。 イベントの処理にドライバーをもう一度呼び出すことが、アプリケーションが通信しようとした場合またはします。 このメソッドの呼び出しでは、すべてのクライアントが切断されているとは限りません。 クライアントの切断あたり 1 回の呼び出しが必要です。
呼び出しごとに、 **IWiaMiniDrv::drvUnInitializeWia**に対応する呼び出しとメソッドのペアを設定する必要があります、 **IWiaMiniDrv::drvInitializeWia**メソッド。

WIA ドライバーにする必要があります*いない*を安全に判断できる場合を除き、このメソッドの呼び出しのすべてのドライバー リソースを解放*ありません*アプリケーションが現在接続されています。

現在のアプリケーション接続の数を確認するのに WIA ドライバーは、メソッド呼び出しを追跡する参照カウンターとしてクラスのメンバー変数をインクリメントする必要があります**IWiaMiniDrv::drvInitializeWia** (カウンターをインクリメントする)**IWiaMiniDrv::drvUnInitializeWia** (カウンターをデクリメントする操作)。

 

次の例の実装を示しています、 **IWiaMiniDrv::drvUnInitializeWia**メソッド。

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

 

 




