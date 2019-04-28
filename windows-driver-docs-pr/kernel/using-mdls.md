---
title: MDL の使用
description: MDL の使用
ms.assetid: 60652eb8-cfdb-4591-88ff-cf9dc4b9743d
keywords:
- メモリ管理の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e9f8a0e9a8acd2d3d9972f060ebea95c405c48c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364905"
---
# <a name="using-mdls"></a>MDL の使用


連続した仮想メモリ アドレスの範囲にわたる I/O バッファーをいくつかの物理ページに分散させることができ、これらのページを連続していないことができます。 オペレーティング システムの使用、*メモリ記述子のリスト*仮想メモリ バッファーの物理的なページ レイアウトを記述するには、(MDL)。

MDL から成る、 [ **MDL** ](https://msdn.microsoft.com/library/windows/hardware/ff554414) I/O バッファーが存在する物理メモリを説明するデータの配列が続く構造体。 MDL のサイズは、MDL 説明する I/O バッファーの特性によって異なります。 システムのルーチン、MDL の必要なサイズの計算と割り当てし、解放 MDL を利用できます。

MDL 構造体は、不透明度の低いです。 ドライバーにのみ直接アクセスする必要があります、**次**と**MdlFlags**この構造体のメンバー。 これら 2 つのメンバーを使用するコード例では、次の例のセクションを参照してください。

MDL の残りのメンバーは、不透明です。 不透明な MDL のメンバーに直接アクセスしない操作を行います。 代わりに、構造体に基本的な操作を実行するオペレーティング システムを提供する次のマクロを使用します。

[**MmGetMdlVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554539) MDL によって記述される I/O バッファーの仮想メモリ アドレスを返します。

[**MmGetMdlByteCount** ](https://msdn.microsoft.com/library/windows/hardware/ff554530)サイズ、I/O バッファーのバイト単位で返します。

[**MmGetMdlByteOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff554533) I/O バッファーの先頭の物理的なページ内のオフセットを返します。

MDL を割り当てることができます、 [ **IoAllocateMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff548263)ルーチン。 MDL を解放するには、使用、 [ **IoFreeMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff549126)ルーチン。 または、非ページ メモリのブロックを割り当てます、MDL としてメモリのブロックを書式設定し、呼び出すことによって、 [ **MmInitializeMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff554568)ルーチン。

どちらも**IoAllocateMdl**も**MmInitializeMdl** MDL 構造体の直後にデータの配列を初期化します。 非ページ メモリのドライバーに割り当てられたブロック内にある MDL、使用[ **MmBuildMdlForNonPagedPool** ](https://msdn.microsoft.com/library/windows/hardware/ff554498) I/O バッファーが存在する物理メモリを記述するには、この配列を初期化します。

ページング可能なメモリは、仮想および物理メモリ間の通信は一時的なもので MDL 構造体に続くデータ配列は特定の状況下でのみ有効です。 呼び出す[ **MmProbeAndLockPages** ](https://msdn.microsoft.com/library/windows/hardware/ff554664)をページング可能なメモリを固定して、現在のレイアウトの場合は、このデータ配列を初期化します。 呼び出し元が使用されるまで、メモリをページングされないが、 [ **MmUnlockPages** ](https://msdn.microsoft.com/library/windows/hardware/ff556381)ルーチンは、この時点でデータの配列の内容は無効になります。

[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559)ルーチン システム アドレスにマップされていない場合、システム アドレス空間内の仮想アドレスに指定された MDL によって記述される物理的なページがマップされます領域。 この仮想のアドレスは、ドライバー、元の仮想アドレスには、元のコンテキストでのみ使用できますし、いつでも削除できるユーザーのアドレスが可能性があるため、I/O を実行するページを確認する必要がある場合に便利です。

部分的な MDL を使用してビルドすると、 [ **IoBuildPartialMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff548324) 、呼び出し元を使用する必要があります、日常的な**MmGetMdlVirtualAddress**の代わりに、 **MmGetSystemAddressForMdlSafe**ルーチンに渡す仮想アドレスを決定するときにします。 **IoBuildPartialMdl**アドレスを使用している**MmGetMdlVirtualAddress**ターゲット MDL のオフセットを決定する MDL ソースから取得します。 アドレスが (たとえば、最初のアドレスがユーザーのアドレスである場合)、異なる場合は、アドレスを渡す**MmGetSystemAddressForMdlSafe**を返します。 データの破損またはバグ チェックが発生することができます。

ドライバーを呼び出すと**IoAllocateMdl**に関連付けることができます、IRP 新しく割り当てられた MDL IRP をへのポインターを指定することで、 *Irp*パラメーターの**IoAllocateMdl**します。 IRP が 1 つまたは複数 MDLs 関連付けられています。 IRP が関連付けられている、IRP の 1 つ MDL **MdlAddress**その MDL へのポインターします。 IRP がそれに関連付けられている複数の MDLs **MdlAddress**と呼ばれる、IRP に関連付けられている MDLs のリンク リストの最初の MDL を指す、 *MDL チェーン*します。 によって、MDLs がリンクされている、**次**メンバー。 **次**チェーン内の最後の MDL のメンバーに設定されている**NULL**します。

ドライバーを呼び出すと場合、 **IoAllocateMdl**を指定します**FALSE**の*SecondaryBuffer*パラメーター、IRP の**MdlAddress**新しい MDL を指すメンバーが設定されます。 場合*SecondaryBuffer*は**TRUE**ルーチンが MDL チェーンの末尾に新しい MDL を挿入します。

IRP が完了したら、システムがロックを解除し、IRP に関連付けられているすべての MDLs を解放します。 システムは、I/O 完了ルーチンから I/O 完了ルーチンの実行後に、解放する前に、MDLs をロック解除します。

ドライバーを使用して MDL チェーンをスキャンすることができます、**次**チェーンで次の MDL にアクセスするには、各 MDL のメンバー。 ドライバーは更新することによって、チェーンに MDLs を手動で挿入できます、**次**メンバー。

MDL チェーンは、1 つの I/O 要求に関連付けられているバッファーの配列を管理する通常使用されます。 (たとえば、ネットワーク ドライバーでしたを使用して、1 つのバッファー ネットワーク操作では、各 IP パケットの。)配列内の各バッファーは、チェーンに、独自の MDL を持っています。 ドライバーには、要求が完了するは、1 つの大きなバッファーにバッファーを結合します。 システムから自動的にクリーンアップ要求に割り当てられているすべての MDLs。

[I/O マネージャー](windows-kernel-mode-i-o-manager.md)は I/O 要求の頻繁なソースです。 I/O マネージャーには、I/O 要求が完了すると、I/O マネージャーは IRP を解放し、IRP にアタッチされている任意の MDLs を解放します。 これら MDLs のいくつかの可能性がありますがアタッチされている IRP デバイス スタックの I/O マネージャー下に配置されたドライバー。 同様に、ドライバーが、I/O 要求のソースの場合は、ドライバーする必要があります IRP とクリーンアップ I/O 要求が完了したときに、IRP にアタッチされている任意の MDLs します。

### <a name="example"></a>例

次のコード例では、IRP から、MDL チェーンを解放するドライバー実装関数を示します。

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

チェーンの MDL によって記述される物理的なページがロックされている場合、例関数は、 [ **MmUnlockPages** ](https://msdn.microsoft.com/library/windows/hardware/ff556381)ルーチンを呼び出す前に、ページのロックを解除する[ **IoFreeMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff549126) MDL を解放します。 ただし、例の関数は、ページを呼び出す前に明示的にマップ解除する必要はありません**IoFreeMdl**します。 代わりに、 **IoFreeMdl**自動的に MDL を解放する場合、ページの割り当てを解除します。

割り当て、解放、および MDLs を管理するシステム ルーチンの概要については、次を参照してください。[アドレス マッピングと MDLs](https://msdn.microsoft.com/library/windows/hardware/ff540568)します。

 

 




