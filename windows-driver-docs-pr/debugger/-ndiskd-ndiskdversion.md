---
title: ndiskd ndiskdversion
description: Ndiskd. ndiskdversion 拡張機能には、ndiskd 自体に関する情報が表示されます。
ms.assetid: 12EB9E0F-7D2F-447B-B678-1E23EFF522FE
keywords:
- ndiskd. ndiskdversion Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ndiskdversion
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3f395a1d866e17ffcabfb77956f306b994776f7c
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534727"
---
# <a name="ndiskdndiskdversion"></a>!ndiskd.ndiskdversion


! **Ndiskd. ndiskdversion**拡張機能に関する情報が表示されます。

```console
!ndiskd.ndiskdversion 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


この拡張機能にはパラメーターがありません。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>例
--------

次の例では、 **! ndiskd. ndiskdversion**の出力を示します。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワーク ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 拡張機能 (Ndiskd .dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

 

 






