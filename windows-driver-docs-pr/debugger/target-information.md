---
title: ターゲット情報
description: ターゲット情報
ms.assetid: e818c0bb-ba91-4752-8baf-00fff759106f
keywords:
- エンジン API、ターゲット、情報をデバッガーします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42ffc3a38260c6a2e54963a8e4118d9177929a4b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335450"
---
# <a name="target-information"></a>ターゲット情報


メソッド[ **GetDebuggeeType** ](https://msdn.microsoft.com/library/windows/hardware/ff546559) (たとえば、かどうかは、カーネル モードまたはユーザー モードのターゲット)、現在のターゲットの種類を取得する方法と、[デバッガー エンジン](introduction.md#debugger-engine)はそれに接続します。

ターゲットがクラッシュ ダンプ ファイル ファイル、メソッドがかどうか[ **GetDumpFormatFlags** ](https://msdn.microsoft.com/library/windows/hardware/ff546592)ダンプにどのような情報が含まれているが示されます。

### <a name="span-idtargetscomputerspanspan-idtargetscomputerspantargets-computer"></a><span id="target_s_computer"></span><span id="TARGET_S_COMPUTER"></span>ターゲットのコンピューター

ターゲットのコンピューターのページ サイズがによって返される[ **GetPageSize**](https://msdn.microsoft.com/library/windows/hardware/ff548086)します。 [**IsPointer64Bit** ](https://msdn.microsoft.com/library/windows/hardware/ff551092)コンピューターが 32 ビットまたは 64 ビットのアドレスを使用するかどうかを示します。

**注**  内部的には、デバッガー エンジン常に 64 ビットのアドレスを使用、ターゲット。 ターゲットには、32 ビット アドレスでのみ使用している場合、エンジン自動的に変換先と通信するとき。

 

ターゲットのコンピューターのプロセッサの数がによって返される[ **GetNumberProcessors**](https://msdn.microsoft.com/library/windows/hardware/ff547950)します。

ターゲットのコンピューターに関連付けられている 3 つの異なるプロセッサ種類があります。

-   *実際のプロセッサの種類*ターゲットのコンピューターの物理プロセッサの種類です。 これは、によって返される[ **GetActualProcessorType**](https://msdn.microsoft.com/library/windows/hardware/ff545572)します。

-   *プロセッサの種類を実行して*現在実行中のプロセッサ コンテキストで使用されるプロセッサの種類です。 これは、によって返される[ **GetExecutingProcessorType**](https://msdn.microsoft.com/library/windows/hardware/ff546670)します。

-   *有効なプロセッサの種類*はスタック トレースをたとえば--ターゲットからの情報を解釈する、ブレークポイントの設定、レジスタへのアクセスおよび取得するときに、デバッガーを使用して、プロセッサの種類。 有効なプロセッサの種類がによって返される[ **GetEffectiveProcessorType** ](https://msdn.microsoft.com/library/windows/hardware/ff546595)を使用して変更できる[ **SetEffectiveProcessorType** ](https://msdn.microsoft.com/library/windows/hardware/ff556657).

有効なプロセッサの種類と実行中のプロセッサの種類異なる場合があります--実際のプロセッサの種類などの物理プロセッサが x64 では、x86 プロセッサとそれが実行されているモードです。

ターゲットのコンピューター上の物理プロセッサでサポートされているさまざまな実行中のプロセッサ種類がによって返される[ **GetPossibleExecutingProcessorTypes**](https://msdn.microsoft.com/library/windows/hardware/ff548130)します。 これらの数がによって返される[ **GetNumberPossibleExecutingProcessorTypes**](https://msdn.microsoft.com/library/windows/hardware/ff547939)します。

デバッガー エンジンでサポートされているプロセッサの種類の一覧がによって返される[ **GetSupportedProcessorTypes**](https://msdn.microsoft.com/library/windows/hardware/ff548438)します。 サポートされているプロセッサの種類の数がによって返される[ **GetNumberSupportedProcessorTypes**](https://msdn.microsoft.com/library/windows/hardware/ff547966)します。

プロセッサの種類の名前 (完全と省略形) がによって返される[ **GetProcessorTypeNames**](https://msdn.microsoft.com/library/windows/hardware/ff548169)します。

ターゲットのコンピューターの現在の時刻がによって返される[ **GetCurrentTimeDate**](https://msdn.microsoft.com/library/windows/hardware/ff546553)します。 時間の長さ、ターゲットのコンピューターが実行されている最後のブートがによって返されるため[ **GetCurrentSystemUpTime**](https://msdn.microsoft.com/library/windows/hardware/ff545883)します。 時刻の情報は、すべてのターゲットにできない場合があります。

### <a name="span-idtargetversionsspanspan-idtargetversionsspantarget-versions"></a><span id="target_versions"></span><span id="TARGET_VERSIONS"></span>ターゲットのバージョン

ターゲットのコンピューターで実行されている Windows バージョンがによって返される[ **GetSystemVersionValues** ](https://msdn.microsoft.com/library/windows/hardware/ff549258)と[**要求**](https://msdn.microsoft.com/library/windows/hardware/ff554564)操作[**デバッグ\_要求\_取得\_WIN32\_メジャー\_マイナー\_バージョン**](https://msdn.microsoft.com/library/windows/hardware/ff541563)、および説明Windows のバージョンがによって返される[ **GetSystemVersionString**](https://msdn.microsoft.com/library/windows/hardware/ff549245)します。 この情報の一部がによって返されるも[ **GetSystemVersion**](https://msdn.microsoft.com/library/windows/hardware/ff549234)します。

 

 





