---
title: WdbgExts のメモリ アクセス
description: WdbgExts のメモリ アクセス
ms.assetid: 7b600d18-343e-4c22-b1e9-5dcc83d88695
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1d934e1916f032bd3186a18a9275163e53dfe7c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369438"
---
# <a name="wdbgexts-memory-access"></a>WdbgExts のメモリ アクセス


このトピックでは、メモリにアクセスする方法の概要は WdbgExts API を使用して実行できます。 メモリ アクセスの概要については、[デバッガー エンジン](introduction.md#debugger-engine)を参照してください[メモリ](memory.md)で、[デバッガー エンジンの概要](debugger-engine-overview.md)このドキュメントの「します。

### <a name="span-idvirtualmemoryspanspan-idvirtualmemoryspanvirtual-memory"></a><span id="virtual_memory"></span><span id="VIRTUAL_MEMORY"></span>仮想メモリ

使用して、ターゲットの仮想メモリを読み取ることができます、 [ **ReadMemory** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff554287(v=vs.85))関数とを使用して、 [ **WriteMemory** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff561420(v=vs.85))関数。 ターゲットのメモリ内のポインターを読み取りを使用して書き込むことができます、 [ **ReadPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-readpointer)、 [ **ReadPtr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-readptr)、および[ **WritePointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-writepointer)関数。

仮想メモリのバイトのパターンを検索するには、使用、 [ **SearchMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-searchmemory)関数。

[ **TranslateVirtualToPhysical** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-translatevirtualtophysical)仮想メモリ アドレスを物理メモリ アドレスに変換する関数を使用できます。

[ **Disasm** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_disasm)ターゲット上の 1 つのアセンブリ命令を逆アセンブルする関数を使用できます。

物理アドレス拡張 (PAE) を使用する場合は、低の 4 GB のメモリの破損を確認するには、使用、 [ **Ioctl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作[ **IG\_LOWMEM\_確認**](https://docs.microsoft.com/previous-versions/ff550931(v=vs.85))します。

### <a name="span-idphysicalmemoryspanspan-idphysicalmemoryspanphysical-memory"></a><span id="physical_memory"></span><span id="PHYSICAL_MEMORY"></span>物理メモリ

カーネル モードのデバッグで物理メモリに直接アクセスのみできます。

使用して、ターゲット上の物理メモリを読み取ることができます、 [ **ReadPhysical** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-readphysical)と[ **ReadPhysicalWithFlags** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-readphysicalwithflags)関数、と書き込み使用して、 [ **WritePhysical** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-writephysical)と[ **WritePhysicalWithFlags** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-writephysicalwithflags)関数。

指定した範囲内の場所へのポインターの物理メモリを検索するには、使用、 [ **Ioctl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作[ **IG\_ポインター\_検索\_物理**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_pointer_search_physical)します。

### <a name="span-idotherdataspacesspanspan-idotherdataspacesspanother-data-spaces"></a><span id="other_data_spaces"></span><span id="OTHER_DATA_SPACES"></span>その他のデータ領域

カーネル モードのデバッグは、さまざまなメイン メモリだけでなくデータ領域にデータを読み書きすることです。 次のデータ領域にアクセスできます。

<span id="Control-Space_Memory"></span><span id="control-space_memory"></span><span id="CONTROL-SPACE_MEMORY"></span>コントロールの領域のメモリ  
関数は、 [ **ReadControlSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-readcontrolspace)、 [ **ReadControlSpace64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-readcontrolspace64)、 [ **ReadTypedControlSpace32**](https://docs.microsoft.com/previous-versions/ff554339(v=vs.85))、および[ **ReadTypedControlSpace64** ](https://docs.microsoft.com/previous-versions/ff554341(v=vs.85))コントロール領域からデータを読み取ります。 [ **WriteControlSpace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-writecontrolspace)関数は、コントロールの領域にデータを書き込みます。

<span id="I_O_Memory"></span><span id="i_o_memory"></span><span id="I_O_MEMORY"></span>I/O メモリ  
関数は、 [ **ReadIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-readiospace)、 [ **ReadIoSpace64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-readiospace64)、 **ReadIoSpace64**、 [**ReadIoSpaceEx64** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-readiospaceex64)は、システム I/O メモリからデータを読み取り、I/O メモリ バスします。 関数は、 [ **WriteIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-writeiospace)、 [ **WriteIoSpace64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-writeiospace64)、 [ **WriteIoSpaceEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-writeiospaceex)、および[ **WriteIoSpaceEx64** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-writeiospaceex64)はシステム I/O メモリにデータを記述し、I/O メモリ バスします。

<span id="Model_Specific_Register__MSR_"></span><span id="model_specific_register__msr_"></span><span id="MODEL_SPECIFIC_REGISTER__MSR_"></span>モデル専用レジスタ (MSR)  
関数は、 [ **ReadMsr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-readmsr)と[ **WriteMsr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-writemsr) MSRs を読み書きします。

<span id="System_Bus"></span><span id="system_bus"></span><span id="SYSTEM_BUS"></span>システム バス  
[ **Ioctl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作[ **IG\_取得\_BUS\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_getsetbusdata)と**IG\_設定\_BUS\_データ**システム バス データを読み書きします。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

強力なメモリ アクセス API を次を参照してください。[メモリ アクセス](memory-access.md)で、[デバッガー エンジン API を使用して](using-the-debugger-engine-api.md)このドキュメントの「します。

 

 





