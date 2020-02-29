---
title: コンポーネントのバインドの変更
description: コンポーネントのバインドの変更
ms.assetid: 2e59a160-d8d9-4739-a8fa-919760f8eb05
keywords:
- オブジェクトに WDK ネットワークを通知し、変更をバインドする
- ネットワーク通知オブジェクト WDK、バインドの変更
- バインドの変更 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c25c990da302101854b146c60b493f6878643ef8
ms.sourcegitcommit: 69939496f6d5cb535aad2bd426ab2baa8d7b9051
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2020
ms.locfileid: "78178061"
---
# <a name="changing-bindings-for-a-component"></a>コンポーネントのバインドの変更





ネットワーク構成サブシステムは、通知オブジェクトのネットワークコンポーネントに影響を与えるバインドの変更について、通知オブジェクトに常に通知します。 サブシステムは、notify オブジェクトの[**Inetcfgcomponentnotifybinding:: NotifyBindingPath**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547731(v=vs.85))メソッドを呼び出し、変更に関係するバインドパスの**inetcfgbindingpath**インターフェイスへのポインターと共に、変更を指定する値を渡します。 サブシステムが NCN\_DISABLE を渡して、通知オブジェクトのネットワークコンポーネントが特定のネットワークカードと共有するバインドパスを無効にすると、通知オブジェクトは、次のコードに示すように、別のネットワークカードを使用してバインドをアクティブ化できます。

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
        if (SUCCEEDED(hr)) {
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

 

 





