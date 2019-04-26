---
title: 実際のヒープ ベース アドレスの通知
description: 実際のヒープ ベース アドレスの通知
ms.assetid: b2fe29c7-7c97-41c2-a6be-2c0ef25c5b58
keywords:
- ヒープ WDK DirectDraw
- ヒープ メモリ WDK の DirectDraw を表示します。
- WDK DirectDraw、ヒープの非ローカルの表示メモリ
- AGP WDK DirectDraw、ヒープ
- ヒープ AGP サポート WDK DirectDraw を描画するには、
- DirectDraw AGP サポート WDK Windows 2000 の表示、ヒープ
- WDK DirectDraw AGP、ヒープ メモリ
- 通知の WDK DirectDraw ヒープ アドレス
- 線形ヒープ WDK DirectDraw
- 物理的なヒープ WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff0afa25a9bbf81866bebb263b8066eb1bfa19d5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345520"
---
# <a name="notification-of-actual-heap-base-addresses"></a>実際のヒープ ベース アドレスの通知


## <span id="ddk_notification_of_actual_heap_base_addresses_gg"></span><span id="DDK_NOTIFICATION_OF_ACTUAL_HEAP_BASE_ADDRESSES_GG"></span>


ドライバーは、サーフェスの作成要求を待つと、グローバル DirectDraw surface オブジェクトでヒープを調べるのではなく (たとえば中モードの変更) DirectDraw 初期化時に、ヒープのベースの線形と物理アドレスを知っている必要があります。 この、DirectDraw 呼び出しをサポートするドライバーによって提供される[ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)ドライバーによって返される情報を識別するグローバル一意識別子 (GUID) でコールバック関数。 場合は、ドライバーは、GUID が認識され、返される情報は、この情報を提供されたデータ構造にコピーし、DirectDraw に戻してします。

ドライバーでは、2 つの Guid を使用を収集してヒープ関連の直接描画の詳細を提供します。

-   GUID\_GetHeapAlignment

-   GUID\_UpdateNonLocalHeap

GUID\_GetHeapAlignment 信号をヒープの配置について、DirectDraw ヒープを収集するために、ドライバーに渡されます。 ヒープ情報がドライバーを使用して、渡される、 [ **DD\_GETHEAPALIGNMENTDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551572)構造体。 GUID\_GetHeapAlignment として定義されます。

```cpp
DEFINE_GUID( GUID_GetHeapAlignment,
    0x42e02f16, 0x7b41, 0x11d2, 0x8b, 0xff, 0x0, 0xa0, 0xc9, 0x83, 0xea, 0xf6);
```

GUID\_UpdateNonLocalHeap DirectDraw によって提供される非ローカル ヒープ構造体を持つ、ヒープ情報ありの内部状態を更新するドライバーに通知します。 この情報は、 [ **DD\_UPDATENONLOCALHEAPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551748)構造体。 GUID\_UpdateNonLocalHeap として定義されます。

```cpp
DEFINE_GUID( GUID_UpdateNonLocalHeap,
           0x42e02f17, 0x7b41, 0x11d2, 0x8b, 0xff, 0x0, 0xa0, 0xc9, 0x83, 0xea, 0xf6);
```

場合は、ドライバーは AGP 自体は、明らかになりますが、DirectDraw にヒープを公開するがメモリを割り当てる必要があります[ **HeapVidMemAllocAligned** ](https://msdn.microsoft.com/library/windows/hardware/ff567267)として公開される、**への Eng**関数この目的。 **HeapVidMemAllocAligned**のみヒープ アドレス扱うためのオフセットが返されます。 返される情報を有効にするために必要なすべてのメモリ マッピングの機能、ドライバーが行う必要があります**HeapVidMemAllocAligned**仮想アドレスに変換します。

 

 





