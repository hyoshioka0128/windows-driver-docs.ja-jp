---
title: 仮想メモリと物理メモリ
description: 仮想メモリと物理メモリ
ms.assetid: 346a46ea-9d44-4e12-8623-d118cd0c7e25
keywords:
- メモリ アクセス、仮想および物理メモリ
- 仮想メモリへのアクセス
- 物理メモリへのアクセス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4488b599f1a4fcf9c7019efd5c2aa5cbe0100617
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369428"
---
# <a name="virtual-and-physical-memory"></a>仮想メモリと物理メモリ


## <span id="ddk_virtual_and_physical_memory_dbx"></span><span id="DDK_VIRTUAL_AND_PHYSICAL_MEMORY_DBX"></span>


エンジンは、多数の読み取りとターゲットの仮想および物理メモリの書き込みメソッドを提供します。

### <a name="span-idvirtualmemoryspanspan-idvirtualmemoryspanvirtual-memory"></a><span id="virtual_memory"></span><span id="VIRTUAL_MEMORY"></span>仮想メモリ

ターゲットの仮想メモリの場所を指定する、ターゲットの仮想アドレス空間が使用されます。 ユーザー モードのデバッグは、これは、現在のプロセスの仮想アドレス空間です。 カーネル モードのデバッグは、これは、暗黙的なプロセスの仮想アドレス空間です。 参照してください[スレッドとプロセス](controlling-threads-and-processes.md)詳細については、現在と暗黙的なプロセスです。

使用して読み取ることができます (ターゲット) の仮想メモリ[ **ReadVirtual** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-readvirtual)を使用して記述および[ **WriteVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-writevirtual)します。

ターゲットのメモリ内のポインターを読み取り、便利なメソッドを使用して記述できる[**されるため、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-readpointersvirtual)と[ **WritePointersVirtual** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-writepointersvirtual). これらのメソッドは、エンジンによって使用される 64 ビット ポインターと、ターゲットによって使用されるネイティブ ポインターの間に自動的に変換されます。 これらのメソッドは、たとえば、文字列へのポインターに--の後続の要求の使用はポインターが格納されたメモリを要求するときに便利です。

[ **SearchVirtual** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-searchvirtual)と[ **SearchVirtual2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-searchvirtual2)メソッドは、ターゲットの仮想メモリのバイト パターンを検索するために使用できます。

[ **FillVirtual** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-fillvirtual)メソッドは、ターゲットの仮想メモリ (バイト単位) のパターンを複数回にコピーするために使用できます。

ターゲットの仮想メモリも読み取り、メソッドを使用して、デバッガー エンジンの仮想メモリ キャッシュをバイパスする方法で記述された[ **ReadVirtualUncached** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-readvirtualuncached)と[ **WriteVirtualUncached**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-writevirtualuncached)します。 これらのキャッシュされていないバージョンは、デバイスのメモリ マップ領域など、本質的に揮発性に悪影響を及ぼしてまたはキャッシュを無効にせずは、仮想メモリの読み取りに役立ちます。 キャッシュされていないアクセスのパフォーマンスと、必要なときにアクセスの状況で使用する必要がありますはだけキャッシュされていないメモリをキャッシュされたアクセスを大幅に下回ることはできます。

エンジンは、ターゲットの仮想メモリから文字列を読み取るには、いくつか便利なメソッドを提供します。 ターゲットからマルチバイト文字列を読み取るには使用[ **ReadMultiByteStringVirtual** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-readmultibytestringvirtual)と[ **ReadMultiByteStringVirtualWide**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-readmultibytestringvirtualwide)します。 ターゲットから Unicode 文字列を読み取るには使用[ **ReadUnicodeStringVirtual** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-readunicodestringvirtual)と[ **ReadUnicodeStringVirtualWide**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-readunicodestringvirtualwide)します。

メモリの場所に関する情報を確認する[ **GetOffsetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-getoffsetinformation)します。 すべてのターゲットの仮想アドレス空間には、有効なメモリが含まれています。 有効なメモリ領域内を検索する使用[ **GetValidRegionVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-getvalidregionvirtual)します。 ターゲット、メソッドで有効なメモリを手動で検索するときに[ **GetNextDifferentlyValidOffsetVirtual** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-getnextdifferentlyvalidoffsetvirtual)有効性の変更可能性がありますが、次の場所を検索します。

### <a name="span-idphysicalmemoryspanspan-idphysicalmemoryspanphysical-memory"></a><span id="physical_memory"></span><span id="PHYSICAL_MEMORY"></span>物理メモリ

カーネル モードのデバッグで物理メモリに直接アクセスのみできます。

使用して、ターゲット上の物理メモリが読み取れる[ **ReadPhysical** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-readphysical)と[ **ReadPhysical2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-readphysical2)を使用して記述および[**WritePhysical** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-writephysical)と[ **WritePhysical2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-writephysical2)します。

[ **FillPhysical** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-fillphysical)ターゲットの物理メモリ (バイト単位) のパターンを複数回にコピーするメソッドを使用できます。

ターゲットの仮想アドレス空間内のアドレスを使用して、ターゲットの物理アドレスに変換できる、 [ **VirtualToPhysical** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-virtualtophysical)メソッド。 使用して、システムのページングの構造体を物理アドレスの仮想アドレスに変換するために使用を検出できる[ **GetVirtualTranslationPhysicalOffsets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-getvirtualtranslationphysicaloffsets)します。

### <a name="span-ideventsspanspan-ideventsspanevents"></a><span id="events"></span><span id="EVENTS"></span>イベント

ターゲットの仮想または物理メモリが変更されたときに、 [ **IDebugEventCallbacks::ChangeDebuggeeState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugeventcallbacks-changedebuggeestate)コールバック メソッドが呼び出されます。

 

 





