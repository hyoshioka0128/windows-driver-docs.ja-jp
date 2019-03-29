---
title: コンポーネントのバインドの変更
description: コンポーネントのバインドの変更
ms.assetid: 2e59a160-d8d9-4739-a8fa-919760f8eb05
keywords:
- オブジェクトの WDK ネットワーク、バインディングの変更を通知します。
- ネットワーク オブジェクト WDK、バインディングの変更を通知します。
- バインディングは、WDK のネットワークを変更します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ccf45fba976db2a9aa2602769b08df22acdcfc18
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350229"
---
# <a name="changing-bindings-for-a-component"></a>コンポーネントのバインドの変更





ネットワーク構成のサブシステムは、通知オブジェクトのネットワーク コンポーネントに影響するバインディングの変更について通知オブジェクトを常に通知します。 サブシステムの呼び出し、通知オブジェクトの[ **INetCfgComponentNotifyBinding::NotifyBindingPath** ](https://msdn.microsoft.com/library/windows/hardware/ff547731)メソッドへのポインターと共に変更を示す値を渡すと、 **INetCfgBindingPath**バインド パスの変更に関係のインターフェイス。 場合は、サブシステム渡します NCN\_無効にすると、特定のネットワーク カードと、通知オブジェクトのネットワーク コンポーネントを共有するバインディング パスが無効にする、通知オブジェクトをアクティブ化できますバインディング別のネットワーク カードで次のコードに示すようにします。

```C++
HRESULT CSample::NotifyBindingPath(DWORD dwChangeFlag,
        INetCfgBindingPath* pncbp1)
{
    INetCfgComponent *pnccLow;
    INetCfgComponentBindings *pncbind;
    IEnumNetCfgBindingPath *penumncbp;
    INetCfgBindingPath *pncbp2;
    IEnumNetCfgBindingInterface *penumncbi;
    INetCfgBindingInterface *pncbi;
    DWORD dwFlags = EBP_BELOW;
    ULONG celt = 1; // Request one enumeration element. 
    HRESULT hr = S_OK;
    // Retrieve bindings for the notify object's component (m_pncc)
    hr = m_pncc->QueryInterface(IID_INetCfgComponentBindings, 
                                (LPVOID*)&pncbind);
    // Determine if notification is about disabling a binding path.
    if (SUCCEEDED(hr) && (NCN_DISABLE & dwChangeFlag)) {
        // Retrieve enumerator for binding paths for the component.
        hr = pncbind->EnumBindingPaths(dwFlags, &penumncbp);
        // Reset the sequence and retrieve a binding path.
        hr = penumncbp->Reset();
        hr = penumncbp->Next(celt, &pncbp2, NULL);
        // Ensure the binding path is different.
        do {
            if (pncbp1 != pncbp2) break;
   hr = penumncbp->Skip(celt); // skip one element
            hr = penumncbp->Next(celt, &pncbp2, NULL);
        } while (SUCCEEDED(hr));
        if (SUCCEEDED(hr) {
            // Retrieve enumerator for interfaces of the binding path.
            hr = pncbp2->EnumBindingInterfaces(&penumncbi);
            // Retrieve a binding interface for the binding path.
            hr = penumncbi->Next(celt, &pncbi, NULL);
            // Retrieve the lower network component.
            hr = pncbi->GetLowerComponent(&pnccLow);
            // If the component is a physical network card and binding 
            // is currently disabled, enable binding.
            DWORD dwcc;
            hr = pnccLow->GetCharacteristics(&dwcc);
            if (SUCCEEDED(hr) && (dwcc & NCF_PHYSICAL)) {
                hr = pncbp2->IsEnabled(); // S_FALSE for disabled
                if (hr == S_FALSE)  hr = pncbp2->Enable(TRUE);
            }
        }
        else return hr;
    }
    return hr;
}
```

 

 





