---
title: 仮想メモリと物理メモリ
description: 仮想メモリと物理メモリ
ms.assetid: 346a46ea-9d44-4e12-8623-d118cd0c7e25
keywords:
- メモリアクセス、仮想メモリ、物理メモリ
- 仮想メモリアクセス
- 物理メモリアクセス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1abf5894b6a8e70c98a924f6f85332f14fa5efa9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838798"
---
# <a name="virtual-and-physical-memory"></a>仮想メモリと物理メモリ


## <span id="ddk_virtual_and_physical_memory_dbx"></span><span id="DDK_VIRTUAL_AND_PHYSICAL_MEMORY_DBX"></span>


エンジンには、ターゲットの仮想メモリと物理メモリの読み取りと書き込みを行うためのさまざまなメソッドが用意されています。

### <a name="span-idvirtual_memoryspanspan-idvirtual_memoryspanvirtual-memory"></a><span id="virtual_memory"></span><span id="VIRTUAL_MEMORY"></span>仮想メモリ

ターゲットの仮想メモリ内の場所を指定すると、ターゲットの仮想アドレス空間が使用されます。 ユーザーモードデバッグでは、これは現在のプロセスの仮想アドレス空間です。 カーネルモードのデバッグでは、これは暗黙的なプロセスの仮想アドレス空間です。 現在のプロセスと暗黙のプロセスの詳細については、「[スレッドとプロセス](controlling-threads-and-processes.md)」を参照してください。

仮想メモリ (ターゲット) は[**Readvirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readvirtual)を使用して読み取ることができ、 [**writevirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-writevirtual)を使用して書き込まれます。

ターゲットのメモリ内のポインターは、 [**ReadPointersVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readpointersvirtual)および[**WritePointersVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-writepointersvirtual)という便利なメソッドを使用して読み書きできます。 これらのメソッドは、エンジンによって使用される64ビットポインターとターゲットによって使用されるネイティブポインターとの間で自動的に変換されます。 これらのメソッドは、後続の要求に使用されるポインター (文字列へのポインターなど) を格納するメモリを要求するときに役立ちます。

[**Searchvirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-searchvirtual)メソッドと[**SearchVirtual2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-searchvirtual2)メソッドを使用して、ターゲットの仮想メモリでバイトのパターンを検索できます。

[**Fillvirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-fillvirtual)メソッドを使用すると、バイトのパターンをターゲットの仮想メモリに複数回コピーできます。

ターゲットの仮想メモリは、 [**Readvirtualuncached**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readvirtualuncached)メソッドと[**writevirtualuncached**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-writevirtualuncached)メソッドを使用してデバッガーエンジンの仮想メモリキャッシュをバイパスするように読み取りおよび書き込みを行うこともできます。 これらのキャッシュされていないバージョンは、メモリマップトデバイスなど、本質的に揮発性の仮想メモリを読み取る場合に便利です。キャッシュを汚染したり、無効にしたりする必要はありません。 キャッシュされていないアクセスのパフォーマンスはキャッシュされたアクセスより大幅に低くなる可能性があるため、キャッシュされていないメモリアクセスは、必要な場合にのみ使用してください。

エンジンには、ターゲットの仮想メモリから文字列を読み取るための便利なメソッドがいくつか用意されています。 ターゲットからマルチバイト文字列を読み取るには、 [**ReadMultiByteStringVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readmultibytestringvirtual)と[**ReadMultiByteStringVirtualWide**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readmultibytestringvirtualwide)を使用します。 ターゲットから Unicode 文字列を読み取るには、 [**ReadUnicodeStringVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readunicodestringvirtual)と[**ReadUnicodeStringVirtualWide**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readunicodestringvirtualwide)を使用します。

メモリ位置に関する情報を検索するには、 [**Getoffsetinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-getoffsetinformation)を使用します。 ターゲット内のすべての仮想アドレス空間に有効なメモリが含まれていません。 リージョン内の有効なメモリを見つけるには、 [**Getvalidregionvirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-getvalidregionvirtual)を使用します。 ターゲットで有効なメモリを手動で検索する場合、 [**GetNextDifferentlyValidOffsetVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-getnextdifferentlyvalidoffsetvirtual)メソッドは、有効期間が変更される次の場所を検索します。

### <a name="span-idphysical_memoryspanspan-idphysical_memoryspanphysical-memory"></a><span id="physical_memory"></span><span id="PHYSICAL_MEMORY"></span>物理メモリ

物理メモリには、カーネルモードのデバッグでのみ直接アクセスできます。

ターゲットの物理メモリは、 [**Readphysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readphysical)と[**ReadPhysical2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readphysical2)を使用して読み取ることができ、 [**writephysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writephysical)と[**WritePhysical2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-writephysical2)を使用して書き込まれます。

[**Fillphysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-fillphysical)メソッドを使用すると、バイトのパターンをターゲットの物理メモリに複数回コピーできます。

ターゲットの仮想アドレス空間内のアドレスは、 [**Virtualtophysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-virtualtophysical)メソッドを使用してターゲットの物理アドレスに変換できます。 物理アドレスへの仮想アドレスの変換に使用されるシステムのページング構造は、 [**GetVirtualTranslationPhysicalOffsets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-getvirtualtranslationphysicaloffsets)を使用して見つけることができます。

### <a name="span-ideventsspanspan-ideventsspanevents"></a><span id="events"></span><span id="EVENTS"></span>記録

ターゲットの仮想メモリまたは物理メモリが変更されると、 [**IDebugEventCallbacks:: ChangeDebuggeeState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugeventcallbacks-changedebuggeestate)コールバックメソッドが呼び出されます。

 

 





