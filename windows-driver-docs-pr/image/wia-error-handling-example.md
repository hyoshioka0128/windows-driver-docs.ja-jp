---
title: WIA エラー処理の例
description: WIA エラー処理の例
ms.assetid: 7dc4b15e-40db-4e64-be41-d6bcc44603c6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4e145ab226945a8f79182cc95f26350e709ca75
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379582"
---
# <a name="wia-error-handling-example"></a>WIA エラー処理の例


デバイスのステータス メッセージを送信するドライバーの例は、WIA モンスターのドライバーの拡張のサンプルを参照してください、 [WIA ドライバー サンプル](https://go.microsoft.com/fwlink/p/?linkid=256210)します。 サンプルは、単純なエラー ハンドラーを実装する方法を示しています。

### <a name="example-error-handling-extension"></a>以下に例を示します。エラー処理の拡張機能

次のコード スニペットでは、単純なエラー処理を拡張機能を実装する方法を示します。 拡張機能のみを処理します。 このエラーの処理、WIA\_エラー\_カバー\_開いているデバイスの状態エラーし、モーダル ダイアログ ボックスが表示されます。 コードの一部がこの例を簡略化に省略されていることに注意してください。

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

 

 




