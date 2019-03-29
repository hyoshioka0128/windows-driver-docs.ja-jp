---
title: コンポーネントの追加
description: コンポーネントの追加
ms.assetid: f8177904-77a2-4d1a-8c72-0b47a100bc37
keywords:
- 通知オブジェクト WDK ネットワー キング、コンポーネントの追加
- ネットワークは、コンポーネントの追加、WDK のオブジェクトに通知します。
- ネットワーク コンポーネントの追加
- ネットワーク コンポーネントの追加 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9fc5f79e9a754f0b1e0e68f6345c1addb5a4037
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350289"
---
# <a name="adding-a-component"></a>コンポーネントの追加





サブシステムは、ネットワーク コンポーネントを追加するとき、ネットワーク構成のサブシステムは、通知オブジェクトに通知できます。 通知オブジェクトを初期化した後、サブシステムが通知オブジェクトを呼び出す[ **INetCfgComponentNotifyGlobal::GetSupportedNotifications** ](https://msdn.microsoft.com/library/windows/hardware/ff547734)メソッドで必要な通知の種類を取得するにはオブジェクト。 通知オブジェクトを呼び出して、ネットワーク コンポーネントが追加されたときに通知が必要だった通知オブジェクトが指定した場合、サブシステム[ **INetCfgComponentNotifyGlobal::SysNotifyComponent** ](https://msdn.microsoft.com/library/windows/hardware/ff547736)メソッドを呼び出し NCN\_通知を通知するために追加のネットワーク コンポーネントがサブシステムにインストールされているオブジェクトします。 通知オブジェクトを所有するコンポーネントは、指定したコンポーネントにバインドする必要があります、通知オブジェクトは、バインドを容易に操作を実行する必要があります。 たとえば、次のコードでは、通知オブジェクトにバインドする方法、コンポーネント、指定したコンポーネント、指定したコンポーネントが必要な物理ネットワーク カードの場合を示しています。

```cpp
HRESULT CSample::SysNotifyComponent(DWORD dwChangeFlag,
        INetCfgComponent* pnccItem)
{
    HRESULT hr = S_OK;
    INetCfgComponentBindings *pncfgcompbind;
    // Retrieve bindings for the notify object's component (m_pncc)
    hr = m_pncc->QueryInterface(IID_INetCfgComponentBindings, 
                                (LPVOID*)&pncfgcompbind);
    // Determine if notification is about adding a component
    if (SUCCEEDED(hr) && (NCN_ADD & dwChangeFlag)) {
        // Retrieve the characteristics of the added component
        DWORD dwcc;
        hr = pnccItem->GetCharacteristics(&dwcc);
        // Determine if the added component is a physical adapter
        if (SUCCEEDED(hr) && (dwcc & NCF_PHYSICAL)) {
            // Determine the component's ID
            LPWSTR pszwInfId;
            hr = pnccItem->GetId(&pszwInfId);
            if (SUCCEEDED(hr)) {
                // Compare the component's ID to the required ID
                // and if they are the same perform the binding.
                static const TCHAR c_szCompId[] = TEXT("BINDTO_NIC");
                if (!_tcsicmp(pszwInfId, c_szCompId)) {
                    hr = pncfgcompbind->BindTo(pnccItem);
                }
            }
        }
    }
    return hr;
}
```

 

 





