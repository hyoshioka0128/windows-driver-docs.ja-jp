---
title: wmitrace.dynamicprint
description: Wmitrace.dynamicprint 拡張機能では、デバッガーが KD_FILTER_MODE で実行されているセッションで生成されたトレース メッセージを表示するかどうかを制御します。
ms.assetid: 458a9dfa-e3cc-4652-a9e5-5098a962f1c7
keywords:
- デバッグ wmitrace.dynamicprint Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.dynamicprint
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e7cb0158b16894603df4abf156196fd179904eab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528623"
---
# <a name="wmitracedynamicprint"></a>!wmitrace.dynamicprint


**! Wmitrace.dynamicprint**拡張機能は、デバッガーが KD で実行されているセッションで生成されたトレース メッセージを表示するかどうかを制御\_フィルター\_モード。

```dbgcmd
!wmitrace.dynamicprint {0 | 1}
```

## <a name="span-idddkwmitracedynamicprintdbgspanspan-idddkwmitracedynamicprintdbgspanparameters"></a><span id="ddk__wmitrace_dynamicprint_dbg"></span><span id="DDK__WMITRACE_DYNAMICPRINT_DBG"></span>パラメーター


<span id="_______0______"></span> **0**   
トレース メッセージの表示をオフにします。

<span id="_______1______"></span> **1**   
トレース メッセージの表示をオンにします。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

この拡張機能は、Wmitrace.dll によってエクスポートされます。

この拡張機能は、Windows 2000 以降のバージョンの Windows で使用できます。 Windows 2000 でこの拡張機能を使用する場合は、w2kfre サブディレクトリに Wmitrace.dll ファイルを Windows 内のデバッグ ツールのインストール ディレクトリの winxp サブディレクトリからまずコピーする必要があります。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

イベントのトレースの概念的な概要については、Microsoft Windows SDK を参照してください。 トレース セッションの開始時にヘルプは、Windows Driver Kit (WDK) で「トレース ログ」を参照してください。

<a name="remarks"></a>注釈
-------

この拡張機能を使用する前に、トレース セッションを開始し、デバッガーにトレース メッセージを送信する必要がありますを指定します。 たとえば、 [ **! wmitrace.start** ](-wmitrace-start.md)がセッションを開始するには使用、 **-kd**パラメーター。 トレース ログを使用してトレース セッションを開始する場合を使用して、その **-kd**パラメーター。 トレース ログ (tracelog.exe) は、Windows ドライバー キットに含まれるトレース コント ローラーです。

トレース メッセージは、ターゲット コンピューター上のバッファーに保持されます。 これらのバッファーがフラッシュされ、一定の間隔で、ホスト コンピューター上のデバッガーに送信します。 フラッシュ タイマーの間隔を指定して、 **-kd**のパラメーター、 [ **! wmitrace.start** ](-wmitrace-start.md)コマンドまたは **-kd**のパラメータートレース ログ ツールです。 Windows 8 以降、する値を指定できますフラッシュ タイマー (ミリ秒単位) を追加して**ms**フラッシュ タイマー値にします。

既定では、ETW は、ターゲット コンピューターのプロセッサあたりトレース バッファーを保持します。 トレース バッファーがフラッシュされ、ホスト コンピューター上のデバッガーに送信されるとき、に、時系列の一連のイベント バッファーをマージするためのメカニズムはありません。 ように、順不同のイベントを表示する可能性があります。 Windows 7 以降、問題を解決するこの設定によって、 **- lowcapacity**トレース ログ ツールを使用してトレース セッションを開始するときにパラメーター。

**Tracelog** *MySession* **-kd lowcapacity**

セッションを開始するときに **- lowcapacity**設定すると、対象のコンピューターに、すべてのイベントが 1 つのバッファーに移動し、イベントがデバッガー ホスト コンピューター上で正しい順序で表示されます。

また、この拡張機能を使用する前に次のように使用します[ **! wmitrace.searchpath** ](-wmitrace-searchpath.md)または[ **! wmitrace.tmffile** ](-wmitrace-tmffile.md)トレース メッセージの形式を指定するには。ファイル。 システムでは、人間が判読できるテキストとして表示できるように、バイナリのトレース メッセージを書式設定するのにトレース メッセージのフォーマット ファイルを使用します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**!wmitrace.start**](-wmitrace-start.md)

 

 






