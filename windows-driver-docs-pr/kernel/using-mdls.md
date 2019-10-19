---
title: MDL の使用
description: MDL の使用
ms.assetid: 60652eb8-cfdb-4591-88ff-cf9dc4b9743d
keywords:
- メモリ管理 (WDK) カーネル、
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d948aad219df86fde7f8720c6d4f2ea3a7fa196f
ms.sourcegitcommit: 87975bf11f43410ae113b57a34131778fb9677a0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2019
ms.locfileid: "72549719"
---
# <a name="using-mdls"></a>MDL の使用


連続した仮想メモリアドレスの範囲にまたがる i/o バッファーは、複数の物理ページに分散できます。また、これらのページは連続していてもかまいません。 オペレーティングシステムでは、*メモリ記述子リスト*(MDL) を使用して、仮想メモリバッファーの物理的なページレイアウトを記述します。

MDL は、その後に i/o バッファーが存在する物理メモリを示すデータの配列を続けた[**mdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_mdl)構造体で構成されます。 MDL のサイズは、MDL が記述する i/o バッファーの特性によって異なります。 システムルーチンを使用して、必要な MDL のサイズを計算し、MDL を割り当てたり解放したりすることができます。

MDL 構造体は、半不透明です。 ドライバーは、この構造体の**Next**および**mdlflags**メンバーにのみ直接アクセスする必要があります。 これらの2つのメンバーを使用するコード例については、次の「例」のセクションを参照してください。

MDL の残りのメンバーは不透明です。 MDL の非透過的メンバーに直接アクセスしないでください。 代わりに、次のマクロを使用します。これは、オペレーティングシステムによって構造に対する基本的な操作を実行するために用意されています。

[**Mmgetmdlvirtualaddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)は、MDL によって記述される i/o バッファーの仮想メモリアドレスを返します。

[**MmGetMdlByteCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmgetmdlbytecount)は、i/o バッファーのサイズ (バイト単位) を返します。

[**Mmgetmdlbyteoffset**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)は、i/o バッファーの先頭にある物理ページ内のオフセットを返します。

[**IoAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocatemdl)ルーチンを使用して、MDL を割り当てることができます。 MDL を解放するには、 [**Iofreemdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreemdl)ルーチンを使用します。 または、非ページメモリのブロックを割り当て、 [**MmInitializeMdl**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)ルーチンを呼び出して、このメモリブロックを MDL としてフォーマットすることもできます。

**IoAllocateMdl**も**MmInitializeMdl**でも、MDL 構造体の直後にあるデータ配列は初期化されません。 ドライバーで割り当てられた非ページメモリのブロックにある MDL の場合は、 [**MmBuildMdlForNonPagedPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmbuildmdlfornonpagedpool)を使用してこの配列を初期化し、i/o バッファーが存在する物理メモリを記述します。

ページング可能なメモリの場合、仮想メモリと物理メモリの対応は一時的なものであるため、MDL 構造に従うデータ配列は、特定の状況でのみ有効です。 [**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)を呼び出して、ページング可能なメモリを所定の場所にロックし、このデータ配列を現在のレイアウト用に初期化します。 呼び出し元が[**MmUnlockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunlockpages)ルーチンを使用するまで、メモリはページアウトされません。その時点で、データ配列の内容は無効になります。

[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)ルーチンは、指定された MDL によって記述される物理ページがシステムアドレス空間にまだマップされていない場合、システムアドレス空間内の仮想アドレスにマップします。 この仮想アドレスは、i/o を実行するためにページを確認する必要があるドライバーに役立ちます。元の仮想アドレスは、元のコンテキストでのみ使用でき、いつでも削除できるユーザーアドレスである可能性があるためです。

[**Iobuildpartialmdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildpartialmdl)ルーチンを使用して部分的な mdl を構築する場合、渡す仮想アドレスを決定するときに、呼び出し元は**MmGetSystemAddressForMdlSafe**ルーチンの代わりに**Mmgetmdlvirtualaddress**を使用する必要があることに注意してください。 **Iobuildpartialmdl**は、ソースの Mdl から**Mmgetmdlvirtualaddress**が返すアドレスを使用して、ターゲットの mdl のオフセットを決定します。 アドレスが異なる場合 (たとえば、最初のアドレスがユーザーアドレスの場合)、 **MmGetSystemAddressForMdlSafe**から返されるアドレスを渡すと、データの破損またはバグチェックが発生する可能性があります。

