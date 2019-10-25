---
title: ndiskd ndisstack
description: '! Ndiskd ndisstack 拡張機能は、デバッグスタックトレースを表示します。'
ms.assetid: 939DEC34-3D20-41FE-B5A8-DDF810195B07
keywords:
- ndisstack Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ndisstack
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 00e6ffb04f3c6420e59f3f26e938817d788483de
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837579"
---
# <a name="ndiskdndisstack"></a>!ndiskd.ndisstack


**注**  サードパーティのネットワークドライバーの開発者は、この拡張機能コマンドを手動で使用することは想定されていません。 これを実行すると表示される情報を確認できますが、ドライバーで提供される詳細を再利用することはできません。

 

**! Ndiskd ndisstack**拡張機能は、デバッグスタックトレースを表示します。

```console
!ndiskd.ndisstack [-handle <x>] [-statistics] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-  を処理*します  
必須。 スタックブロックのハンドル。

<span id="_______-statistics______"></span><span id="_______-STATISTICS______"></span> *-統計*   
デバッグの統計情報を表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワークドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd .dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **! ndiskd ヘルプ**](-ndiskd-help.md)

 

 






