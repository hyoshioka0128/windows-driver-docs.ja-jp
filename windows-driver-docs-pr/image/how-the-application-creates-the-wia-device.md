---
title: アプリケーションで WIA デバイスを作成する方法
description: アプリケーションで WIA デバイスを作成する方法
ms.assetid: f4268c61-11e5-4796-b7cb-80c8112be4d8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64bd865a52fe598e44ee7802e21bdd502b38e412
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840834"
---
# <a name="how-the-application-creates-the-wia-device"></a>アプリケーションで WIA デバイスを作成する方法





アプリケーションで WIA デバイスドライバーを使用する場合は、 **Iwiadevmgr:: CreateDevice**メソッドを呼び出します (Microsoft Windows SDK のドキュメントを参照してください)。 WIA サービスは、最初に[**iexclusive usd:: LockDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-lockdevice)を呼び出して、同時に排他的にアクセスできるように wia ドライバーをロックします。 次に、WIA サービスは[**IWiaMiniDrv::D rvinitializewia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)を呼び出して、最初の wia 項目ツリー構造を作成します。 最後に、WIA サービスは[**Istiusd:: UnLockDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-unlockdevice)を呼び出すことによって、デバイスドライバーのロックを解除します。

**IWiaMiniDrv::D rvinitializewia**メソッドでは、次のタスクを実行する必要があります。

1.  *Parp デバイス*パラメーターが指すインターフェイスをキャッシュして、適切なデバイスロックを行います。 (詳細については、「 [**IWiaMiniDrv::D rvlockwiadevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvlockwiadevice)」を参照してください)。

2.  最初の WIA 項目ツリー構造を作成します。

3.  現在のアプリケーション接続数をインクリメントします。 この数は、アプリケーションがまだ接続されているかどうかをドライバーに通知するために使用されます。 また、 [**IWiaMiniDrv::D rvuninitializewia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvuninitializewia)で実行する適切なアクションを決定するのにも役立ちます。

WIA 項目は、論理的な意味を持つ名前にする必要があります。 Microsoft では、Windows XP 以降では次の項目名を必要とします。

<a href="" id="root"></a>**ルート**  
これは、WIA 項目ツリーのルート項目の用語です。

<a href="" id="flatbed"></a>**ベッド**  
これは、フラットベッドスキャナーのみをサポートするスキャナー、またはドキュメントフィーダーを備えたフラットベッドスキャナーをサポートするスキャナーの用語です。

<a href="" id="feeder"></a>**フィーダー**  
これは、フィーダーだけをサポートするスキャナーの用語です。

WIA サービスは、 **IWiaMiniDrv::D rvinitializewia**メソッドを呼び出します。このメソッドは、wia アプリケーションの**Iwiadevmgr:: CreateDevice**への呼び出しに応答しています (Windows SDK のドキュメントを参照)。 この結果、新しいクライアント接続ごとに、WIA サービスが**IWiaMiniDrv::D rvinitializewia**メソッドを呼び出すことになります。

**IWiaMiniDrv::D rvinitializewia**メソッドは、プライベート構造体を初期化し、ドライバー項目ツリーを作成する必要があります。 [ドライバー] 項目ツリーには、この WIA デバイスでサポートされているすべての WIA 項目のレイアウトが表示されます。 このメソッドは、コンテンツ (WIA プロパティ) では*なく*、初期ツリー構造のみを作成するために使用されます。 Wia サービスは、 [**IWiaMiniDrv::D rvinititemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinititemproperties)メソッドを複数回呼び出すことによって、wia ドライバー項目の wia プロパティを個別に設定します。

すべての WIA デバイスには、すべての WIA デバイス項目の親であるルート項目があります。 Wia デバイス項目を作成するには、wia ドライバーが WIA サービスヘルパー関数[**wiasCreateDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)を呼び出す必要があります。

次の例は、WIA デバイスのルート項目を作成する方法を示しています。

```cpp
LONG lItemFlags = WiaItemTypeFolder|WiaItemTypeDevice|WiaItemTypeRoot;
IWiaDrvItem  *pIWiaDrvRootItem  = NULL;
HRESULT hr = 
    wiasCreateDrvItem(
                       lItemFlags, // item flags
                       bstrRootItemName, // item name ("Root")
                       bstrRootFullItemName, // item full name ("0000\Root")
                      (IWiaMiniDrv *)this, // this WIA driver object
                       sizeof(MINIDRIVERITEMCONTEXT), // size of context
                       NULL, // context
                       &pIWiaDrvRootItem // created ROOT item
                      );                 // (IWiaDrvItem interface)

if(S_OK == hr){

  //
  // ROOT item was created successfully
  //

 }
```

前の例で作成したルート項目の直下にある WIA 子項目を作成するには、次のようなコードを使用します。

**注**  * * * * [**IWiaDrvItem:: AddItemToFolder**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-additemtofolder)メソッドが呼び出され、新しく作成された子項目がルート項目に追加されていることに注意してください。

 

