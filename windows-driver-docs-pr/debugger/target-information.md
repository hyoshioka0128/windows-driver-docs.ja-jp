---
title: ターゲット情報
description: ターゲット情報
ms.assetid: e818c0bb-ba91-4752-8baf-00fff759106f
keywords:
- デバッガーエンジン API、ターゲット、情報
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f7fe85783098b7611a4290f9ab2f756cf28a809
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534285"
---
# <a name="target-information"></a>ターゲット情報


[**Getdebuggeetype**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getdebuggeetype)メソッドは、現在のターゲットの性質 (カーネルモードまたはユーザーモードターゲットであるかどうかなど) と、[デバッガーエンジン](introduction.md#debugger-engine)がどのように接続されているかを返します。

ターゲットがクラッシュダンプファイルファイルの場合、 [**Getdumpformatflags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getdumpformatflags)メソッドはダンプに含まれている情報を示します。

### <a name="span-idtarget_s_computerspanspan-idtarget_s_computerspantargets-computer"></a><span id="target_s_computer"></span><span id="TARGET_S_COMPUTER"></span>ターゲットのコンピューター

ターゲットのコンピューターのページサイズは、 [**GetPageSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getpagesize)によって返されます。 [**IsPointer64Bit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-ispointer64bit)は、コンピューターが32ビットまたは64ビットのどちらのアドレスを使用しているかを示します。

**メモ**   内部的には、デバッガーエンジンは常にターゲットの64ビットアドレスを使用します。 ターゲットが32ビットのアドレスのみを使用する場合、エンジンはターゲットと通信するときにそれらを自動的に変換します。

 

ターゲットのコンピューターのプロセッサ数は、 [**Getnumber processor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getnumberprocessors)によって返されます。

ターゲットのコンピューターには、次の3種類のプロセッサが関連付けられています。

-   *実際のプロセッサの種類*は、ターゲットのコンピューターの物理プロセッサの種類です。 これは、 [**Getactualprocessortype**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getactualprocessortype)によって返されます。

-   実行中のプロセッサの*種類*は、現在実行中のプロセッサコンテキストで使用されるプロセッサの種類です。 これは、 [**Getexecutingprocessortype**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getexecutingprocessortype)によって返されます。

-   *有効なプロセッサの種類*は、デバッガーがターゲットから情報を解釈するときに使用するプロセッサの種類です。たとえば、ブレークポイントの設定、レジスタへのアクセス、スタックトレースの取得などです。 有効なプロセッサの種類は[**GetEffectiveProcessorType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-geteffectiveprocessortype)によって返され、 [**SetEffectiveProcessorType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-seteffectiveprocessortype)を使用して変更できます。

有効なプロセッサの種類と実行中のプロセッサの種類は、実際のプロセッサの種類とは異なる場合があります。たとえば、物理プロセッサが x64 プロセッサで、x86 モードで実行されている場合などです。

ターゲットのコンピューターの物理プロセッサによってサポートされている、異なる実行中のプロセッサの種類が、 [**Get、Executingprocessortypes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getpossibleexecutingprocessortypes)によって返されます。 これらの数は、 [**Getnumber 型の Executingprocessortypes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getnumberpossibleexecutingprocessortypes)によって返されます。

デバッガーエンジンによってサポートされるプロセッサの種類の一覧は、 [**Getsupportedprocessortypes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getsupportedprocessortypes)によって返されます。 サポートされているプロセッサの種類の数は、 [**Getnumber Supportedprocessortypes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getnumbersupportedprocessortypes)によって返されます。

プロセッサの種類の名前 (完全および省略形) は、 [**GetProcessorTypeNames**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getprocessortypenames)によって返されます。

ターゲットのコンピューターの現在の時刻が[**Getcurrenttimedate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getcurrenttimedate)によって返されます。 前回の起動以降に、ターゲットのコンピューターが実行されていた時間の[**長さ。**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getcurrentsystemuptime) 時間情報は、すべてのターゲットで使用できるとは限りません。

### <a name="span-idtarget_versionsspanspan-idtarget_versionsspantarget-versions"></a><span id="target_versions"></span><span id="TARGET_VERSIONS"></span>ターゲットバージョン

ターゲットのコンピューターで実行されている Windows バージョンは[**GetSystemVersionValues**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-getsystemversionvalues)によって返され、[**要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugadvanced3-request)操作[**デバッグ \_ 要求は \_ \_ WIN32 \_ メジャー \_ マイナー \_ バージョンを取得**](debug-request-get-win32-major-minor-versions.md)し、Windows バージョンの説明は[**GetSystemVersionString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-getsystemversionstring)によって返されます。 この情報の一部は、 [**GetSystemVersion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getsystemversion)によっても返されます。

 

 





