---
title: その他のデータ領域
description: その他のデータ領域
ms.assetid: f676a478-c02a-4400-8173-a1b3103c6c1b
keywords:
- デバッガーのエンジンの API、メモリ、データ領域
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6b036d66aa8406a2282e2f5f2a308ebe8ad9049
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366441"
---
# <a name="other-data-spaces"></a>その他のデータ領域


## <span id="ddk_other_data_spaces_dbx"></span><span id="DDK_OTHER_DATA_SPACES_DBX"></span>


カーネル モードのデバッグ、さまざまなメイン メモリやレジスタに加えてデータ領域にデータを読み書きすることです。 次のデータ領域にアクセスできます。

<span id="System_Bus"></span><span id="system_bus"></span><span id="SYSTEM_BUS"></span>システム バス  
メソッド[ **ReadBusData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-readbusdata)と[ **WriteBusData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-writebusdata)システム バス データを読み書きします。

<span id="Control-Space_Memory"></span><span id="control-space_memory"></span><span id="CONTROL-SPACE_MEMORY"></span>コントロールの領域のメモリ  
メソッド[ **ReadControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-readcontrol)と[ **WriteControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-writecontrol)コントロール領域のメモリを読み書きします。

<span id="i_o_memory."></span><span id="I_O_MEMORY."></span>I/O メモリ。  
メソッド[ **ReadIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-readio)と[ **WriteIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-writeio)読み取りおよびシステムを書き込み、および I/O メモリ バスします。

<span id="Model_Specific_Register__MSR_"></span><span id="model_specific_register__msr_"></span><span id="MODEL_SPECIFIC_REGISTER__MSR_"></span>モデル専用レジスタ (MSR)  
メソッド[ **ReadMsr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-readmsr)と[ **WriteMsr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-writemsr) 、制御レジスタを有効にして、機能を無効にするには、MSRs の読み書きとデバッグ、CPU の特定のモデルをサポートします。

### <a name="span-idhandlesspanspan-idhandlesspan-handles"></a><span id="handles"></span><span id="HANDLES"></span> ハンドル

ユーザー モードのデバッグは、ターゲット プロセスによって所有されているシステム ハンドルを使用してシステム オブジェクトに関する情報を取得できます。 メソッド[ **ReadHandleData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-readhandledata)この情報を読み取ることができます。

スレッドとプロセスのシステム オブジェクトに対してシステム ハンドルを使用して取得できます、 [ **GetCurrentThreadHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentthreadhandle)と[ **GetCurrentProcessHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects-getcurrentprocesshandle)メソッド。 これらのハンドルにも用意されています、 [ **IDebugEventCallbacks::CreateThread** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugeventcallbacks-createthread)と[ **IDebugEventCallbacks::CreateProcess** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugeventcallbacks-createprocess)複数のスレッドが作成し、作成プロセスのデバッグ イベントが発生したときのコールバック メソッド。

**注**  カーネル モードでプロセスとスレッドのハンドルには、人為的なハンドル。 処理システムではありません。

 

 

 





