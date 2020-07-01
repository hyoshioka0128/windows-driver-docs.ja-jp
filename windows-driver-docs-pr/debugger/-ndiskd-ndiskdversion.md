---
title: ndiskd ndiskdversion
description: Ndiskd. ndiskdversion 拡張機能には、ndiskd 自体に関する情報が表示されます。
ms.assetid: 12EB9E0F-7D2F-447B-B678-1E23EFF522FE
keywords:
- ndiskd. ndiskdversion Windows デバッグ
ms.date: 06/11/2020
topic_type:
- apiref
api_name:
- ndiskd.ndiskdversion
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 887ff00c3e2a277862de67aade636184358d489d
ms.sourcegitcommit: 8596782b07c8a71adf38fc2c2da68b75ba0a1259
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85593928"
---
# <a name="ndiskdndiskdversion"></a>!ndiskd.ndiskdversion

! **Ndiskd. ndiskdversion**拡張機能に関する情報が表示されます。

```console
!ndiskd.ndiskdversion
```

## <a name="parameters"></a>パラメーター

この拡張機能にはパラメーターがありません。

## <a name="dll"></a>[DLL]

Ndiskd.dll

## <a name="examples"></a>例

次の例では、 **! ndiskd. ndiskdversion**の出力を示します。

```console
0: kd> !ndiskd.ndiskdversion
    NDISKD Version     17.08.00 (NDISKD codename "We'll deploy IPv6 real soon now")
    Build              Release
    Debugger CPU       AMD64
    Hyperlinks (DML)   Enabled
    Unicode            Enabled
    Debug NDISKD       Disabled
```

## <a name="see-also"></a>関連項目

[ネットワーク ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)
