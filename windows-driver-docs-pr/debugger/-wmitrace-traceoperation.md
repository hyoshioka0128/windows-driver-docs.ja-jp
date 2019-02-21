---
title: wmitrace.traceoperation
description: Wmitrace.traceoperation 拡張機能では、Windows のトレーシング コンポーネントからの進行状況メッセージが表示されます。
ms.assetid: 92d189fe-fb3b-40a6-81a8-9e66868c4d1d
keywords:
- デバッグ wmitrace.traceoperation Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.traceoperation
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f87ca73192cdd724136b772b1f04ada53e35f39a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539387"
---
# <a name="wmitracetraceoperation"></a>!wmitrace.traceoperation


**! Wmitrace.traceoperation**拡張機能では、Windows のトレーシング コンポーネントからの進行状況メッセージが表示されます。

```dbgcmd
!wmitrace.traceoperation {0 | 1 | 2} 
```

## <a name="span-idddkwmitracetraceoperationdbgspanspan-idddkwmitracetraceoperationdbgspanparameters"></a><span id="ddk__wmitrace_traceoperation_dbg"></span><span id="DDK__WMITRACE_TRACEOPERATION_DBG"></span>パラメーター


<span id="_______0______"></span> **0**   
進行状況メッセージをトレースの表示を無効にします。

<span id="_______1______"></span> **1**   
進行状況メッセージをトレースの表示を有効にします。 WMI のトレース デバッガー拡張機能によって生成されたすべてのメッセージが表示されます。

<span id="_______2______"></span> **2**   
進行状況メッセージをトレースの表示を有効にします。 Tracefmt または WMI トレース デバッガー拡張機能によって生成するすべてのメッセージが表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

この拡張機能は、Wmitrace.dll によってエクスポートされます。


### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

イベントのトレースの概念的な概要については、Microsoft Windows SDK を参照してください。

<a name="remarks"></a>注釈
-------

この拡張機能には、詳細な出力を表示するトレースのコンポーネントが原因です。 この機能は、ソフトウェア トレースのトラブルシューティングに役立ちます。

 

 





