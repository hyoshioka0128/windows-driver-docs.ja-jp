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
ms.openlocfilehash: 77959db759c5ca646c5d58f0a234806fc3294b5f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336001"
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

コンパートメントは、NDIS がインターフェイスを管理する方法です。 」の説明に従ってにサード パーティ製インターフェイス プロバイダーがプライマリのコンパートメントにのみ使用して、 **CompartmentId**のメンバー、 [ **NDIS\_バインド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff564832)構造体。

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


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**NDIS\_バインド\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff564832)

 

 






