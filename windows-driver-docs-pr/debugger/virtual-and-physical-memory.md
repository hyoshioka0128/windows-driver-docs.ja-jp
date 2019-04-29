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
ms.openlocfilehash: e134b53e280f31c671ae02adadd0b650d2d8dc40
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325909"
---
# <a name="virtual-and-physical-memory"></a>仮想メモリと物理メモリ


## <span id="ddk_virtual_and_physical_memory_dbx"></span><span id="DDK_VIRTUAL_AND_PHYSICAL_MEMORY_DBX"></span>


エンジンは、多数の読み取りとターゲットの仮想および物理メモリの書き込みメソッドを提供します。

### <a name="span-idvirtualmemoryspanspan-idvirtualmemoryspanvirtual-memory"></a><span id="virtual_memory"></span><span id="VIRTUAL_MEMORY"></span>仮想メモリ

ターゲットの仮想メモリの場所を指定する、ターゲットの仮想アドレス空間が使用されます。 ユーザー モードのデバッグは、これは、現在のプロセスの仮想アドレス空間です。 カーネル モードのデバッグは、これは、暗黙的なプロセスの仮想アドレス空間です。 参照してください[スレッドとプロセス](controlling-threads-and-processes.md)詳細については、現在と暗黙的なプロセスです。

使用して読み取ることができます (ターゲット) の仮想メモリ[ **ReadVirtual** ](https://msdn.microsoft.com/library/windows/hardware/ff554359)を使用して記述および[ **WriteVirtual**](https://msdn.microsoft.com/library/windows/hardware/ff561468)します。

ターゲットのメモリ内のポインターを読み取り、便利なメソッドを使用して記述できる[**されるため、** ](https://msdn.microsoft.com/library/windows/hardware/ff554323)と[ **WritePointersVirtual** ](https://msdn.microsoft.com/library/windows/hardware/ff561451). これらのメソッドは、エンジンによって使用される 64 ビット ポインターと、ターゲットによって使用されるネイティブ ポインターの間に自動的に変換されます。 これらのメソッドは、たとえば、文字列へのポインターに--の後続の要求の使用はポインターが格納されたメモリを要求するときに便利です。

[ **SearchVirtual** ](https://msdn.microsoft.com/library/windows/hardware/ff554747)と[ **SearchVirtual2** ](https://msdn.microsoft.com/library/windows/hardware/ff554755)メソッドは、ターゲットの仮想メモリのバイト パターンを検索するために使用できます。

[ **FillVirtual** ](https://msdn.microsoft.com/library/windows/hardware/ff545395)メソッドは、ターゲットの仮想メモリ (バイト単位) のパターンを複数回にコピーするために使用できます。

ターゲットの仮想メモリも読み取り、メソッドを使用して、デバッガー エンジンの仮想メモリ キャッシュをバイパスする方法で記述された[ **ReadVirtualUncached** ](https://msdn.microsoft.com/library/windows/hardware/ff554361)と[ **WriteVirtualUncached**](https://msdn.microsoft.com/library/windows/hardware/ff561473)します。 これらのキャッシュされていないバージョンは、デバイスのメモリ マップ領域など、本質的に揮発性に悪影響を及ぼしてまたはキャッシュを無効にせずは、仮想メモリの読み取りに役立ちます。 キャッシュされていないアクセスのパフォーマンスと、必要なときにアクセスの状況で使用する必要がありますはだけキャッシュされていないメモリをキャッシュされたアクセスを大幅に下回ることはできます。

エンジンは、ターゲットの仮想メモリから文字列を読み取るには、いくつか便利なメソッドを提供します。 ターゲットからマルチバイト文字列を読み取るには使用[ **ReadMultiByteStringVirtual** ](https://msdn.microsoft.com/library/windows/hardware/ff554300)と[ **ReadMultiByteStringVirtualWide**](https://msdn.microsoft.com/library/windows/hardware/ff554304)します。 ターゲットから Unicode 文字列を読み取るには使用[ **ReadUnicodeStringVirtual** ](https://msdn.microsoft.com/library/windows/hardware/ff554351)と[ **ReadUnicodeStringVirtualWide**](https://msdn.microsoft.com/library/windows/hardware/ff554357)します。

メモリの場所に関する情報を確認する[ **GetOffsetInformation**](https://msdn.microsoft.com/library/windows/hardware/ff548055)します。 すべてのターゲットの仮想アドレス空間には、有効なメモリが含まれています。 有効なメモリ領域内を検索する使用[ **GetValidRegionVirtual**](https://msdn.microsoft.com/library/windows/hardware/ff549471)します。 ターゲット、メソッドで有効なメモリを手動で検索するときに[ **GetNextDifferentlyValidOffsetVirtual** ](https://msdn.microsoft.com/library/windows/hardware/ff547847)有効性の変更可能性がありますが、次の場所を検索します。

### <a name="span-idphysicalmemoryspanspan-idphysicalmemoryspanphysical-memory"></a><span id="physical_memory"></span><span id="PHYSICAL_MEMORY"></span>物理メモリ

カーネル モードのデバッグで物理メモリに直接アクセスのみできます。

使用して、ターゲット上の物理メモリが読み取れる[ **ReadPhysical** ](https://msdn.microsoft.com/library/windows/hardware/ff554313)と[ **ReadPhysical2**](https://msdn.microsoft.com/library/windows/hardware/ff554311)を使用して記述および[**WritePhysical** ](https://msdn.microsoft.com/library/windows/hardware/ff561432)と[ **WritePhysical2**](https://msdn.microsoft.com/library/windows/hardware/ff561441)します。

[ **FillPhysical** ](https://msdn.microsoft.com/library/windows/hardware/ff545394)ターゲットの物理メモリ (バイト単位) のパターンを複数回にコピーするメソッドを使用できます。

ターゲットの仮想アドレス空間内のアドレスを使用して、ターゲットの物理アドレスに変換できる、 [ **VirtualToPhysical** ](https://msdn.microsoft.com/library/windows/hardware/ff560335)メソッド。 使用して、システムのページングの構造体を物理アドレスの仮想アドレスに変換するために使用を検出できる[ **GetVirtualTranslationPhysicalOffsets**](https://msdn.microsoft.com/library/windows/hardware/ff549498)します。

### <a name="span-ideventsspanspan-ideventsspanevents"></a><span id="events"></span><span id="EVENTS"></span>イベント

ターゲットの仮想または物理メモリが変更されたときに、 [ **IDebugEventCallbacks::ChangeDebuggeeState** ](https://msdn.microsoft.com/library/windows/hardware/ff550678)コールバック メソッドが呼び出されます。

 

 





