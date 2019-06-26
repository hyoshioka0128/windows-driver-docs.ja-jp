---
title: 項目ツリーの変更をアプリケーションに通知
description: 項目ツリーの変更をアプリケーションに通知
ms.assetid: 6b3cb1d0-ab9f-4895-8c3f-f66c398960bb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eaa1c9568a9154975c92ae5db53a098b3367e55f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378947"
---
# <a name="informing-an-application-of-item-tree-changes"></a>項目ツリーの変更をアプリケーションに通知





WIA デバイス用のミニドライバーは、デバイスの項目のツリーへの変更の WIA デバイスに関連付けられているアプリケーションに通知できる必要があります。 たとえば、アプリケーションでは、カメラで画像のサムネイルを示すユーザー インターフェイスが表示されている場合、WIA ミニドライバーは、ユーザーが既に削除されている画像のサムネイルを表示しないアプリケーションのユーザー インターフェイスを通知することのようになります。

次のサンプル実装、 [ **IWiaMiniDrv::drvDeviceCommand** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdevicecommand)メソッド WIA ミニドライバーが、WIA サービスによって送信されたコマンドに応答し、デバイスにコマンドを渡す方法を示しています。 WIA ミニドライバーは、デバイスにコマンドを発行、ミニドライバーは、アプリケーション、デバイスの項目のツリーが変更されたことを通知します。 この実装で、メソッドを判断、WIA サービスが「画像の撮影」コマンドを発行する (WIA\_CMD\_かかる\_画像)。 メソッドの呼び出し、 **TakePicture**ルート上のメソッドは、項目 (デバイスの項目) と、項目のツリーが新しい画像には今すぐが含まれているすべての接続されているアプリケーションに通知します。 (両方 WIA\_CMD\_かかる\_画像と**TakePicture** Microsoft Windows SDK ドキュメントに記載されています)。ミニドライバーは呼び出すことによって、 [ **wiasQueueEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasqueueevent)関数。

ミニドライバーは、ツリーが更新されたことを示すイベントを送信する場合は注意*すべて*呼び出し元だけでなく、変更のリッスンしているアプリケーションが通知されます。 たとえば、ユーザーが開いている場合は、カメラのエクスプ ローラーのビューがあります、Microsoft ペイントを使用して、新しい画像を取得する場合は、エクスプ ローラー ウィンドウも画像が表示新しい到着した時点でこのようなイベントをリッスンするため。

次の例の実装を示しています、 **IWiaMiniDrv::drvDeviceCommand**メソッド。

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

 

 




