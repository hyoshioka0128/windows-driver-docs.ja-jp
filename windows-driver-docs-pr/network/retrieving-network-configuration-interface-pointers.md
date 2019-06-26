---
title: ネットワーク構成インターフェイス ポインターの取得
description: ネットワーク構成インターフェイス ポインターの取得
ms.assetid: ac3638a1-d039-478e-baec-c73d4d1b6751
keywords:
- オブジェクトの WDK ネットワー キング、インターフェイス ポインターへの通知します。
- ネットワークは、インターフェイス ポインターであるオブジェクト、WDK を通知します。
- ネットワーク構成インターフェイス ポインター WDK
- インターフェイス ポインターの WDK ネットワーク
- ポインターの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4ca82f92c031c53f170d1e4b1f25df1a8a8c087
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386526"
---
# <a name="retrieving-network-configuration-interface-pointers"></a>ネットワーク構成インターフェイス ポインターの取得





ネットワーク構成のサブシステムが通知オブジェクトのインスタンスを初期化する」の説明に従ってと[を作成して、通知オブジェクトのインスタンスを初期化して](creating-and-initializing-an-instance-of-a-notify-object.md)、オブジェクトを受け取ります[ **INetCfgComponent** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547715(v=vs.85))と[ **INetCfg** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547694(v=vs.85))インターフェイス ポインター。 **INetCfgComponent**にアクセスして、コンポーネントを制御するオブジェクトで使用できる通知オブジェクトのコンポーネントのインターフェイスを指します。 **INetCfg**通知オブジェクトを使用してネットワークの構成のすべての側面にアクセスするルートのネットワーク構成インターフェイスを指します。 次のコードを使用してこれら**INetCfgComponent**と**INetCfg**インターフェイス ポインターを通知オブジェクトを必要とする他のネットワーク構成インターフェイスを取得します。

```C++
// Using the notify object's component interface that the notify 
// object received:
INetCfgComponent *pncfgcompThis, *pncfgcompUp, *pncfgcompLow;
INetCfgComponentBindings *pncfgcompbind;
IEnumNetCfgBindingPath *penumncfgbindpath;
INetCfgBindingPath *pncfgbindpath;
IEnumNetCfgBindingInterface *penumncfgbindintrfc;
INetCfgBindingInterface *pncfgbindintrfc;
HRESULT hr;
DWORD dwFlags;  // EBP_ABOVE or EBP_BELOW
ULONG celt, celtFetched; // Number of requested and returned elements

// Retrieve a pointer to INetCfgComponentBindings to control and 
// retrieve information about bindings for the component.
hr = pncfgcompThis->QueryInterface(IID_INetCfgComponentBindings, 
                                  (LPVOID*)&pncfgcompbind);
// Retrieve a pointer to IEnumNetCfgBindingPath to enumerate binding 
// paths for the component.
hr = pncfgcompbind->EnumBindingPaths(dwFlags, &penumncfgbindpath);
// Retrieve a pointer to INetCfgBindingPath that points to one or more 
// binding paths for the component.
hr = penumncfgbindpath->Next(celt, &pncfgbindpath, &celtFetched);
// Retrieve a pointer to IEnumNetCfgBindingInterface to enumerate 
// the collection of binding interfaces for the binding path.
hr = pncfgbindpath->EnumBindingInterfaces(&penumncfgbindintrfc);
// Retrieve a pointer to INetCfgBindingInterface that points to one or 
// more binding interfaces for the binding path.
hr = penumncfgbindintrfc->Next(celt, &pncfgbindintrfc, &celtFetched);
// Retrieve pointers to INetCfgComponent for network components 
// above and below the binding interface.
hr = pcfgbindintrfc->GetUpperComponent(&pncfgcompUp);
hr = pcfgbindintrfc->GetLowerComponent(&pncfgcompLow);

// Using the root network configuration interface that the notify 
// object received:
INetCfg *pnetcfg;
INetCfgLock *pncfglock;
INetCfgClass *pncfgclass;
INetCfgComponent *pncfgcompOther, *pncfgcompInstall;
INetCfgClassSetup *pncfgclsSetup
GUID *pguidClass; // For example, set to GUID_DEVCLASS_NETTRANS
IEnumNetCfgComponent *penumncfgcomp;
HWND hwndParent; // Handle to Window for selecting.
OBO_TOKEN *pOboToken; // Another component or the user installs.
DWORD dwSetupFlags, dwUpgradeFromBuildNo;
 
// Retrieve a pointer to INetCfgLock to obtain a lock on network 
// configuration.
hr = pnetcfg->QueryInterface(IID_INetCfgLock, (LPVOID*)&pncfglock);
// Retrieve a pointer to INetCfgComponent for a specific component.
hr = pnetcfg->FindComponent(TEXT("MS_TCPIP"), &pncfgcompOther);
// Retrieve a pointer to IEnumNetCfgComponent to enumerate 
// the collection of a particular type of component.
hr = pnetcfg->EnumComponents(pguidClass, &penumncfgcomp);
// Retrieve a pointer to INetCfgClass for a specific class of 
// component.
hr = pnetcfg->QueryNetCfgClass(pguidClass, IID_INetCfgClass, 
                              (LPVOID*)&pncfgclass);
// Retrieve a pointer to INetCfgComponent for a specific component.
hr = pncfgclass->FindComponent(TEXT("MS_TCPIP"), &pncfgcompOther);
// Retrieve a pointer to IEnumNetCfgComponent to enumerate 
// the collection of a particular type of component.
hr = pncfgclass->EnumComponents(&penumncfgcomp);
// Retrieve a pointer to INetCfgComponent that points to one or 
// more components for the particular type of component.
hr = penumncfgcomp->Next(celt, &pncfgcompOther, &celtFetched);
// Retrieve a pointer to INetCfgClassSetup that enables installation 
// or removal of a particular type of component.
hr = pncfgclass->QueryInterface(IID_INetCfgClassSetup, 
                               (LPVOID*)&pncfgclsSetup);
// Retrieve a pointer to INetCfgComponent for an installed component.
hr = pncfgclsSetup->SelectAndInstall(hwndParent, pOboToken,
                                     &pncfgcompInstall);
// Retrieve a pointer to INetCfgComponent for an installed component.
hr = pncfgclsSetup->Install(TEXT("MS_TCPIP"), pOboToken, dwSetupFlags, 
                           dwUpgradeFromBuildNo, TEXT("AnswerFile"), 
                    TEXT("AnswerFileSections"), &pncfgcompInstall);
```

 

 





