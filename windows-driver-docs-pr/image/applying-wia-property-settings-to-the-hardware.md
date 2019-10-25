---
title: WIA プロパティ設定のハードウェアへの適用
description: WIA プロパティ設定のハードウェアへの適用
ms.assetid: adb85f77-1814-427b-8b75-0bfce4c8ca06
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc54a559c2405203c396ddc6f16ec4e0463c6f3a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840895"
---
# <a name="applying-wia-property-settings-to-the-hardware"></a>WIA プロパティ設定のハードウェアへの適用





Wia アプリケーションでデータ転送が開始されると、wia サービスによって、現在の WIA プロパティ設定を適用し、デバイス固有の設定をハードウェアに適用する機会が WIA ミニドライバーに与えられます。 次に、 [**IWiaMiniDrv::D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)メソッドを呼び出す前に、WIA サービスが[**IWiaMiniDrv::d rvwriteitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties)メソッドを呼び出します。 後者の方法は、WIA アプリケーションでデータ転送が開始された場合にのみ呼び出されます。 WIA ミニドライバーは、WIA サービスの機能を使用して、独自のドライバー項目ツリー内のプロパティを読み取る必要があります。

### <a href="" id="implementing-iwiaminidrv-drvwriteitemproperties"></a>IWiaMiniDrv の実装::d rvWriteItemProperties

クライアントがデータ転送を要求した後、WIA サービスは**IWiaMiniDrv::D rvwriteitemproperties**メソッドを呼び出します。 [**IWiaMiniDrv::D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)の呼び出しを行う前に、WIA サービスはこのメソッドを呼び出します。 WIA ミニドライバーは、このメソッドから戻る前に、ハードウェアに必要なすべての設定をコミットする必要があります。

このメソッドが呼び出されると、データ転送を実行するために、WIA ミニドライバーがコミットされました。 Wia サービスは、この時点でデータを取得しようとするすべてのアプリケーションが、WIA\_エラー\_ビジーエラーコードで失敗します。

次の例は、 [**IWiaMiniDrv::D rvwriteitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties)メソッドの実装を示しています。

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

 

 




