---
title: ndiskd ifprovider
description: Ndiskd ifprovider 拡張機能には、NDIS インターフェイスプロバイダー (IfProvider) に関する情報が表示されます。
ms.assetid: 89C406E5-81D3-42AA-BA15-3D7C093BCD3C
keywords:
- ndiskd ifprovider Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ifprovider
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 052e809ac9dcec973315345007eb2505a318fb20
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534931"
---
# <a name="ndiskdifprovider"></a>!ndiskd.ifprovider


**! Ndiskd ifprovider**拡張機能には、 [NDIS インターフェイスプロバイダー](https://docs.microsoft.com/windows-hardware/drivers/network/registering-as-an-interface-provider) (ifprovider) に関する情報が表示されます。 パラメーターを使用せずにこの拡張機能を実行すると、登録されているすべての NDIS インターフェイスプロバイダーの一覧がに表示されます。

```console
!ndiskd.ifprovider [-handle <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-ハンドル*   
IfProvider のハンドル。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>例
--------

パラメーターを付けずに **! ndiskd ifprovider**拡張機能を実行して、登録されているすべての ifprovider の一覧を取得します。

```console
1: kd> !ndiskd.ifprovider
    IfProvider                                                                  
    ffffd20d14334180 - wanarp
    ffffd20d1264a950 - wfplwfs
    ffffd20d11deae00 - The NDIS loopback provider
    ffffd20d11deae70 - The NDIS interface provider
```

前の例では、デバッグ対象マシンに4つのインターフェイスプロバイダーが登録されていることがわかります。 そのうちの2つは NDIS インターフェイスプロバイダーです。

**メモ**   インターフェイスプロバイダーは一般的な概念であり、ミニポートドライバーである必要はありません。 ミニポートドライバーは、必要に応じてインターフェイスプロバイダーとして登録することができますが、ほとんどのミニポートドライバーは、組み込みのインターフェイスプロバイダーを備えているため、これを行いません。 NDIS 組み込みインターフェイスプロバイダーは、すべてのミニポートドライバー、すべてのライトウェイトフィルター (LWF) モジュール、およびループバックインターフェイスのインターフェイスを自動的に提供します。 詳細については、「 [NDIS interface provider](https://docs.microsoft.com/windows-hardware/drivers/network/registering-as-an-interface-provider)」を参照してください。

 

次の例では、ハンドルが ffffd20d14334180 である前の例の "wanarp" インターフェイスプロバイダーの詳細を示します。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワーク ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 拡張機能 (Ndiskd .dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[インターフェイス プロバイダーとしての登録](https://docs.microsoft.com/windows-hardware/drivers/network/registering-as-an-interface-provider)

 

 