```cpp
LONG lItemFlags = WiaItemTypeFile|WiaItemTypeDevice|WiaItemTypeImage;
PMINIDRIVERITEMCONTEXT pItemContext    = NULL;
IWiaDrvItem           *pIWiaDrvNewItem = NULL;
HRESULT hr = 
    wiasCreateDrvItem(
                       lItemFlags, // item flags
                       bstrItemName,  // item name ("Flatbed")
                       bstrFullItemName,  // item full name ("0000\Root\Flatbed")
                      (IWiaMiniDrv *)this,  // this WIA driver object
     sizeof(MINIDRIVERITEMCONTEXT), // size of context
                      (PBYTE)&pItemContext, // context
                      &pIWiaDrvNewItem // created child item
                     );                // (IWiaDrvItem interface)  

if(S_OK == hr){

  //
  // A New WIA driver item was created successfully
  //

  hr = pIWiaDrvNewItem->AddItemToFolder(pIWiaDrvRootItem); // add the new item to the ROOT
  if(S_OK == hr){

     //
     // successfully created and added a new WIA driver item to 
     // the WIA driver item tree.
    //

   }
   pNewItem->Release();
   pNewItem = NULL;
 }
```

**IWiaMiniDrv::D rvinitializewia**メソッドの実装例を次に示します。

```cpp
HRESULT _stdcall CWIADevice::drvInitializeWia(
  BYTE        *pWiasContext,
  LONG        lFlags,
  BSTR        bstrDeviceID,
  BSTR        bstrRootFullItemName,
  IUnknown    *pStiDevice,
  IUnknown    *pIUnknownOuter,
  IWiaDrvItem **ppIDrvItemRoot,
  IUnknown    **ppIUnknownInner,
  LONG        *plDevErrVal)
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

  HRESULT hr = S_OK;

  *plDevErrVal = 0;
  *ppIDrvItemRoot = NULL;
  *ppIUnknownInner = NULL;

  if (m_pStiDevice == NULL) {

      //
      // save STI device interface for locking
      //

      m_pStiDevice = (IStiDevice *)pStiDevice;
  }

  //
  // build WIA item tree
  //

  LONG lItemFlags = WiaItemTypeFolder|WiaItemTypeDevice|WiaItemTypeRoot;

  IWiaDrvItem  *pIWiaDrvRootItem  = NULL;

  //
  // create the ROOT item of the WIA device.  This name should NOT be 
  // localized in different languages. "Root" is used by WIA drivers.
  //

  BSTR bstrRootItemName = SysAllocString(WIA_DEVICE_ROOT_NAME);
  if(!bstrRootItemName) {
      return E_OUTOFMEMORY;
  }

  hr = wiasCreateDrvItem(lItemFlags,  // item flags
               bstrRootItemName,  // item name ("Root")
               bstrRootFullItemName,  // item full name ("0000\Root")
                (IWiaMiniDrv *)this,  // this WIA driver object
      sizeof(MINIDRIVERITEMCONTEXT),  // size of context
                               NULL,  // context
                 &pIWiaDrvRootItem);  // created ROOT item
                                      // (IWiaDrvItem interface)
  if (S_OK == hr) {

    //
    // ROOT item was created successfully, save the newly created Root
    // item in the pointer given by the WIA service (ppIDrvItemRoot).
    //

      *ppIDrvItemRoot = pIWiaDrvRootItem;

    //
    // Create a child item  directly under the Root WIA item
    //

      lItemFlags = WiaItemTypeFile|WiaItemTypeDevice|WiaItemTypeImage;

      PMINIDRIVERITEMCONTEXT pItemContext    = NULL;
      IWiaDrvItem           *pIWiaDrvNewItem = NULL;

      //
      // create a name for the WIA child item.  "Flatbed" is used by 
      // WIA drivers that support a flatbed scanner.
      //

      BSTR bstrItemName = SysAllocString(WIA_DEVICE_FLATBED_NAME);

      if (bstrItemName) {

          WCHAR  wszFullItemName[MAX_PATH + 1] = {0};
          _snwprintf(wszFullItemName,(sizeof(wszFullItemName) / sizeof(WCHAR)) - 1,L"%ls\\%ls",
                   bstrRootFullItemName,bstrItemName);

        BSTR bstrFullItemName = SysAllocString(wszFullItemName);
        if (bstrFullItemName) {
          hr = wiasCreateDrvItem(lItemFlags,  // item flags
                               bstrItemName,  // item name ("Flatbed")
                             trFullItemName,  // item full name ("0000\Root\Flatbed")
                        (IWiaMiniDrv *)this,  // this WIA driver object
               sizeof(MINIDRIVERITEMCONTEXT), // size of context
                       (BYTE**)&pItemContext, // context
                        &pIWiaDrvNewItem);    // created child item
                                              // (IWiaDrvItem interface)

            if (S_OK == hr) {

                //
                // A New WIA driver item was created successfully
                //

                hr = pIWiaDrvNewItem->AddItemToFolder(pIWiaDrvRootItem); // add the new item to the ROOT
  if (S_OK == hr) {

                    //
                    // successfully created and added a new WIA 
                    // driver item to the WIA driver item tree.
                    //

                }

                //
                // The new item is no longer needed, because it has
                // been passed to the WIA service.
                //

                pIWiaDrvNewItem->Release();
                pIWiaDrvNewItem = NULL;
            }
            SysFreeString(bstrFullItemName);
            bstrFullItemName = NULL;
        } else {
            hr = E_OUTOFMEMORY;
        }
        SysFreeString(bstrItemName);
        bstrItemName = NULL;
    } else {
        hr = E_OUTOFMEMORY;
    }
  }

  //
  // increment application connection count
  //

  if(S_OK == hr){
    InterlockedIncrement(&m_lClientsConnected);
  }

  return hr;
}
```

 

 




