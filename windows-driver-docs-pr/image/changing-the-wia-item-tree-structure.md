---
title: WIA 項目ツリー構造の変更
description: WIA 項目ツリー構造の変更
ms.assetid: fa6c9d25-4435-43ee-a262-9e267b9a0a69
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79376077e55bb593e47d18d23529096074016c16
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373534"
---
# <a name="changing-the-wia-item-tree-structure"></a>WIA 項目ツリー構造の変更





WIA ミニドライバーは、いつでも、WIA 項目のツリー構造を変更する権限を持ちます。 ミニドライバーが WIA 項目のツリーに変更するとき、ミニドライバーは、サービスに WIA を通知する必要があります。 WIA サービスは、接続されたすべての WIA アプリケーションを通知します。 通知が受信した後、WIA アプリケーションは、変更の結果を判定 WIA 項目ツリーを列挙する必要があります。

ミニドライバーは、WIA サービス ユーティリティ関数を使用して[ **wiasQueueEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasqueueevent)、WIA サービスにツリー構造での変更が通知されます。 WIA ミニドライバーがで報告されているイベントのみをキュー [ **IWiaMiniDrv::drvGetCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)します。 WIA イベントをレポートの詳細については、次を参照してください。[イベントの報告](event-reporting.md)します。

### <a name="explanation-of-the-iwiaminidrvdrvdeleteitem-implementation"></a>IWiaMiniDrv::drvDeleteItem 実装の説明

WIA サービスの呼び出し、 [ **IWiaMiniDrv::drvDeleteItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdeleteitem)メソッド WIA アプリケーションを呼び出すと、 **IWiaItem::DeleteItem**メソッド (Microsoft Windows で説明します。SDK のドキュメント) WIA 項目を削除します。

WIA サービスは、このメソッドを呼び出す前に、次を確認します。

-   項目は、ルート項目ではありません。

-   項目が子を持っていません。

-   項目のアクセス権は、削除を許可します。

WIA サービスは、これらの条件を検証、ために、WIA ドライバーもそう必要はありません。

次のコード例の実装を示しています**IWiaMiniDrv::drvDeleteItem**:。

```cpp
HRESULT _stdcall CWIADevice::drvDeleteItem(BYTE *pWiasContext,
                                           LONG lFlags,
                                           LONG *plDevErrVal)
{
    //
    // If the caller did not pass in the correct parameters,
    // then fail the call with E_INVALIDARG.
    //

    if ((!pWiasContext) || (!plDevErrVal))
    {
        return E_INVALIDARG;
    }

    *plDevErrVal = 0;

    HRESULT hr = S_OK;

    //
    // Two pieces of information are needed to queue an event:
    // 1. Full item name
    // 2. Device ID (passed in from drvInitializeWia,
    //    or read from the ROOT item's property set)
    //

    BSTR bstrFullItemName = NULL;
    hr = wiasReadPropStr(pWiasContext,
                         WIA_IPA_FULL_ITEM_NAME,
                         &bstrFullItemName,NULL,TRUE);
    if (hr == S_OK)
    {
        hr = HARDWARE_DELETE_DATA_FOR_ITEM();
        if (hr == S_OK)
        {
            //
            // Use m_bstrDeviceID cached from the
            // drvInitializeWia method call.
            //

            hr = wiasQueueEvent(m_bstrDeviceID,
                                &WIA_EVENT_ITEM_DELETED,
                                bstrFullItemName);
        }

        //
        // Free item's full item name, read above.
        //

        if (bstrFullItemName)
        {
            SysFreeString(bstrFullItemName);
            bstrFullItemName = NULL;
        }
    }

    //
    // Returning S_OK will instruct the WIA service to remove the WIA
    // item from the item tree. The WIA minidriver should only remove
    // any associated data corresponding to the target item.
    //

    return hr;
}
```

 

 




