---
title: ndiskd.ndiskdversion
description: Ndiskd.ndiskdversion 拡張機能では、ndiskd 自体に関する情報が表示されます。
ms.assetid: 12EB9E0F-7D2F-447B-B678-1E23EFF522FE
keywords:
- デバッグ ndiskd.ndiskdversion Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ndiskdversion
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2bfbcdc6fe050700fcf3bf6115ab5aa0ac0c2989
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335916"
---
# <a name="ndiskdndiskdversion"></a>!ndiskd.ndiskdversion


**! Ndiskd.ndiskdversion**拡張機能に関する情報が表示されます。 ndiskd 自体。

```console
!ndiskd.ndiskdversion 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


この拡張機能には、パラメーターがありません。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>例
--------

次の例の出力を示しています **! ndiskd.ndiskdversion**します。

```console
1: kd> !ndiskd.ndiskdversion
    NDISKD Version     17.01.00 (NDISKD codename "All your WDF are belong to us")
    Build              Release
    Debugger CPU       AMD64
    NDIS symbols       Private             More info
    Hyperlinks (DML)   Enabled
    Unicode            Enabled
    Debug NDISKD       Enabled
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

 

 






