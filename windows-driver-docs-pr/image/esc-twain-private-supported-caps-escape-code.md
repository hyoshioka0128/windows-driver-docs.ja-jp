---
title: ESC_TWAIN_PRIVATE_SUPPORTED_CAPS エスケープコード
description: ESC_TWAIN_PRIVATE_SUPPORTED_CAPS エスケープコード
ms.assetid: 99b9f180-018b-47c4-ab8d-dc037e3f637a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e20e2a41f4d32013dd212a43cdfda09d96cf6212
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840848"
---
# <a name="esc_twain_private_supported_caps-escape-code"></a>ESC\_TWAIN\_プライベート\_サポートされている\_CAPS エスケープコード





Twain アプリケーションは、twain でサポートされているプライベート機能を確認するために、twain 互換性レイヤーに通知します。これによって、\_サポートされている ESC\_TWAIN\_プライベート WIA ドライバーの Iと Usd に送信さ\_れます[ **。Escape**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-escape)メソッド。 次に示す**エスケープ**メソッドの擬似コード実装では、UTF-8\_TWAIN\_プライベート\_サポートされている\_cap エスケープコードに応答して、プライベート twain サポート機能を報告する方法を示します。

この例の**エスケープ**メソッドは、 [esc\_TWAIN\_機能のエスケープコード](esc-twain-capability-escape-code.md)に示されているものと**同じ   ます**が、各サンプルのフォーカスは異なるエスケープコードです。

 

```cpp
STDMETHODIMP CWIADevice::Escape(STI_RAW_CONTROL_CODE EscapeFunction,
  LPVOID               lpInData,
  DWORD                cbInDataSize,
  LPVOID               pOutData,
  DWORD                dwOutDataSize,
  LPDWORD              pdwActualData)
{
  //
  // Only process EscapeFunction codes that are known to your driver.
  // Any application can send escape calls to your driver using the
  // IWiaItemExtras interface Escape() method call.  The driver must
  // be prepared to validate all incoming calls to Escape().
  //

  //
  // Because this driver does not support any escape functions, it will
  // reject all incoming EscapeFunction codes.
  //
  // If your driver supports an EscapeFunction, then add your function
  // code to the switch statement, and set hr = S_OK. This will allow
  // the function to continue to the incoming/outgoing buffer
  // validation.
  //

  HRESULT hr = E_NOTIMPL;
  switch(EscapeFunction) {
  case ESC_TWAIN_PRIVATE_SUPPORTED_CAPS: // processing TWAIN supported caps Escapecode
     hr = S_OK;
     break;
  default:
     break;
  }

  //
  // If an EscapeFunction code is supported, then first validate the
  // incoming and outgoing buffers.
  //

  if(S_OK == hr) {

     //
     // Validate the incoming data buffer.
     //

     if(IsBadReadPtr(lpInData,cbInDataSize)) {
         hr = E_UNEXPECTED;
     }

     //
     // If the incoming buffer is valid, proceed to validate the
     // outgoing buffer.
     //

     if(S_OK == hr) {
         if(IsBadWritePtr(pOutData,dwOutDataSize)) {
             hr = E_UNEXPECTED;
         } else {

             //
             // Validate the outgoing size pointer.
             //

             if(IsBadWritePtr(pdwActualData,sizeof(DWORD))) {
                 hr = E_UNEXPECTED;
             }
        }
     }

     //
     // Now that buffer validation is complete, proceed to process the
     // proper EscapeFunction code.
     //

     if(S_OK == hr) {

       //
       // Only process a validated EscapeFunction code, and buffers.
       //

       if(EscapeFunction == ESC_TWAIN_PRIVATE_SUPPORTED_CAPS) {

           //
           // Process a TWAIN supported capabilities message.
           //

           // Check the lpInData buffer for the number of bytes
           // of the capability array.
           //
           // 1. Create variable of type LONG*, initializing it
           //    to the value in lpInData.
           // 2. Dereference this variable to obtain the size, in
           //    bytes, of the private TWAIN capability array.

           LONG *pSupportedCapsSize = NULL;
           pSupportedCapsSize = (LONG*)lpInData;

           if(pSupportedCapsSize) {
               LONG lNumBytes = *pSupportedCapsSize;

                // lNumBytes determines the operation to perform.

               if(lNumBytes == 0) {
                // If lNumBytes is zero:
                // a. Create a variable of type LONG*, and
                //    initialize it to the value in pOutData.
                // b. Dereference this variable, and set the size,
                //    in bytes, of the private TWAIN capability array.
                //  c. Set *pchActualData to sizeof(LONG).
                //  d. Set the HRESULT to S_OK, and return.

                  LONG *pCapArraySize = (LONG*)pOutData;
                  *pCapArraySize = (NUM_PRIVATE_TWAIN_CAPS * sizeof(LONG));
                  *pdwActualData = sizeof(LONG);
                   hr = S_OK;
               } else if(lNumBytes > 0) {
                  // If lNumBytes is positive:
                  //  a. Create a variable of type LONG*, and
                  //     initialize it to the value in pOutData.
                  //  b. Dereference this variable, and set each
                  //     capability ID of the private TWAIN capability
                  //     array.
                  //  c. Set *pchActualData to the size, in bytes, of
                  //     the total capability array.
                  //  d. Set the HRESULT to S_OK, and return.

                   LONG *pCapArray = (LONG*)pOutData;
                   pCapArray[0] = ICAP_MY_PRIVATE_CAP1;
                   pCapArray[1] = ICAP_MY_PRIVATE_CAP2;
                   pCapArray[2] = ICAP_MY_PRIVATE_CAP3;
                   pCapArray[3] = ICAP_MY_PRIVATE_CAP4;
                   pCapArray[4] = ICAP_MY_PRIVATE_CAP5;
                   *pdwActualData = (NUM_PRIVATE_TWAIN_CAPS * sizeof(LONG));
                   hr = S_OK;
               } // if (lNumBytes > 0)
           } // if (pSupportedCapsSize)
       }
     }
  }

  //
  // If your driver will not support this entry point, then
  // it must return E_NOTIMPL (error, not implemented).
  //

  return hr;
}
```

 

 




