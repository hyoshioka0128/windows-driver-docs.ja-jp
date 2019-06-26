---
title: ndiskd.ndisstack
description: '! Ndiskd.ndisstack 拡張機能には、デバッグのスタック トレースが表示されます。'
ms.assetid: 939DEC34-3D20-41FE-B5A8-DDF810195B07
keywords:
- デバッグ ndiskd.ndisstack Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ndisstack
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7ae7153034b14a0b7061e55c2bbfd5ddd3da45a6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362485"
---
# <a name="ndiskdndisstack"></a>!ndiskd.ndisstack


**注**  サード パーティ製ネットワーク ドライバー開発者が手動でこの拡張機能のコマンドを使用する必要はありません。 表示される情報を表示することを行うことができますが、ドライバー、詳細を再利用できません。

 

**! Ndiskd.ndisstack**拡張機能には、デバッグのスタック トレースが表示されます。

```console
!ndiskd.ndisstack [-handle <x>] [-statistics] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必須。 スタックのブロックのハンドル。

<span id="_______-statistics______"></span><span id="_______-STATISTICS______"></span> *統計情報*   
デバッグ統計情報を示しています。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

 

 






