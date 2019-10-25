---
title: 項目ツリーの変更をアプリケーションに通知する
description: 項目ツリーの変更をアプリケーションに通知する
ms.assetid: 6b3cb1d0-ab9f-4895-8c3f-f66c398960bb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 964b8ad174393388f110839fda42c9078e578e38
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840820"
---
# <a name="informing-an-application-of-item-tree-changes"></a>項目ツリーの変更をアプリケーションに通知する





WIA デバイスのミニドライバーは、デバイスの項目ツリーに変更があった場合に、WIA デバイスに関連付けられているアプリケーションに通知できる必要があります。 たとえば、カメラ上の画像のサムネイルを示すユーザーインターフェイスをアプリケーションが表示した場合、WIA ミニドライバーは、ユーザーが既に削除した画像のサムネイルを表示しないように、アプリケーションのユーザーインターフェイスに通知する必要があります。

[**IWiaMiniDrv::D rvdevicecommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdevicecommand)メソッドの次の実装例では、wia サービスによって送信されたコマンドに wia ミニドライバーが応答する方法を示し、コマンドをデバイスに渡します。 WIA ミニドライバーがデバイスにコマンドを発行した後、ミニドライバーは、デバイス項目ツリーが変更されたことをアプリケーションに通知します。 この実装では、メソッドは、WIA サービスが "Take Picture" コマンドを発行したことを確認します (WIA\_CMD\_\_の画像を取得します)。 メソッドは、ルート項目 (デバイスの項目) に対して "表示される**画像**" メソッドを呼び出し、すべての接続されたアプリケーションに、項目ツリーに新しい画像が含まれていることを通知します。 (Microsoft Windows SDK のドキュメントでは、WIA\_CMD\_撮影\_画像を取得し、**画像**を撮ることができます)。ミニドライバーは、 [**Wiasqueueevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasqueueevent)関数を呼び出すことによってこれを行います。

ミニドライバーは、ツリーが更新されたことを示すイベントを送信するときに、呼び出し元だけでなく、*すべて*のリッスン中のアプリケーションに変更が通知されることに注意してください。 たとえば、ユーザーがカメラの [エクスプローラー] ビューを開いていて、Microsoft Paint を使用して新しい画像を取得した場合、[エクスプローラー] ウィンドウには、そのようなイベントをリッスンするため、新しい画像が届いたときにも表示されます。

**IWiaMiniDrv::D rvdevicecommand**メソッドの実装例を次に示します。

```cpp
HRESULT _stdcall CWIADevice::drvDeviceCommand(
  BYTE        *pWiasContext,
  LONG        lFlags,
  const GUID  *plCommand,
  IWiaDrvItem **ppWiaDrvItem,
  LONG        *plDevErrVal)
{
  //
  // If the caller did not pass in the correct parameters, 
  // then fail the call and return E_INVALIDARG.
  //

  if ((!pWiasContext)||(!plDevErrVal)||(!plCommand)) {
    return E_INVALIDARG;
  }

  *plDevErrVal = 0;
  HRESULT hr = E_NOTIMPL;

  //
  //  Check which command was issued
  //

  if (*plCommand == WIA_CMD_TAKE_PICTURE) {

    //
    // process command here
    //

      hr = HARDWARE_SNAP_PHOTO();
  }
  return hr;
}
```

 

 




