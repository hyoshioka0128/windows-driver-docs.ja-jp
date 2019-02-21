---
title: コンポーネントを追加します。
description: コンポーネントを追加します。
ms.assetid: f8177904-77a2-4d1a-8c72-0b47a100bc37
keywords:
- 通知オブジェクト WDK ネットワー キング、コンポーネントの追加
- ネットワークは、コンポーネントの追加、WDK のオブジェクトに通知します。
- ネットワーク コンポーネントの追加
- ネットワーク コンポーネントの追加 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9441d3a528e0b9fb0ef1974e0087fcebea576a99
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556873"
---
# <a name="adding-a-component"></a>コンポーネントを追加します。





サブシステムは、ネットワーク コンポーネントを追加するとき、ネットワーク構成のサブシステムは、通知オブジェクトに通知できます。 通知オブジェクトを初期化した後、サブシステムが通知オブジェクトを呼び出す[ **INetCfgComponentNotifyGlobal::GetSupportedNotifications** ](https://msdn.microsoft.com/library/windows/hardware/ff547734)メソッドで必要な通知の種類を取得するにはオブジェクト。 通知オブジェクトを呼び出して、ネットワーク コンポーネントが追加されたときに通知が必要だった通知オブジェクトが指定した場合、サブシステム[ **INetCfgComponentNotifyGlobal::SysNotifyComponent** ](https://msdn.microsoft.com/library/windows/hardware/ff547736)メソッドを呼び出し NCN\_通知を通知するために追加のネットワーク コンポーネントがサブシステムにインストールされているオブジェクトします。 通知オブジェクトを所有するコンポーネントは、指定したコンポーネントにバインドする必要があります、通知オブジェクトは、バインドを容易に操作を実行する必要があります。 たとえば、次のコードでは、通知オブジェクトにバインドする方法、コンポーネント、指定したコンポーネント、指定したコンポーネントが必要な物理ネットワーク カードの場合を示しています。

```cpp
HRESULT CSample::SysNotifyComponent(DWORD dwChangeFlag,
        INetCfgComponent* pnccItem)
{
    HRESULT hr = S_OK;
    INetCfgComponentBindings *pncfgcompbind;
    // Retrieve bindings for the notify object&#39;s component (m_pncc)
    hr = m_pncc->QueryInterface(IID_INetCfgComponentBindings, 
                                (LPVOID*)&pncfgcompbind);
    // Determine if notification is about adding a component
    if (SUCCEEDED(hr) && (NCN_ADD & dwChangeFlag)) {
        // Retrieve the characteristics of the added component
        DWORD dwcc;
        hr = pnccItem->GetCharacteristics(&dwcc);
        // Determine if the added component is a physical adapter
        if (SUCCEEDED(hr) && (dwcc & NCF_PHYSICAL)) {
            // Determine the component&#39;s ID
            LPWSTR pszwInfId;
            hr = pnccItem->GetId(&pszwInfId);
            if (SUCCEEDED(hr)) {
                // Compare the component&#39;s ID to the required ID
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

 

 





