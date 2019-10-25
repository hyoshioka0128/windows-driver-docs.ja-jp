---
title: その他のデータ領域
description: その他のデータ領域
ms.assetid: f676a478-c02a-4400-8173-a1b3103c6c1b
keywords:
- デバッガーエンジン API、メモリ、データ領域
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e9072eebe7d1259d22c2bf40643302707a3761b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838821"
---
# <a name="other-data-spaces"></a>その他のデータ領域


## <span id="ddk_other_data_spaces_dbx"></span><span id="DDK_OTHER_DATA_SPACES_DBX"></span>


カーネルモードのデバッグでは、メインメモリとレジスタに加えて、さまざまなデータ領域に対してデータの読み取りと書き込みを行うことができます。 次のデータ領域にアクセスできます。

<span id="System_Bus"></span><span id="system_bus"></span><span id="SYSTEM_BUS"></span>システムバス  
[**Readbusdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readbusdata)および[**writebusdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-writebusdata)メソッドは、システムバスデータの読み取りと書き込みを行います。

<span id="Control-Space_Memory"></span><span id="control-space_memory"></span><span id="CONTROL-SPACE_MEMORY"></span>制御領域のメモリ  
[**Readcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readcontrol)と[**writecontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-writecontrol)のメソッドは、読み取りと書き込みの制御領域のメモリを確保します。

<span id="i_o_memory."></span><span id="I_O_MEMORY."></span>I/o メモリ。  
これらのメソッドは、 [**ReadIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readio)と[**WriteIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-writeio)によって、システムおよびバス i/o メモリの読み取りと書き込みを行います。

<span id="Model_Specific_Register__MSR_"></span><span id="model_specific_register__msr_"></span><span id="MODEL_SPECIFIC_REGISTER__MSR_"></span>モデル固有レジスタ (MSR)  
[**Readmsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readmsr)と[**writemsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writemsr)の読み取りと書き込みのメソッドは、特定の CPU モデルに対して機能を有効または無効にし、デバッグをサポートするコントロールレジスタです。

### <a name="span-idhandlesspanspan-idhandlesspan-handles"></a><span id="handles"></span><span id="HANDLES"></span>対応

ユーザーモードのデバッグでは、ターゲットプロセスによって所有されているシステムハンドルを使用して、システムオブジェクトに関する情報を取得できます。 メソッド[**Readhandledata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readhandledata)を使用して、この情報を読み取ることができます。

スレッドおよびプロセスシステムオブジェクトのシステムハンドルは、 [**Getcurrentthreadhandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentthreadhandle)メソッドと[**GetCurrentProcessHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects-getcurrentprocesshandle)メソッドを使用して取得できます。 これらのハンドルは、 [**IDebugEventCallbacks:: CreateThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugeventcallbacks-createthread)および[**IDebugEventCallbacks:: CreateProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugeventcallbacks-createprocess)コールバックメソッドにも用意されています。これは、スレッドの作成とプロセスのデバッグイベントが発生したときに行われます。

**注**   カーネルモードでは、プロセスハンドルとスレッドハンドルは人工ハンドルです。 これらはシステムハンドルではありません。

 

 

 





