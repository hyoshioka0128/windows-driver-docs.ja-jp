---
title: ndiskd.ifprovider
description: Ndiskd.ifprovider 拡張機能では、NDIS インターフェイス プロバイダー (IfProvider) に関する情報が表示されます。
ms.assetid: 89C406E5-81D3-42AA-BA15-3D7C093BCD3C
keywords:
- デバッグ ndiskd.ifprovider Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ifprovider
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9ccf94056b2905e3daab3a435ecccf1552c7c80d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335998"
---
# <a name="ndiskdifprovider"></a>!ndiskd.ifprovider


**! Ndiskd.ifprovider**拡張機能に関する情報を表示する、 [NDIS インターフェイス プロバイダー](https://msdn.microsoft.com/windows/hardware/drivers/network/registering-as-an-interface-provider) (IfProvider)。 パラメーターなしで、この拡張機能を実行する場合。 ndiskd 登録されているすべての NDIS インターフェイス プロバイダーの一覧が表示されます。

```console
!ndiskd.ifprovider [-handle <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
IfProvider のハンドル。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>例
--------

実行、 **! ndiskd.ifprovider** IfProviders がすべての一覧を取得するパラメーターなしで拡張機能に登録されています。

```console
1: kd> !ndiskd.ifprovider
    IfProvider                                                                  
    ffffd20d14334180 - wanarp
    ffffd20d1264a950 - wfplwfs
    ffffd20d11deae00 - The NDIS loopback provider
    ffffd20d11deae70 - The NDIS interface provider
```

前の例をデバッグ対象のコンピューターに登録されている 4 つのインターフェイス プロバイダーから確認できます。 これらの 2 つは、NDIS インターフェイス プロバイダーです。

**注**  インターフェイス プロバイダーは汎用的な概念、ミニポート ドライバーにする必要はありません。 必要な場合に、インターフェイス プロバイダーとして登録するミニポート ドライバーを選択することがあります、ほとんどのミニポート ドライバーしないで NDIS インターフェイスの組み込みのプロバイダーが存在するためです。 NDIS インターフェイスの組み込みプロバイダーは、自動的にすべてミニポート ドライバーや軽量な Filter (LWF) のすべてのモジュールでは、ループバック インターフェイスのインターフェイスを提供します。 詳細については、次を参照してください。 [NDIS インターフェイス プロバイダー](https://msdn.microsoft.com/windows/hardware/drivers/network/registering-as-an-interface-provider)します。

 

次の例では、前の例では、そのハンドルは ffffd20d14334180"wanarp"インターフェイス プロバイダーの詳細を示します。

```console
1: kd> !ndiskd.ifprovider ffffd20d14334180


IF PROVIDER

    wanarp
    Ndis handle        ffffd20d14334180


INTERFACES

    Interface                                                                   
    [No interfaces found]


HANDLERS

    Protocol handler                       Function pointer   Symbol (if available)
    QueryObjectHandler                     fffff80d2f0414b0  bp wanarp!WanNdisIfQueryHandler
    SetObjectHandler                       fffff80d2f04bd10  bp wanarp!WanNdisIfSetHandler
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[インターフェイスをプロバイダーとして登録します。](https://msdn.microsoft.com/windows/hardware/drivers/network/registering-as-an-interface-provider)

 

 






