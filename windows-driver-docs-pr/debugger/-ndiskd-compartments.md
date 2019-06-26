---
title: ndiskd.compartments
description: Ndiskd.compartments 拡張機能では、すべてのネットワーク コンパートメントが表示されます。
ms.assetid: F9BF319D-77E9-4D12-84E9-655058F57AC4
keywords:
- デバッグ ndiskd.compartments Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.compartments
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 06b9930beb61d63a5c000f72c0ef1fd68266b7dd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364296"
---
# <a name="ndiskdcompartments"></a>!ndiskd.compartments


**! Ndiskd.compartments**拡張機能には、すべてのネットワーク コンパートメントが表示されます。

```console
!ndiskd.compartments 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


この拡張機能には、パラメーターがありません。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="remarks"></a>注釈
-------

コンパートメントは、NDIS がインターフェイスを管理する方法です。 」の説明に従ってにサード パーティ製インターフェイス プロバイダーがプライマリのコンパートメントにのみ使用して、 **CompartmentId**のメンバー、 [ **NDIS\_バインド\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)構造体。

<a name="examples"></a>例
--------

実行、 **! ndiskd.compartments**拡張機能をすべてのネットワーク コンパートメントの一覧を参照してください。 この例では、1 つだけのコンパートメント (プライマリ 1 つです)。

```console
3: kd> !ndiskd.compartments
    Compartment        ffffdf80139b9940
    ID                 1
    Loopback Network   ffffdf80139b8900
    Loopback Interface ffffdf80139b6a20
    Networks:
                       ffffdf80139b8900    [Unnamed network]
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[**NDIS\_バインド\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)

 

 






