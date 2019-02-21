---
title: ドライバーによって WIA プロパティを書き込む
description: ドライバーによって WIA プロパティを書き込む
ms.assetid: 6d2164ac-0fbc-4ecb-b3bf-a46efbe07f51
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5c56ff01f0b867de158b01ef9825b974cdfa6e7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528889"
---
# <a name="writing-wia-properties-by-a-driver"></a>ドライバーによって WIA プロパティを書き込む





WIA ミニドライバーは、次の WIA サービス機能を使用して、WIA プロパティの現在の値と有効な値のいずれかを更新できます。

<a href="" id="wiaswritemultiple"></a>[**wiasWriteMultiple**](https://msdn.microsoft.com/library/windows/hardware/ff549475)  
WIA プロパティのすべての型を記述します。 これは、カスタム プロパティを含む、WIA 項目を既存の任意のプロパティを書き込む WIA ドライバーをできるようにする一般的な関数です。 呼び出しごとの複数のプロパティに書き込むために使用します。

<a href="" id="wiaswritepropstr"></a>[**wiasWritePropStr**](https://msdn.microsoft.com/library/windows/hardware/ff549525)  
文字列である WIA プロパティの書き込み (VT 入力\_BSTR)。

<a href="" id="wiaswriteproplong"></a>[**wiasWritePropLong**](https://msdn.microsoft.com/library/windows/hardware/ff549515)  
4 バイト整数 WIA プロパティの書き込み (VT 入力\_I4)。

<a href="" id="wiaswritepropfloat"></a>[**wiasWritePropFloat**](https://msdn.microsoft.com/library/windows/hardware/ff549507)  
4 バイトの実数である WIA プロパティの書き込み (VT 入力\_R4)。

<a href="" id="wiaswritepropguid"></a>[**wiasWritePropGuid**](https://msdn.microsoft.com/library/windows/hardware/ff549512)  
Guid である WIA プロパティの書き込み (VT 入力\_CLSID)。

<a href="" id="wiaswritepropbin"></a>[**wiasWritePropBin**](https://msdn.microsoft.com/library/windows/hardware/ff549500)  
符号なしバイトの文字列である WIA プロパティの書き込み (VT 入力\_ベクター |VT\_UI1)。

<a href="" id="wiasgetchangedvaluelong"></a>[**wiasGetChangedValueLong**](https://msdn.microsoft.com/library/windows/hardware/ff549214)  
WIA プロパティは、4 バイト整数の現在の変更された情報を取得 (VT 入力\_I4)。

<a href="" id="wiasgetchangedvaluefloat"></a>[**wiasGetChangedValueFloat**](https://msdn.microsoft.com/library/windows/hardware/ff549200)  
4 バイトの実数である WIA プロパティの現在の変更された情報を取得 (VT 入力\_R4)。

<a href="" id="wiasgetchangedvalueguid"></a>[**wiasGetChangedValueGuid**](https://msdn.microsoft.com/library/windows/hardware/ff549211)  
Guid である WIA プロパティの現在の変更された情報を取得 (VT 入力\_CLSID)。

<a href="" id="wiasgetchangedvaluestr"></a>[**wiasGetChangedValueStr**](https://msdn.microsoft.com/library/windows/hardware/ff549219)  
文字列である WIA プロパティの現在の変更された情報を取得 (VT 入力\_BSTR)。

<a href="" id="wiascreatepropcontext"></a>[**wiasCreatePropContext**](https://msdn.microsoft.com/library/windows/hardware/ff549167)  
使用されている WIA プロパティのコンテキストを作成、 [ **wiasGetChangedValueLong**](https://msdn.microsoft.com/library/windows/hardware/ff549214)、 [ **wiasGetChangedValueFloat**](https://msdn.microsoft.com/library/windows/hardware/ff549200)、 [ **wiasGetChangedValueGuid**](https://msdn.microsoft.com/library/windows/hardware/ff549211)、および[ **wiasGetChangedValueStr** ](https://msdn.microsoft.com/library/windows/hardware/ff549219)サービスの機能です。

<a href="" id="wiasfreepropcontext"></a>[**wiasFreePropContext**](https://msdn.microsoft.com/library/windows/hardware/ff549195)  
によって作成されたコンテキストが割り当てられたメモリを解放[ **wiasCreatePropContext**](https://msdn.microsoft.com/library/windows/hardware/ff549167)します。

### <a href="" id="implementing-iwiaminidrv-drvvalidateitemproperties"></a>IWiaMiniDrv::drvValidateItemProperties を実装します。

[ **IWiaMiniDrv::drvValidateItemProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff545017)アイテムの WIA プロパティに変更されたときに、メソッドが呼び出されます。 WIA ミニドライバーでは、更新プログラムの任意の有効な値その変更をする必要がありますが、値が有効では現在チェックだけする必要があります。

WIA プロパティが有効で、アプリケーションがそれを記述しない場合は、無効な値との依存の値、有効な値に変更する必要がありますまたはそれ以外の場合 (アプリケーションでは、無効な値にプロパティを設定です) ため、検証に失敗します。

次の例の実装を示しています、 **IWiaMiniDrv::drvValidateItemProperties**メソッド。

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

 

 




