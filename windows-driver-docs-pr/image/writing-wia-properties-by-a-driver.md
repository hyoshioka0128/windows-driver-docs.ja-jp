---
title: ドライバーによる WIA プロパティの書き込み
description: ドライバーによる WIA プロパティの書き込み
ms.assetid: 6d2164ac-0fbc-4ecb-b3bf-a46efbe07f51
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c2bbaf4b6b389134499cf2cbf12772b1ad1e56e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840659"
---
# <a name="writing-wia-properties-by-a-driver"></a>ドライバーによる WIA プロパティの書き込み





Wia ミニドライバーは、次の WIA サービス関数を使用して、WIA プロパティと有効値の現在の値を更新できます。

<a href="" id="wiaswritemultiple"></a>[**wiasWriteMultiple**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritemultiple)  
すべての WIA プロパティの型を書き込みます。 これは、wia ドライバーがカスタムプロパティを含む、WIA 項目に存在する任意のプロパティを書き込むことができるようにする一般的な関数です。 これを使用して、呼び出しごとに複数のプロパティに書き込むことができます。

<a href="" id="wiaswritepropstr"></a>[**wiasWritePropStr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropstr)  
文字列である WIA プロパティを作成します (「VT\_BSTR」と入力します)。

<a href="" id="wiaswriteproplong"></a>[**wiasWritePropLong p)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswriteproplong)  
4バイトの整数である WIA プロパティを作成します (「VT\_I4)」と入力します。

<a href="" id="wiaswritepropfloat"></a>[**wiasWritePropFloat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropfloat)  
4バイトの実数 (型 VT\_R4) である WIA プロパティを作成します。

<a href="" id="wiaswritepropguid"></a>[**wiasWritePropGuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropguid)  
Guid である WIA プロパティを作成します (「VT\_CLSID」と入力します)。

<a href="" id="wiaswritepropbin"></a>[**wiasWritePropBin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropbin)  
符号なしバイトの文字列である WIA プロパティを作成します (型 VT\_VECTOR |VT\_UI1)。

<a href="" id="wiasgetchangedvaluelong"></a>[**wiasGetChangedValueLong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluelong)  
4バイトの整数 (型 VT\_I4) である WIA プロパティについて、現在変更されている情報を取得します。

<a href="" id="wiasgetchangedvaluefloat"></a>[**wiasGetChangedValueFloat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat)  
4バイトの実数 (型 VT\_R4) である WIA プロパティについて、現在変更されている情報を取得します。

<a href="" id="wiasgetchangedvalueguid"></a>[**Wiasgetのすべての属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvalueguid)  
Guid である WIA プロパティについて、現在変更されている情報を取得します (「VT\_CLSID」と入力します)。

<a href="" id="wiasgetchangedvaluestr"></a>[**wiasGetChangedValueStr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluestr)  
文字列である WIA プロパティについて、現在変更されている情報を取得します (「VT\_BSTR)」と入力します。

<a href="" id="wiascreatepropcontext"></a>[**wiasCreatePropContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatepropcontext)  
[**WiasGetChangedValueLong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluelong)、 [**wiasgetchangedvaluefloat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat)、 [**wiasget valueguid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvalueguid)、および[**wiasGetChangedValueStr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluestr) service 関数で使用される、WIA プロパティコンテキストを作成します。

<a href="" id="wiasfreepropcontext"></a>[**wiasFreePropContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasfreepropcontext)  
[**Wiascreatepropcontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatepropcontext)によって作成された割り当て済みコンテキストメモリを解放します。

### <a href="" id="implementing-iwiaminidrv-drvvalidateitemproperties"></a>IWiaMiniDrv の実装::d rvValidateItemProperties

[**IWiaMiniDrv::D rvvalidateitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)メソッドは、項目の WIA プロパティに変更が加えられたときに呼び出されます。 WIA ミニドライバーは、値が有効であることを確認するだけでなく、変更される有効な値を更新する必要があります。

WIA プロパティが無効で、アプリケーションがそれに書き込めない場合は、無効な値と依存する値を有効な値に変更するか、検証に失敗する必要があります (アプリケーションではプロパティが無効な値に設定されているため)。

次の例は、 **IWiaMiniDrv::D rvvalidateitemproperties**メソッドの実装を示しています。

```cpp
HRESULT _stdcall CWIADevice::drvValidateItemProperties(
  BYTE           *pWiasContext,
  LONG           lFlags,
  ULONG          nPropSpec,
  const PROPSPEC *pPropSpec,
  LONG           *plDevErrVal)
{
  //
  // If the caller did not pass in the correct parameters,
  //  then fail the call with E_INVALIDARG.
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

  HRESULT hr      = S_OK;
  LONG lItemType  = 0;
  WIA_PROPERTY_CONTEXT Context;

  *plDevErrVal = 0;

  //
  // create a WIA property context, to gain access to
  // the WIA application's intended settings.
  //

  hr = wiasCreatePropContext(nPropSpec,
                             (PROPSPEC*)pPropSpec,
                             0,
                             NULL,
                             &Context);
  if(S_OK == hr) {

    //
    // get the current item type to help determine what property set to validate
    //

      hr = wiasGetItemType(pWiasContext, &lItemType);
      if (S_OK == hr) {
          if (lItemType & WiaItemTypeRoot) {

            //
            //  validate root item properties here
            //

        } else {

            //
            // validate item properties here
            //

              WIAS_CHANGED_VALUE_INFO cviDataType;
              memset(&cviDataType,0,sizeof(cviDataType));

            //
            // check to see if the application was updating
            // the WIA_IPA_DATATYPE property
   //

              hr = wiasGetChangedValueLong(pWiasContext,pContext,FALSE,WIA_IPA_DATATYPE,&cviDataType);
              if(S_OK == hr) {
                  if (cviDataType.bChanged) {

                    //
                    // This value was changed, and needs to be checked
                    //
                    // cviDataType.Current.lVal is the current application setting.
                    //

                  } else {

                    //
                    // Nothing has been changed, so leave this property alone.
                    // Let the WIA service function wiasValidateItemProperties
                    // do the rest of the work for you.
                    //

 }
              }
          }

        //
        // free the property context
        //

          wiasFreePropContext(&Context);
      }

    //
    // call WIA service helper when you have finished updating dependent values
    //

    if(S_OK == hr) {

        //
        // call WIA service helper to validate other properties
        //

          hr = wiasValidateItemProperties(pWiasContext, nPropSpec, pPropSpec);
      }
  }
  return hr;
}
```

 

 




