---
title: アプリケーションによる WIA 項目のプロパティの読み取り
description: アプリケーションによる WIA 項目のプロパティの読み取り
ms.assetid: e09f604e-451e-40dc-bc12-a077d4d263ee
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a19af7d39c3d80b0c341e17b35f1a9d07e5bb24a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840761"
---
# <a name="reading-wia-item-properties-by-an-application"></a>アプリケーションによる WIA 項目のプロパティの読み取り





アプリケーションが WIA 項目のプロパティを読み取る要求を行うと、WIA サービスは[**IWiaMiniDrv::D rvreaditemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties)メソッドを呼び出します。

**IWiaMiniDrv::D rvreaditemproperties**メソッドでは、次のタスクを実行する必要があります。

1.  読み取り中のプロパティにランタイムの更新が必要かどうかを判断します。 どの WIA プロパティが読み取られているかを判断するために、WIA ミニドライバーは PROPSPEC 配列 (Microsoft Windows SDK ドキュメントで定義されています) を使用できます。 PROPSPEC 配列を処理する前に、WIA ミニドライバーが項目の種類を決定することをお勧めします。 これにより、すべての**IWiaMiniDrv::D rvreaditemproperties**呼び出しで配列を走査する必要性が軽減されます。 このデバイスの子項目に実行時プロパティがない場合は、ルート項目のプロパティ読み取り要求だけが処理されます。

2.  WIA プロパティの ID を使用して、 [**wiasWriteMultiple**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritemultiple)または**Wiaswriteprop**_Xxx_サービス関数を呼び出すことにより、現在の値を更新します。 これにより、ドライバー項目に格納されている WIA プロパティセットが更新され、WIA サービスによって新しい値がアプリケーションに返されます。

この関数で wia ミニドライバーが WIA プロパティの実行時調整を実行しない場合、WIA サービスは、現在の WIA プロパティ値のみをアプリケーションに自動的に返します。 この関数は、デバイスクロックなどのプロパティや、ドキュメントフィーダーの状態など、ハードウェア固有のチェックを必要とする WIA プロパティに対してのみ使用してください。

### <a href="" id="implementing-iwiaminidrv--drvreaditemproperties-"></a>IWiaMiniDrv の実装::d rvReadItemProperties

**IWiaMiniDrv::D rvreaditemproperties**メソッドは、アプリケーションが WIA 項目のプロパティを読み取ろうとしたときに呼び出されます。 最初に、このメソッドを呼び出して、WIA サービスがドライバーに通知します。 WIA ドライバーは、読み取られているプロパティが正しいことを確認する必要があります。 これは、デバイスの状態を必要とするプロパティのハードウェアにアクセスするのに適しています ( [**wia\_DPS\_ドキュメント\_\_の状態を処理**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-status)したり、デバイスがある場合は、 [**wia\_DPA\_デバイス\_時刻**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dpa-device-time)など)。時計をサポートします)。

WIA ドライバーは、まれな場合にのみハードウェアと通信する必要があることに注意してください。 この呼び出しでは、ハードウェアと通信する WIA ドライバーの動作が遅く、低速であると表示されます。

次の例は、 [**IWiaMiniDrv::D rvreaditemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties)メソッドの実装を示しています。

```cpp
HRESULT _stdcall CWIADevice::drvReadItemProperties(
  BYTE           *pWiasContext,
  LONG           lFlags,
  ULONG          nPropSpec,
  const PROPSPEC *pPropSpec,
  LONG           *plDevErrVal)
{

  //
  // If the caller did not pass in the correct parameters,
  // then fail the call with E_INVALIDARG.
  //

  if (!pWiasContext) {
      return E_INVALIDARG;
  }

  if (!plDevErrVal) {
      return E_INVALIDARG;
  }

  if (!pPropSpec) {
      return E_INVALIDARG;
  }

  *plDevErrVal = 0;

  LONG lWIAItemType = 0;
  HRESULT hr = wiasGetItemType(pWiasContext,&lWIAItemType);
  if(S_OK == hr) {
    //
    // perform custom operations depending on the type of
    // WIA item that was passed to drvReadItemProperties
    //

      if(lWIAItemType & WiaItemTypeRoot) {
      //
      // If the WIA_DPA_CONNECT_STATUS property ID is in the PROPSPEC
      // array, then read the latest "Connect Status".
      // If it is NOT then do nothing. (skip access to the hardware)
      //
      // NOTE: only read properties contained in the PROPSPEC array
      //     from the hardware that need device updates.
      //     If the property in PROPSPEC does not need to be read
      //     from the hardware, or updated, do nothing. The WIA service
      //     will supply the caller with the current value in the
      //     the WIA property set.
      //

          BOOL bReadLatestConnectStatus = FALSE;

      //
      // traverse the WIA PROPSPEC array, looking for known WIA
      // properties that require run-time updates, or needs to be
      // updated with hardware access.
      //

          for(ULONG ulIndex = 0; ulIndex < nPropSpec; ulIndex++) {

        //
        // look for WIA property IDs that really need hardware
        // access, or run-time adjusting.
        //

              if(pPropSpec[ulIndex].propid == WIA_DPA_CONNECT_STATUS) {
                  bReadLatestConnectStatus = TRUE;
              }
          }

        //
        // The item passed in is a ROOT item
        //

         if(bReadLatestConnectStatus) {

            //
            // WIA_DPA_CONNECT_STATUS should be updated from the
            // hardware
            //

 LONG lConnectStatus = HARDWARE_READ_ConnectStatus();

            //
            // update WIA_DPA_CONNECT_STATUS property value using
            // wiasWritePropLong ().  The pWiasContext passed in
            // already represents the current item to be written to.
            //

              hr = wiasWritePropLong(pWiasContext,WIA_DPA_CONNECT_STATUS,lConnectStatus);
              if(S_OK == hr) {

                //
                // The WIA_DPA_CONNECT_STATUS property was successfully updated
                //

              } else {

                //
                //  wiasWritePropLong() failed to write the WIA 
                //  property.  The WIA_DPA_CONNECT_STATUS
                //  property was NOT updated
                //

              }
          }

      } else {

        //
        // The item passed in is any other child item
        //

      }
  } else {

    //
    // wiasGetItemType() failed to get the current item type
    //
  }

  return hr;
}
```

 

 




