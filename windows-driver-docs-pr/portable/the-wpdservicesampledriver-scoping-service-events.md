---
Description: Scoping Service Events
title: サービス イベントの範囲設定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 048b2a54edc0fd92f504c1d31b0c8290d0a0acbd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581138"
---
# <a name="scoping-service-events"></a>サービス イベントの範囲設定


既定では、WPD は、すべてのクライアント アプリケーション (その他のサービスに接続されているクライアント) にサービスのイベントをブロードキャストします。 ドライバー、ブロードキャストのスコープを制限するため、WPD を設定する必要があります\_オブジェクト\_コンテナー\_機能\_オブジェクト\_ブロードキャストする必要がある、サービスの ObjectID を ID イベント パラメーター制限されています。

次のコード例に示す方法**WPD\_オブジェクト\_コンテナー\_機能\_設定\_ID**イベントのパラメーターに追加されます**FakeDevice::SetPropertyValues**をオブジェクトが更新されたことを示しています。

```ManagedCPlusPlus
        if (SUCCEEDED(hr) && (*pbObjectChanged)) 
        {
            HRESULT hrEvent = pEventParams->SetGuidValue(WPD_EVENT_PARAMETER_EVENT_ID, WPD_EVENT_OBJECT_UPDATED);
            CHECK_HR(hrEvent, "Failed to add WPD_EVENT_PARAMETER_EVENT_ID");

        . . .

            if (hrEvent == S_OK)
            {
                // Adding this event parameter will allow WPD to scope this event to the container functional object
                hrEvent = pEventParams->SetStringValue(WPD_OBJECT_CONTAINER_FUNCTIONAL_OBJECT_ID, pContent->ContainerFunctionalObjectID);
                CHECK_HR(hrEvent, "Failed to add WPD_OBJECT_CONTAINER_FUNCTIONAL_OBJECT_ID");
            }
        }
```

連絡先、サービス内のオブジェクトの*pContent -&gt;ContainerFunctionalObjectID*連絡先サービスのオブジェクト識別子が含まれています。 このパラメーターを指定すると、WPD はこのイベント パラメーターと一致して、同じアドレス帳サービスに接続するその他のクライアントのみがこのイベントを受信するイベントをフィルター処理します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





