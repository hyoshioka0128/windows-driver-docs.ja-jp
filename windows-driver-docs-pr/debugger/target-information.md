---
title: ターゲット情報
description: ターゲット情報
ms.assetid: e818c0bb-ba91-4752-8baf-00fff759106f
keywords:
- エンジン API、ターゲット、情報をデバッガーします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce9c2e26978decf117de974df89ff601ceaf7bd4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366353"
---
# <a name="target-information"></a>ターゲット情報


メソッド[ **GetDebuggeeType** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getdebuggeetype) (たとえば、かどうかは、カーネル モードまたはユーザー モードのターゲット)、現在のターゲットの種類を取得する方法と、[デバッガー エンジン](introduction.md#debugger-engine)はそれに接続します。

ターゲットがクラッシュ ダンプ ファイル ファイル、メソッドがかどうか[ **GetDumpFormatFlags** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getdumpformatflags)ダンプにどのような情報が含まれているが示されます。

### <a name="span-idtargetscomputerspanspan-idtargetscomputerspantargets-computer"></a><span id="target_s_computer"></span><span id="TARGET_S_COMPUTER"></span>ターゲットのコンピューター

ターゲットのコンピューターのページ サイズがによって返される[ **GetPageSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getpagesize)します。 [**IsPointer64Bit** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-ispointer64bit)コンピューターが 32 ビットまたは 64 ビットのアドレスを使用するかどうかを示します。

**注**  内部的には、デバッガー エンジン常に 64 ビットのアドレスを使用、ターゲット。 ターゲットには、32 ビット アドレスでのみ使用している場合、エンジン自動的に変換先と通信するとき。

 

ターゲットのコンピューターのプロセッサの数がによって返される[ **GetNumberProcessors**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getnumberprocessors)します。

ターゲットのコンピューターに関連付けられている 3 つの異なるプロセッサ種類があります。

-   *実際のプロセッサの種類*ターゲットのコンピューターの物理プロセッサの種類です。 これは、によって返される[ **GetActualProcessorType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getactualprocessortype)します。

-   *プロセッサの種類を実行して*現在実行中のプロセッサ コンテキストで使用されるプロセッサの種類です。 これは、によって返される[ **GetExecutingProcessorType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getexecutingprocessortype)します。

-   *有効なプロセッサの種類*はスタック トレースをたとえば--ターゲットからの情報を解釈する、ブレークポイントの設定、レジスタへのアクセスおよび取得するときに、デバッガーを使用して、プロセッサの種類。 有効なプロセッサの種類がによって返される[ **GetEffectiveProcessorType** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-geteffectiveprocessortype)を使用して変更できる[ **SetEffectiveProcessorType** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-seteffectiveprocessortype).

有効なプロセッサの種類と実行中のプロセッサの種類異なる場合があります--実際のプロセッサの種類などの物理プロセッサが x64 では、x86 プロセッサとそれが実行されているモードです。

ターゲットのコンピューター上の物理プロセッサでサポートされているさまざまな実行中のプロセッサ種類がによって返される[ **GetPossibleExecutingProcessorTypes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getpossibleexecutingprocessortypes)します。 これらの数がによって返される[ **GetNumberPossibleExecutingProcessorTypes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getnumberpossibleexecutingprocessortypes)します。

デバッガー エンジンでサポートされているプロセッサの種類の一覧がによって返される[ **GetSupportedProcessorTypes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getsupportedprocessortypes)します。 サポートされているプロセッサの種類の数がによって返される[ **GetNumberSupportedProcessorTypes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getnumbersupportedprocessortypes)します。

プロセッサの種類の名前 (完全と省略形) がによって返される[ **GetProcessorTypeNames**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getprocessortypenames)します。

ターゲットのコンピューターの現在の時刻がによって返される[ **GetCurrentTimeDate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getcurrenttimedate)します。 時間の長さ、ターゲットのコンピューターが実行されている最後のブートがによって返されるため[ **GetCurrentSystemUpTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getcurrentsystemuptime)します。 時刻の情報は、すべてのターゲットにできない場合があります。

### <a name="span-idtargetversionsspanspan-idtargetversionsspantarget-versions"></a><span id="target_versions"></span><span id="TARGET_VERSIONS"></span>ターゲットのバージョン

ターゲットのコンピューターで実行されている Windows バージョンがによって返される[ **GetSystemVersionValues** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol4-getsystemversionvalues)と[**要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugadvanced3-request)操作[**デバッグ\_要求\_取得\_WIN32\_メジャー\_マイナー\_バージョン**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-get-win32-major-minor-versions)、および説明Windows のバージョンがによって返される[ **GetSystemVersionString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol4-getsystemversionstring)します。 この情報の一部がによって返されるも[ **GetSystemVersion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getsystemversion)します。

 

 





