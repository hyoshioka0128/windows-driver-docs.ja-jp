---
title: WdbgExts のメモリ アクセス
description: WdbgExts のメモリ アクセス
ms.assetid: 7b600d18-343e-4c22-b1e9-5dcc83d88695
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 845b4ca00a6e1a5c9398302422446f7795216e2f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834177"
---
# <a name="wdbgexts-memory-access"></a>WdbgExts のメモリ アクセス


このトピックでは、WdbgExts API を使用してメモリアクセスを実行する方法の概要について説明します。 [デバッガーエンジン](introduction.md#debugger-engine)でのメモリアクセスの概要については、このドキュメントの「[デバッガーエンジンの概要](debugger-engine-overview.md)」セクションの「[メモリ](memory.md)」を参照してください。

### <a name="span-idvirtual_memoryspanspan-idvirtual_memoryspanvirtual-memory"></a><span id="virtual_memory"></span><span id="VIRTUAL_MEMORY"></span>仮想メモリ

ターゲットの仮想メモリは、 [**Readmemory**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff554287(v=vs.85))関数を使用して読み取ることができ、 [**WriteMemory**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff561420(v=vs.85))関数を使用して記述されます。 ターゲットのメモリ内のポインターは、 [**Readpointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readpointer)関数、 [**readpointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readptr)関数、および[**writepointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writepointer)関数を使用して読み書きできます。

仮想メモリでバイトのパターンを検索するには、 [**Searchmemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-searchmemory)関数を使用します。

[**TranslateVirtualToPhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-translatevirtualtophysical)関数は、仮想メモリアドレスを物理メモリアドレスに変換するために使用できます。

[**Disasm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_disasm)関数を使用すると、ターゲットで1つのアセンブリ命令を逆アセンブルできます。

物理アドレス拡張 (PAE) を使用しているときに、4 GB 未満のメモリが破損していないかどうかを確認するには、 [ **\_LOWMEM\_チェック**](https://docs.microsoft.com/previous-versions/ff550931(v=vs.85))の[**Ioctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作を使用します。

### <a name="span-idphysical_memoryspanspan-idphysical_memoryspanphysical-memory"></a><span id="physical_memory"></span><span id="PHYSICAL_MEMORY"></span>物理メモリ

カーネルモードのデバッグでは、物理メモリに直接アクセスできます。

ターゲットの物理メモリは、 [**Readphysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readphysical)および[**readphysicalwithflags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readphysicalwithflags)関数を使用して読み取ることができ、 [**Writephysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writephysical)および[**writephysicalwithflags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writephysicalwithflags)関数を使用して記述されます。

物理メモリで指定された範囲内の場所へのポインターを検索するには、 [**Ioctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作[**IG\_ポインター\_検索\_物理**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_pointer_search_physical)を使用します。

### <a name="span-idother_data_spacesspanspan-idother_data_spacesspanother-data-spaces"></a><span id="other_data_spaces"></span><span id="OTHER_DATA_SPACES"></span>その他のデータ領域

カーネルモードのデバッグでは、メインメモリに加えて、さまざまなデータ領域に対してデータの読み取りと書き込みを行うことができます。 次のデータ領域にアクセスできます。

<span id="Control-Space_Memory"></span><span id="control-space_memory"></span><span id="CONTROL-SPACE_MEMORY"></span>制御領域のメモリ  
関数[**Readcontrolspace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readcontrolspace)、 [**ReadControlSpace64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readcontrolspace64)、 [**ReadTypedControlSpace32**](https://docs.microsoft.com/previous-versions/ff554339(v=vs.85))、および[**ReadTypedControlSpace64**](https://docs.microsoft.com/previous-versions/ff554341(v=vs.85))は、コントロールスペースからデータを読み取ります。 [**WriteControlSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writecontrolspace)関数は、コントロール領域にデータを書き込みます。

<span id="I_O_Memory"></span><span id="i_o_memory"></span><span id="I_O_MEMORY"></span>I/o メモリ  
関数[**ReadIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readiospace)、 [**ReadIoSpace64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readiospace64)、 **ReadIoSpace64**、 [**ReadIoSpaceEx64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readiospaceex64)は、システム i/o メモリおよびバス i/o メモリからデータを読み取ります。 関数[**WriteIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writeiospace)、 [**WriteIoSpace64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writeiospace64)、 [**WriteIoSpaceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writeiospaceex)、および[**WriteIoSpaceEx64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writeiospaceex64)は、システム i/o メモリおよびバス i/o メモリにデータを書き込みます。

<span id="Model_Specific_Register__MSR_"></span><span id="model_specific_register__msr_"></span><span id="MODEL_SPECIFIC_REGISTER__MSR_"></span>モデル固有レジスタ (MSR)  
[**Readmsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readmsr)および[**writemsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writemsr)の関数は、MSRs の読み取りと書き込みを行います。

<span id="System_Bus"></span><span id="system_bus"></span><span id="SYSTEM_BUS"></span>システムバス  
[**Ioctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作の ig\_は、**バス\_データ**の読み取りと書き込みを行う[ **\_バス\_データを取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_getsetbusdata)し、システムバスデータを書き込むように設定\_ます。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

より強力なメモリアクセス API については、このドキュメントの「[デバッガーエンジン API の使用](using-the-debugger-engine-api.md)」セクションの「[メモリアクセス](memory-access.md)」を参照してください。

 

 





