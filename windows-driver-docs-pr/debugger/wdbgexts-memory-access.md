---
title: WdbgExts メモリへのアクセス
description: WdbgExts メモリへのアクセス
ms.assetid: 7b600d18-343e-4c22-b1e9-5dcc83d88695
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c51b1297822e443bd1b93ae9f00f62a591194f20
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527678"
---
# <a name="wdbgexts-memory-access"></a>WdbgExts メモリへのアクセス


このトピックでは、メモリにアクセスする方法の概要は WdbgExts API を使用して実行できます。 メモリ アクセスの概要については、[デバッガー エンジン](introduction.md#debugger-engine)を参照してください[メモリ](memory.md)で、[デバッガー エンジンの概要](debugger-engine-overview.md)このドキュメントの「します。

### <a name="span-idvirtualmemoryspanspan-idvirtualmemoryspanvirtual-memory"></a><span id="virtual_memory"></span><span id="VIRTUAL_MEMORY"></span>仮想メモリ

使用して、ターゲットの仮想メモリを読み取ることができます、 [ **ReadMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff554287)関数とを使用して、 [ **WriteMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff561420)関数。 ターゲットのメモリ内のポインターを読み取りを使用して書き込むことができます、 [ **ReadPointer**](https://msdn.microsoft.com/library/windows/hardware/ff554318)、 [ **ReadPtr**](https://msdn.microsoft.com/library/windows/hardware/ff554330)、および[ **WritePointer** ](https://msdn.microsoft.com/library/windows/hardware/ff561450)関数。

仮想メモリのバイトのパターンを検索するには、使用、 [ **SearchMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff554742)関数。

[ **TranslateVirtualToPhysical** ](https://msdn.microsoft.com/library/windows/hardware/ff558914)仮想メモリ アドレスを物理メモリ アドレスに変換する関数を使用できます。

[ **Disasm** ](https://msdn.microsoft.com/library/windows/hardware/ff541945)ターゲット上の 1 つのアセンブリ命令を逆アセンブルする関数を使用できます。

物理アドレス拡張 (PAE) を使用する場合は、低の 4 GB のメモリの破損を確認するには、使用、 [ **Ioctl** ](https://msdn.microsoft.com/library/windows/hardware/ff551084)操作[ **IG\_LOWMEM\_確認**](https://msdn.microsoft.com/library/windows/hardware/ff550931)します。

### <a name="span-idphysicalmemoryspanspan-idphysicalmemoryspanphysical-memory"></a><span id="physical_memory"></span><span id="PHYSICAL_MEMORY"></span>物理メモリ

カーネル モードのデバッグで物理メモリに直接アクセスのみできます。

使用して、ターゲット上の物理メモリを読み取ることができます、 [ **ReadPhysical** ](https://msdn.microsoft.com/library/windows/hardware/ff554310)と[ **ReadPhysicalWithFlags** ](https://msdn.microsoft.com/library/windows/hardware/ff554315)関数、と書き込み使用して、 [ **WritePhysical** ](https://msdn.microsoft.com/library/windows/hardware/ff561432)と[ **WritePhysicalWithFlags** ](https://msdn.microsoft.com/library/windows/hardware/ff561448)関数。

指定した範囲内の場所へのポインターの物理メモリを検索するには、使用、 [ **Ioctl** ](https://msdn.microsoft.com/library/windows/hardware/ff551084)操作[ **IG\_ポインター\_検索\_物理**](https://msdn.microsoft.com/library/windows/hardware/ff550935)します。

### <a name="span-idotherdataspacesspanspan-idotherdataspacesspanother-data-spaces"></a><span id="other_data_spaces"></span><span id="OTHER_DATA_SPACES"></span>その他のデータ領域

カーネル モードのデバッグは、さまざまなメイン メモリだけでなくデータ領域にデータを読み書きすることです。 次のデータ領域にアクセスできます。

<span id="Control-Space_Memory"></span><span id="control-space_memory"></span><span id="CONTROL-SPACE_MEMORY"></span>コントロールの領域のメモリ  
関数は、 [ **ReadControlSpace**](https://msdn.microsoft.com/library/windows/hardware/ff553527)、 [ **ReadControlSpace64**](https://msdn.microsoft.com/library/windows/hardware/ff553532)、 [ **ReadTypedControlSpace32**](https://msdn.microsoft.com/library/windows/hardware/ff554339)、および[ **ReadTypedControlSpace64** ](https://msdn.microsoft.com/library/windows/hardware/ff554341)コントロール領域からデータを読み取ります。 [ **WriteControlSpace** ](https://msdn.microsoft.com/library/windows/hardware/ff561375)関数は、コントロールの領域にデータを書き込みます。

<span id="I_O_Memory"></span><span id="i_o_memory"></span><span id="I_O_MEMORY"></span>I/O メモリ  
関数は、 [ **ReadIoSpace**](https://msdn.microsoft.com/library/windows/hardware/ff553574)、 [ **ReadIoSpace64**](https://msdn.microsoft.com/library/windows/hardware/ff553577)、 **ReadIoSpace64**、 [**ReadIoSpaceEx64** ](https://msdn.microsoft.com/library/windows/hardware/ff553583)は、システム I/O メモリからデータを読み取り、I/O メモリ バスします。 関数は、 [ **WriteIoSpace**](https://msdn.microsoft.com/library/windows/hardware/ff561406)、 [ **WriteIoSpace64**](https://msdn.microsoft.com/library/windows/hardware/ff561408)、 [ **WriteIoSpaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff561413)、および[ **WriteIoSpaceEx64** ](https://msdn.microsoft.com/library/windows/hardware/ff561414)はシステム I/O メモリにデータを記述し、I/O メモリ バスします。

<span id="Model_Specific_Register__MSR_"></span><span id="model_specific_register__msr_"></span><span id="MODEL_SPECIFIC_REGISTER__MSR_"></span>モデル専用レジスタ (MSR)  
関数は、 [ **ReadMsr** ](https://msdn.microsoft.com/library/windows/hardware/ff554289)と[ **WriteMsr** ](https://msdn.microsoft.com/library/windows/hardware/ff561424) MSRs を読み書きします。

<span id="System_Bus"></span><span id="system_bus"></span><span id="SYSTEM_BUS"></span>システム バス  
[ **Ioctl** ](https://msdn.microsoft.com/library/windows/hardware/ff551084)操作[ **IG\_取得\_BUS\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff550913)と**IG\_設定\_BUS\_データ**システム バス データを読み書きします。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

強力なメモリ アクセス API を次を参照してください。[メモリ アクセス](memory-access.md)で、[デバッガー エンジン API を使用して](using-the-debugger-engine-api.md)このドキュメントの「します。

 

 





