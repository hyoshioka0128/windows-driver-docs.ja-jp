---
title: WIA プロパティ設定のハードウェアへの適用
description: WIA プロパティ設定のハードウェアへの適用
ms.assetid: adb85f77-1814-427b-8b75-0bfce4c8ca06
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67fda89e59039903db39b9c63feae35747fb96ca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373342"
---
# <a name="applying-wia-property-settings-to-the-hardware"></a>WIA プロパティ設定のハードウェアへの適用





WIA アプリケーションを開始すると、データ転送、WIA サービスは、WIA プロパティの現在の設定を適用し、ハードウェアに任意のデバイスに固有の設定を適用する WIA ミニドライバーを示します。 サービスからの呼び出しの WIA、 [ **IWiaMiniDrv::drvWriteItemProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff545020)メソッドを呼び出す前に、 [ **IWiaMiniDrv::drvAcquireItemData** ](https://msdn.microsoft.com/library/windows/hardware/ff543956)メソッド。 WIA アプリケーションは、データ転送を開始する場合にのみ、後者のメソッドが呼び出されます。 WIA ミニドライバーは、ドライバー項目ツリー内のプロパティを読み取る WIA サービス関数を使用する必要があります。

### <a href="" id="implementing-iwiaminidrv-drvwriteitemproperties"></a>IWiaMiniDrv::drvWriteItemProperties を実装します。

WIA サービスの呼び出し、 **IWiaMiniDrv::drvWriteItemProperties**後に、クライアントは、データ転送を要求します。 WIA サービスが呼び出しを実行する前に、このメソッドを呼び出す[ **IWiaMiniDrv::drvAcquireItemData**](https://msdn.microsoft.com/library/windows/hardware/ff543956)します。 WIA ミニドライバーは、このメソッドから戻る前に、ハードウェアに必要なすべての設定をコミットする必要があります。

このメソッドが呼び出されると、WIA ミニドライバーにコミットされたデータ転送を実行します。 WIA サービスには、WIA をこの時点でデータを取得しようとする任意のアプリケーションは失敗\_エラー\_ビジー状態のエラー コード。

次の例の実装を示しています、 [ **IWiaMiniDrv::drvWriteItemProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff545020)メソッド。

```cpp
HRESULT _stdcall CWIADevice::drvWriteItemProperties(
  BYTE                      *pWiasContext,
  LONG                      lFlags,
  PMINIDRV_TRANSFER_CONTEXT pmdtc,
  LONG                      *plDevErrVal)
{
  //
  // If the caller did not pass in the correct parameters,
  // then fail the call with E_INVALIDARG.
  //

  if (!pWiasContext) {
      return E_INVALIDARG;
  }

 if (!pmdtc) {
      return E_INVALIDARG;
  }

  if (!plDevErrVal) {
      return E_INVALIDARG;
  }

  HRESULT hr = S_OK;
  *plDevErrVal = 0;
  PROPVARIANT pv[2];
  PROPSPEC ps[2] = {
      {PRSPEC_PROPID, WIA_IPS_XRES},
      {PRSPEC_PROPID, WIA_IPS_YRES}
  };

  //
  // initialize propvariant structures
  //

  pv[0].vt = VT_I4;   // X resolution is a LONG value
  pv[1].vt = VT_I4;   // Y resolution is a LONG value

  //
  // read 2 WIA item properties (X and Y resolution)
  //

  hr = wiasReadMultiple(pWiasContext, 2, ps, pv, NULL);

  if (hr == S_OK) {

    //
    // write current X and Y resolution values, read from the
    // the WIA property set, and write them to the device.
    //

      hr = SetMyDeviceXResolution(pv[0].lVal);
      if(S_OK == hr) {
          hr = SetMyDeviceYResolution(pv[1].lVal);
          if(FAILED(hr)) {

            //
            // could not set Y resolution to device
            //

          }
   } else {

        //
        // could not set X resolution to device
        //

      }
  }
  return hr;
}
```

 

 




