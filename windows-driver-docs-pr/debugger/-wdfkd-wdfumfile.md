---
title: wdfkd.wdfumfile
description: Wdfkd.wdfumfile 拡張機能には、UMDF のスタック内のファイルに関する情報が表示されます。
ms.assetid: AAE9E003-829D-4A52-8F67-58DFE15D5D3C
keywords:
- デバッグ wdfkd.wdfumfile Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfumfile
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1d20f4369ef1a3cb5fdf21db7ad432ee263fb7ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553062"
---
# <a name="wdfkdwdfumfile"></a>!wdfkd.wdfumfile


**! Wdfkd.wdfumfile**拡張機能は、UMDF のスタック内のファイルに関する情報を表示します。

```dbgcmd
!wdfkd.wdfumfile Address 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
に関する情報を表示 UMDF のスタック内のファイルのアドレスを指定します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク


UMDF 2

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


詳細については、[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)を参照してください。

<a name="remarks"></a>注釈
-------

または UMDF ホスト プロセス (wudfhost.exe) に関連付けられているユーザー モードのデバッグ セッションでカーネル モードのデバッグ セッションでは、このコマンドを使用することができます。

このコマンドは、ユーザー モードのコマンドと同じ情報を表示します[ **! wudfext.umfile**](-wudfext-umfile.md)します。

 

 





