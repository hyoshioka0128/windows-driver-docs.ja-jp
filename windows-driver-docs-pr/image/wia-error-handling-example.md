---
title: WIA エラー処理の例
description: WIA エラー処理の例
ms.assetid: 7dc4b15e-40db-4e64-be41-d6bcc44603c6
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: faadb49f20285d799a11f7f2d0c74557dcf0834a
ms.sourcegitcommit: 609c5731b2db4c17b9959082c4621c001e012db1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223533"
---
# <a name="wia-error-handling-example"></a>WIA エラー処理の例

デバイスステータスメッセージを送信するドライバーの例については、「 [Windows イメージ取得 (wia) ドライバーのサンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/windows-image-acquisition-wia-driver-samples)」の拡張された*Wia 2.0 モンスター driver*サンプルを参照してください。 このサンプルは、単純なエラーハンドラーを実装する方法を示しています。

## <a name="example-error-handling-extension"></a>例: エラー処理拡張機能

次のコードスニペットは、単純なエラー処理拡張機能を実装する方法を示しています。 このエラー処理拡張機能では、WIA エラーの "デバイスの状態を開く" エラーのみが処理され、 \_ \_ \_ モーダルダイアログボックスが表示されます。 この例を簡略化するために、コードの一部が省略されていることに注意してください。

```cpp
STDMETHODIMP

CErrHandler::ReportStatus(

IN LONG lFlags,

IN HWND hwndParent,

IN IWiaItem2 *pWiaItem2,

IN HRESULT hrStatus,

IN LONG lPercentComplete)

{

    HRESULT hr = WIA_STATUS_NOT_HANDLED;

    if (WIA_ERROR_COVER_OPEN == hrStatus)

    {

        int i;

        i = MessageBox(hwndParent,

        ERROR_COVER_OPEN_STR,

        TEXT("Driver UI Extension"),

        MB_RETRYCANCEL|MB_TASKMODAL|MB_ICONERROR);

        if (IDOK == i)

        {

            hr = S_OK;

        }

        else

        {

            hr = WIA_ERROR_COVER_OPEN;

        }

    }

    return hr;

}

STDMETHODIMP

CErrHandler::GetStatusDescription(

IN LONG lFlags,

IN IWiaItem2 *pWiaItem2,

IN HRESULT hrStatus,

OUT BSTR *pbstrDescription)

{

    HRESULT hr = pbstrDescription ? WIA_STATUS_NOT_HANDLED :

    E_INVALIDARG;

    if (WIA_ERROR_COVER_OPEN == hrStatus)

    {

        BSTR bstrDescription = NULL;

        bstrDescription = SysAllocString(ERROR_COVER_OPEN_STR);

        if (bstrDescription)

        {

            *pbstrDescription = bstrDescription;

            hr = S_OK;

        }

        else

        {

            hr = E_OUTOFMEMORY;

        }

    }

    return hr;

}
```