ドライバーが**IoAllocateMdl**を呼び出すと、 **IoAllocateMdl**の*IRP*パラメーターとして irp へのポインターを指定することで、irp を新しく割り当てられた MDL に関連付けることができます。 IRP には、1つ以上の MDLs を関連付けることができます。 IRP に1つの MDL が関連付けられている場合、IRP の**Mdladdress**メンバーはその mdl を指します。 IRP に複数の MDLs が関連付けられている場合、 **Mdladdress**は、( *mdl チェーン*と呼ばれる) irp に関連付けられている mdls のリンクリスト内の最初の MDL を指します。 MDLs は、**次**のメンバーによってリンクされています。 チェーン内の最後の MDL の**次**のメンバーが**NULL**に設定されています。

ドライバーが**IoAllocateMdl**を呼び出したときに、 *Secondarybuffer*パラメーターに**FALSE**を指定した場合、IRP の**mdladdress**メンバーは新しい MDL を指すように設定されます。 *Secondarybuffer*が**TRUE**の場合、このルーチンは新しい mdl を mdl チェーンの最後に挿入します。

IRP が完了すると、システムは、IRP に関連付けられているすべての MDLs をロック解除し、解放します。 I/o 完了ルーチンをキューに置いて、i/o 完了ルーチンの実行後に解放する前に、MDLs のロックが解除されます。

ドライバーは、各 MDL の**次**のメンバーを使用して、チェーン内の次の mdl にアクセスすることによって、mdl チェーンを走査できます。 ドライバーは、**次**のメンバーを更新することで、手動で mdls をチェーンに挿入できます。

通常、MDL チェーンは、単一の i/o 要求に関連付けられたバッファーの配列を管理するために使用されます。 (たとえば、ネットワークドライバーでは、ネットワーク操作で IP パケットごとに1つのバッファーを使用できます)。配列内の各バッファーには、チェーン内に独自の MDL があります。 ドライバーは、要求を完了すると、バッファーを1つの大きなバッファーに結合します。 システムは、要求に割り当てられたすべての MDLs を自動的にクリーンアップします。

I/o[マネージャー](windows-kernel-mode-i-o-manager.md)は、頻繁に i/o 要求を送信します。 I/o マネージャーが i/o 要求を完了すると、i/o マネージャーによって IRP が解放され、IRP にアタッチされている MDLs が解放されます。 これらの MDLs の一部は、デバイススタックの i/o マネージャーの下にあるドライバーによって IRP にアタッチされている可能性があります。 同様に、ドライバーが i/o 要求のソースである場合は、i/o 要求の完了時に irp にアタッチされている IRP と MDLs をドライバーがクリーンアップする必要があります。

### <a name="example"></a>例

次のコード例は、IRP から MDL チェーンを解放するドライバーによって実装される関数です。

```cpp
VOID MyFreeMdl(PMDL Mdl)
{
    PMDL currentMdl, nextMdl;

    for (currentMdl = Mdl; currentMdl != NULL; currentMdl = nextMdl) 
    {
        nextMdl = currentMdl->Next;
        if (currentMdl->MdlFlags & MDL_PAGES_LOCKED) 
        {
            MmUnlockPages(currentMdl);
        }
        IoFreeMdl(currentMdl);
    }
} 
```

チェーン内の MDL によって記述された物理ページがロックされている場合、この例の関数は、 [**Iofreemdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreemdl)を呼び出して mdl を解放する前に、 [**MmUnlockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunlockpages)ルーチンを呼び出してページのロックを解除します。 ただし、この例の関数では、 **Iofreemdl**を呼び出す前にページを明示的にマップ解除する必要はありません。 代わりに、 **Iofreemdl**は、MDL を解放するときにページを自動的に解除します。


