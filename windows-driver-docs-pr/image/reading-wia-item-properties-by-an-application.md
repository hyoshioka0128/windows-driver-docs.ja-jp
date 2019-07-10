---
title: アプリケーションによる WIA 項目のプロパティの読み取り
description: アプリケーションによる WIA 項目のプロパティの読み取り
ms.assetid: e09f604e-451e-40dc-bc12-a077d4d263ee
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4354291206d0996660b9103cd83949b521f7200
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716832"
---
# <a name="reading-wia-item-properties-by-an-application"></a>アプリケーションによる WIA 項目のプロパティの読み取り





アプリケーション要求 WIA 項目のプロパティを読み取ると、WIA サービスを呼び出し、 [ **IWiaMiniDrv::drvReadItemProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties)メソッド。

**IWiaMiniDrv::drvReadItemProperties**メソッドは、次のタスクを実行する必要があります。

1.  プロパティの読み取り中に実行時の更新プログラムが必要かどうかを決定します。 WIA プロパティが読み取られるを確認するのには、WIA ミニドライバーは (Microsoft Windows SDK のドキュメントで定義されている) PROPSPEC 配列を使用できます。 WIA ミニドライバーが PROPSPEC 配列を処理する前に、項目の種類を決定することをお勧めします。 これで配列を走査する必要性が軽減すべて**IWiaMiniDrv::drvReadItemProperties**を呼び出します。 このデバイスの子項目の実行時のプロパティがない場合、のみのルート項目のプロパティでは、要求が処理する読み取り専用です。

2.  呼び出すことによって、現在の値を更新、 [ **wiasWriteMultiple** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritemultiple)または**wiasWriteProp**_Xxx_サービス、WIA を使用して、すべての機能プロパティの id。 これにより、更新、ドライバー項目に格納されている、WIA プロパティ セットと、WIA サービスは、アプリケーションに新しい値を返します。

WIA ミニドライバーがこの関数で WIA プロパティに、実行時の調整を実行しない場合、WIA サービスは自動的にアプリケーションに現在の WIA のプロパティ値のみを返します。 この関数は、デバイスの時計などのプロパティまたはドキュメント フィーダーの状態などのハードウェア固有のチェックを必要とする WIA プロパティに対してのみ使用する必要があります。

### <a href="" id="implementing-iwiaminidrv--drvreaditemproperties-"></a>IWiaMiniDrv::drvReadItemProperties を実装します。

**IWiaMiniDrv::drvReadItemProperties**アプリケーションが、WIA 項目のプロパティの読み取りを試みると、メソッドが呼び出されます。 最初、WIA サービスは、このメソッドを呼び出すことによって、ドライバーを通知します。 WIA ドライバーでは、読み取られるプロパティが正しいことを確認する必要があります。 これは、デバイスの状態を必要とするプロパティをハードウェアにアクセスするに適して (など[ **WIA\_DPS\_ドキュメント\_処理\_状態**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-status)、または[ **WIA\_DPA\_デバイス\_時間**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dpa-device-time)デバイスは、クロックをサポートしている場合)。

ことが重要なまれな状況でのみ、WIA ドライバーが、ハードウェアと通信する必要があることに注意してください。 WIA ドライバーと通信するハードウェアも遅くおよび低速この呼び出しで多く表示されます。

次の例の実装を示しています、 [ **IWiaMiniDrv::drvReadItemProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties)メソッド。

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

 

 




