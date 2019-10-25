---
title: WIA 項目ツリー構造の変更
description: WIA 項目ツリー構造の変更
ms.assetid: fa6c9d25-4435-43ee-a262-9e267b9a0a69
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c05966d83ee2c27e9c2ada3d87b59992e5b24e29
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840875"
---
# <a name="changing-the-wia-item-tree-structure"></a>WIA 項目ツリー構造の変更





WIA ミニドライバーには、いつでも WIA 項目のツリー構造を変更する機能があります。 ミニドライバーが WIA 項目ツリーに変更を加えた場合、ミニドライバーは WIA サービスに通知する必要があります。 その後、WIA サービスは、接続されているすべての WIA アプリケーションに通知します。 通知を受信した後、WIA アプリケーションでは、変更の結果を確認するために、WIA 項目ツリーを列挙する必要があります。

ミニドライバーは、WIA サービスユーティリティ関数[**Wiasqueueevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasqueueevent)を使用して、ツリー構造の変更を wia サービスに伝達します。 WIA ミニドライバーは、 [**IWiaMiniDrv::D rvgetcapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)で報告されたイベントのみをキューに記録できます。 WIA イベントのレポートの詳細については、「[イベントレポート](event-reporting.md)」を参照してください。

### <a name="explanation-of-the-iwiaminidrvdrvdeleteitem-implementation"></a>IWiaMiniDrv::d rvDeleteItem の実装の説明

Wia アプリケーションが**Iwiaitem::D eleteitem**メソッド (Microsoft Windows SDK のドキュメントで説明) を呼び出して、wia 項目を削除すると、wia サービスは[**IWiaMiniDrv::d rvdeleteitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdeleteitem)メソッドを呼び出します。

このメソッドを呼び出す前に、WIA サービスが次のことを確認します。

-   項目がルート項目ではありません。

-   アイテムに子がありません。

-   項目のアクセス権を削除することができます。

これらの条件は、WIA サービスによって検証されるため、WIA ドライバーでも必要ありません。

次のコード例は、 **IWiaMiniDrv::D rvdeleteitem**の実装を示しています。

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

 

 




