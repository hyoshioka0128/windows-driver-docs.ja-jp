---
title: アプリケーションは、WIA デバイスを作成する方法
description: アプリケーションは、WIA デバイスを作成する方法
ms.assetid: f4268c61-11e5-4796-b7cb-80c8112be4d8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca6c0846eca30a6623dd8ea98aaf1811b9a59d73
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536015"
---
# <a name="how-the-application-creates-the-wia-device"></a>アプリケーションは、WIA デバイスを作成する方法





WIA のデバイス ドライバーを使用する場合、アプリケーションが呼び出す、 **IWiaDevMgr::CreateDevice**メソッド (Microsoft Windows SDK のドキュメントで説明)。 サービスの最初の呼び出しを WIA [ **IStiUSD::LockDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff543829) WIA のドライバーを相互に排他的アクセスをロックします。 次に、WIA サービスを呼び出す[ **IWiaMiniDrv::drvInitializeWia** ](https://msdn.microsoft.com/library/windows/hardware/ff544986)初期 WIA 項目のツリー構造を作成します。 WIA サービスが呼び出すことによって、デバイス ドライバーを解除する最後に、 [ **IStiUSD::UnLockDevice**](https://msdn.microsoft.com/library/windows/hardware/ff543843)します。

**IWiaMiniDrv::drvInitializeWia**メソッドは、次のタスクを実行する必要があります。

1.  インターフェイスのキャッシュを*pStiDevice*パラメーターが適切なデバイスのロックを指します。 (詳細については、次を参照してください[ **IWiaMiniDrv::drvLockWiaDevice**](https://msdn.microsoft.com/library/windows/hardware/ff544995)。)。

2.  初期 WIA 項目のツリー構造を作成します。

3.  現在のアプリケーション接続の数をインクリメントします。 この数は、アプリケーションがまだ接続されているかどうかをドライバーに通知するために使用します。 実行する適切なアクションを決定することもできます[ **IWiaMiniDrv::drvUnInitializeWia**](https://msdn.microsoft.com/library/windows/hardware/ff545010)します。

WIA アイテムの論理的な意味で名前が付けする必要があります。 Microsoft では、次の項目名、Windows XP 以降が必要です。

<a href="" id="root"></a>**ルート**  
これは、WIA 項目のツリーのルート項目を表す用語です。

<a href="" id="flatbed"></a>**フラット ベッド**  
これは、フラット ベッド スキャナーでのみをサポートするスキャナーまたはドキュメント フィーダーの付いたフラット ベッド スキャナーをサポートするスキャナーの用語です。

<a href="" id="feeder"></a>**フィーダー**  
これは、フィーダーのみをサポートするスキャナーの用語です。

WIA サービスの呼び出し、 **IWiaMiniDrv::drvInitializeWia**メソッドへの WIA アプリケーションの呼び出しに応答**IWiaDevMgr::CreateDevice** (Windows SDK のドキュメントで説明)。 この結果は、WIA サービスを呼び出す、 **IWiaMiniDrv::drvInitializeWia**新しい各クライアント接続のためのメソッド。

**IWiaMiniDrv::drvInitializeWia**メソッドがプライベート構造体を初期化し、ドライバーの項目のツリーを作成する必要があります。 ドライバーの項目のツリーは、この WIA デバイスでサポートされているすべての WIA 項目のレイアウトを示します。 このメソッドを使用してのみ、最初のツリー構造の作成を*いない*内容 (WIA プロパティ)。 WIA サービスを複数回呼び出すことで、WIA、WIA ドライバーのアイテムのプロパティを設定は個別に、 [ **IWiaMiniDrv::drvInitItemProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff544989)メソッド。

WIA のすべてのデバイスでは、WIA デバイスのすべての項目の親である、ルートの項目があります。 ドライバー、WIA WIA デバイス項目を作成する、WIA サービス ヘルパー関数を呼び出す必要があります[ **wiasCreateDrvItem**](https://msdn.microsoft.com/library/windows/hardware/ff549160)します。

次の例では、WIA デバイス ルート項目を作成する方法を示します。

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

前の例で作成したルート項目のすぐ下に、WIA 子項目を作成するには、次のようなコードを使用します。

**注**  * * * 注意、 [ **IWiaDrvItem::AddItemToFolder** ](https://msdn.microsoft.com/library/windows/hardware/ff543856)ルート項目に新しく作成された子項目を追加するメソッドが呼び出されます。

 

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

次の例の実装を示しています、 **IWiaMiniDrv::drvInitializeWia**メソッド。

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

 

 




