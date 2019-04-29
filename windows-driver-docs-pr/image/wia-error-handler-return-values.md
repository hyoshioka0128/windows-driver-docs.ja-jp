---
title: WIA エラー ハンドラーの戻り値
description: WIA エラー ハンドラーの戻り値
ms.assetid: 9b8efcd7-e767-4344-b3a1-96b1898e102f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60c95e657c3bfe103c6b0983d34423d333d309eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327846"
---
# <a name="wia-error-handler-return-values"></a>WIA エラー ハンドラーの戻り値


すべてのエラー ハンドラーは、さまざまな戻り値に関するルールに従う必要があります。

以下は、有効なすべての戻り値です。

<a href="" id="s-ok"></a>S\_OK  
デバイスの状態コードが正常に処理されました。 エラー ハンドラーが呼び出されます。

エラー状態コード (モーダル ダイアログ ボックス) が発生した場合これは、適切なアクションは、ADF の紙詰まりなどのエラーが修正されたことを意味します。

情報ステータス コードで、この唯一の手段モードレス ダイアログ ボックスをユーザーに提供する適切なアクションが実行されたことと、デバイスのメッセージを後からその他のエラー ハンドラーに転送されませんする必要がありますが発生した場合。

<a href="" id="wia-status-not-handled"></a>WIA\_状態\_いない\_処理済み  
ユーザーに、エラーまたはレポートの状態を処理するために処理が行われません。 リスト内の次のハンドラー (あれば) が呼び出されます。

エラー ハンドラーから既定の戻り値があります。

<a href="" id="s-false"></a>S\_FALSE  
ユーザーには、ハンドラーのモードレス ダイアログからの転送が取り消されました。 これは、任意の時点でデバイスの状態のコードに関係なく、エラー ハンドラーによって返される値を返します (処理、ハンドルされていない、エラー、または情報)。

<a href="" id="other-error-codes"></a>その他のエラー コード  
デバイスのエラーを回復できない場合、またはユーザーが表示されるモーダル ダイアログ ボックスへの応答の転送を中止する場合は、エラー ハンドラーは (「例」例を参照してください)、デバイスの状態コード自体で返す必要があります。 もちろんこのため、エラー ハンドラーでは、デバイスの状態コードを処理します。

さらに、エラー ハンドラーは、一貫性のあるデバイスの状態コードを処理する必要があります。 エラー ハンドラーのインスタンスは状態コード WIA を処理するために選択できません\_状態\_XYZ (または WIA\_エラー\_XYZ) 時間 t0 にし、それを t1 の時点で処理するされません。

次のコードでは、無効なエラー ハンドラーの例を示します。

```cpp
STDMETHODIMP
CErrHandler::ReportStatus(
    IN  LONG        lFlags,
    IN  HWND        hwndParent,
    IN  IWiaItem2   *pWiaItem2,
    IN  HRESULT     hrStatus,
    IN  LONG        lPercentComplete)
{
    HRESULT hr = WIA_STATUS_NOT_HANDLED;
    if ((hrStatus == WIA_ERROR_PAPER_JAM) && HandleMessageNow())
    {
        ...
    }
    return hr;
}
```

削除、 *HandleMessageNow*ルーチンと、この有効なエラー ハンドラー。

 

 




