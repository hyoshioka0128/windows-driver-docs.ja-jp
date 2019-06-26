---
title: 非ローカルの表示メモリ サーフェスのコールバック処理
description: 非ローカルの表示メモリ サーフェスのコールバック処理
ms.assetid: 803c52df-93c4-4124-9e17-6ef6c734a15f
keywords:
- WDK DirectDraw、コールバックのメモリを表示します。
- WDK DirectDraw、コールバックの非ローカルの表示メモリ
- AGP WDK DirectDraw、コールバック
- 描画 AGP サポート WDK DirectDraw、コールバック
- DirectDraw AGP サポート WDK Windows 2000 の表示、コールバック
- WDK DirectDraw AGP、コールバックのメモリ
- コールバック WDK DirectDraw 非ローカル メモリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d297c3fad472cb5148c38dc4d982214854ee8776
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384611"
---
# <a name="callback-handling-of-nonlocal-display-memory-surfaces"></a>非ローカルの表示メモリ サーフェスのコールバック処理


## <span id="ddk_callback_handling_of_nonlocal_display_memory_surfaces_gg"></span><span id="DDK_CALLBACK_HANDLING_OF_NONLOCAL_DISPLAY_MEMORY_SURFACES_GG"></span>


ドライバーのコールバックの観点からローカルの表示メモリ サーフェスとまったく同じ方法では、非ローカルの表示メモリ サーフェスが扱われます。 たとえば、運転免許[ *DdCanCreateSurface* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549213(v=vs.85))しようとすると、非ローカル (だけでなくローカル) の表示メモリ サーフェスを作成するときに呼び出されるコールバック[ *DdBlt*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)時に呼び出されるローカルと非ローカルの間中メモリのサーフェスの表示と[ *DdDestroySurface* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface)表面のメモリが破棄されるときに呼び出されます。

同じドライバー関数は両方の表示のローカルと非ローカル メモリ サーフェスに使用されるため、ドライバーは着信サーフェスのメモリの種類を明示的にチェックする必要があります。 メモリの種類を確認して識別できます、 **ddsCaps.dwCaps**ローカルの表面のオブジェクトのメンバー [ **DD\_画面\_ローカル**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_local)渡されます機能に対してドライバーにビット DDSCAPS\_LOCALVIDMEM と DDSCAPS\_NONLOCALVIDMEM します。

アプリケーションと AGP ハードウェアは、2 つの異なるアドレスを使用して DirectDraw surface のビットにアクセスします。 アプリケーションでは、物理アドレス空間の部分に、オペレーティング システムのページ テーブルから翻訳されて仮想アドレスを使用します。 この物理アドレス空間は、連続して表示する GART ハードウェアによってマップされます。 ハードウェアでは、この物理のリニア アドレス (GART によって再マップ メモリの実際、不連続のページをもう一度) にアクセスします。 **FpVidMem**のメンバー、 [ **DD\_画面\_GLOBAL** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_global)構造体では、アプリケーションの仮想のリニア アドレスが保持 (および可能性のあるいくつかドライバー操作)。 デバイス側の物理アドレスからを確認できます。

```cpp
fpStartOffset = pSurface->fpHeapOffset - pSurface->lpVidMemHeap->fpStart;
```

このオフセットは、デバイスの GART の物理的なベース アドレスに追加されます (に含まれている、 **liPhysAGPBase**のメンバー、 [ **VMEMHEAP** ](https://docs.microsoft.com/windows/desktop/api/dmemmgr/ns-dmemmgr-_vmemheap)構造)。

その他のすべての点では、非ローカルの表示メモリ サーフェスは、ローカルの表示メモリ サーフェスとまったく同じように動作します。 ドライバーは、アプリケーションが非ローカルの表示メモリ サーフェスの画面のデータにアクセスしようとするときに、ロック要求を受信します。 非ローカルの間で転送などの操作はメモリを表示し、ローカルの表示メモリ サーフェス間可能性があると同様、ローカルの表示メモリが非同期にできます。 これらのサーフェスに関連する操作がまだ表示の非ローカル メモリ サーフェスをロックしようと保留中で DDERR ドライバーによって失敗する必要があります\_通常の方法で WASSTILLDRAWING エラー コード。

さらに、DirectDraw を管理、割り当てと解放非ローカルの表示、ドライバーに代わってメモリ サーフェスが、ドライバーがまだ作成と表示の非ローカル メモリ内のサーフェスの破棄の通知を受け取る。 非ローカル メモリ画面が破棄されるときに、画面は使用されなくなるまでもドライバーは返しません。

非表示のメモリが[失わ](losing-and-restoring-directdraw-surfaces.md)正確に同じ方法でローカルの表示メモリとして、つまり、モードの切り替えが発生した場合、または排他モードが変更されたときにすべてのローカルと非ローカルの表示メモリ サーフェスは失われますと[ *DdDestroySurface* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface)各 surface のドライバーのコールバックが呼び出されます。 ただし、DirectDraw では、実際の予約済みアドレス範囲とコミットされたメモリが保持されるは限りません。 コミットされたすべてのメモリと予約済みアドレスの範囲を破棄することもできます DirectDraw またはデコミット メモリは、アドレスの範囲を保持することもできます。 両方を保持する、単に紛失したとサーフェスをマークし、可能性があります。 ドライバーは、これらのシナリオのいずれかの仮定しないようにします。

 

 





