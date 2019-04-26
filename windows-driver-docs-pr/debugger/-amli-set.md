---
title: amli セット
description: Amli セット拡張機能を設定または AMLI デバッガー オプションが表示されます。
ms.assetid: 521fa305-8073-4d94-bc28-fdb35cbc2acd
keywords:
- Windows デバッグ amli の設定
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli set
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e131516c5bf95e19f4277a44ce9a3e59bf175b59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334759"
---
# <a name="amli-set"></a>!amli set


**! Amli セット**拡張機能を設定または AMLI デバッガー オプションが表示されます。

```dbgcmd
    !amli set Options
```

## <a name="span-idddkamlisetdbgspanspan-idddkamlisetdbgspanparameters"></a><span id="ddk__amli_set_dbg"></span><span id="DDK__AMLI_SET_DBG"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
設定する 1 つまたは複数のオプションを指定します。 複数のオプションは、空白で区切ります。 有効な値は次のとおりです。

<span id="spewon"></span><span id="SPEWON"></span>**spewon**  
原因が完全なデバッグ対象のコンピューターから送信される出力です。 このオプションのままにしてですべての時刻 AML デバッグを有効にします。 詳細については、「解説」を参照してください。

<span id="spewoff"></span><span id="SPEWOFF"></span>**spewoff**  
デバッグ出力を抑制します。

<span id="verboseon"></span><span id="VERBOSEON"></span>**verboseon**  
詳細モードをオンにします。 これにより、それらの評価は、AML メソッドの名前を表示する AMLI デバッガーです。

<span id="verboseoff"></span><span id="VERBOSEOFF"></span>**verboseoff**  
詳細モードをオフにします。

<span id="traceon"></span><span id="TRACEON"></span>**traceon**  
ACPI のトレースをアクティブにします。 もさらに多くの出力が生成されます、 **verboseon**オプション。 このオプションは、SMI 関連ハード ハングを追跡するのに便利です。

<span id="traceoff"></span><span id="TRACEOFF"></span>**traceoff**  
ACPI のトレースを無効になります。

<span id="nesttraceon"></span><span id="NESTTRACEON"></span>**nesttraceon**  
入れ子のトレースをアクティブにします。 このオプションは、唯一の有効な場合、 **traceon**オプションも選択します。

<span id="dbgbrkon"></span><span id="DBGBRKON"></span>**dbgbrkon**  
AMLI デバッガーで中断できるようにします。

<span id="dbgbrkoff"></span><span id="DBGBRKOFF"></span>**dbgbrkoff**  
Dbgbrkon オプションを無効になります。

<span id="nesttraceoff"></span><span id="NESTTRACEOFF"></span>**nesttraceoff**  
入れ子のトレースを無効になります。

<span id="lbrkon"></span><span id="LBRKON"></span>**lbrkon**  
DDB 読み込みが完了したときに、AMLI デバッガーを中断します。

<span id="lbrkoff"></span><span id="LBRKOFF"></span>**lbrkoff**  
非アクティブ化、 **lbrkon**オプション。

<span id="errbrkon"></span><span id="ERRBRKON"></span>**errbrkon**  
インタープリター AML コードの評価の問題があるたびに、AMLI デバッガーを中断します。

<span id="errbrkoff"></span><span id="ERRBRKOFF"></span>**errbrkoff**  
非アクティブ化、 **errbrkon**オプション。

<span id="logon"></span><span id="LOGON"></span>**logon**  
イベントのログ記録を有効にします。

<span id="logoff"></span><span id="LOGOFF"></span>**ログオフ**  
イベントのログ記録を無効にします。

<span id="logmuton"></span><span id="LOGMUTON"></span>**logmuton**  
ミュー テックス イベントのログ記録を有効にします。

<span id="logmutoff"></span><span id="LOGMUTOFF"></span>**logmutoff**  
ミュー テックス イベントのログ記録を無効にします。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

関連するコマンドとその用途については、次を参照してください。 [AMLI デバッガー](the-amli-debugger.md)します。

<a name="remarks"></a>コメント
-------

オプションが指定されていない場合は、すべてのオプションの現在の状態が表示されます。

既定では、多くのメッセージがフィルター アウトされて、これに出力を有効にする必要があります **! amli 設定 spewon**します。 それ以外の場合、AMLI デバッガーの多数のメッセージはすべて失われます。

AML インタープリターは AMLI デバッガーを中断、この出力は自動的に有効になります。

この出力のフィルター処理の詳細については、次を参照してください。 **DbgPrintEx**と**KdPrintEx** Windows Driver Kit (WDK) ドキュメントです。

 

 





