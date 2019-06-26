---
title: スウィズル割り当てのロック
description: スウィズル割り当てのロック
ms.assetid: c9be52d9-36b2-4a0f-9629-01b31293af38
keywords:
- WDK の表示のロック スィズルの割り当て
- WDK 表示スィズル割り当てのロック
- によってアンスウィズル割り当て WDK を表示します。
- メモリのセグメントの WDK 表示、スィズル割り当てのロック
- 割り当てスィズル ロック WDK の表示
- 削除された割り当て WDK を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 114256e7cc9f1e6e79ca5b39e45967156f467dcf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360890"
---
# <a name="locking-swizzled-allocations"></a>スウィズル割り当てのロック


ビデオ メモリ マネージャー スィズル割り当てに直接アクセスする CPU の特別なサポートを提供します (を割り当て、ディスプレイのミニポート ドライバーの[ **DxgkDdiCreateAllocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)関数のセット**Swizzled**フラグ、**フラグ**のメンバー、 [ **DXGK\_ALLOCATIONINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)構造)。

ビデオ メモリ マネージャーは、メモリのセグメントからスィズルとしてドライバーによってマークされていない CPU アクセスの割り当てを削除、ときにディスプレイのミニポート ドライバー常に保存する必要あります線形の形式でします。 そのため、このような割り当てすることはできませんスィズル、aperture セグメント内にある、スィズルまたはドライバーのによって unswizzled が必ず[ **DxgkDdiBuildPagingBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)関数。

その一方で、スィズルとしてマークされている割り当てでは、常にメモリのセグメントから削除されるときに、線形形式で格納する必要はありません。 このような割り当てのビデオ メモリ マネージャーはそれらの割り当てのスウィズ リングの状態を追跡およびのみ、ドライバーの必要があります*DxgkDdiBuildPagingBuffer*転送の特定の操作中に割り当てをすべてに機能します。

ユーザー モードの表示後、ドライバーは、マイクロソフトの Direct3D ランタイムを呼び出して[ **pfnLockCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb)関数、ビデオ メモリ マネージャーおよびディスプレイのミニポート ドライバーの動作に応じて次の方法で、割り当ての状態:

1.  メモリのセグメントに割り当て

    ビデオ メモリ マネージャーは、割り当てに線形のアクセスを提供する CPU aperture の取得を試みます。 ビデオ メモリ マネージャーがシステム メモリに再度割り当てを削除する場合は、ビデオ メモリ マネージャーは、開口部を取得できません、(ドライバーを設定しない限り、 **DonotEvict**のメンバー、 [ **D3DDDICB\_LOCKFLAGS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddicb_lockflags)構造)。 ビデオ メモリ マネージャーが、表示ミニポート ドライバーを呼び出すときに[ **DxgkDdiBuildPagingBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)割り当てを転送する機能、ディスプレイのミニポート ドライバーすべて割り当てする必要があります。

2.  割り当ての削除 (スィズル)、aperture セグメントであるか

    割り当ては、CPU がアクセスする前に、によってアンスウィズルにすることがあります。 そのため、まず、ビデオ メモリ マネージャがページ メモリのセグメントに割り当てを試みます。 割り当てがメモリ セグメントにある後、ビデオ メモリ マネージャーとディスプレイのミニポート ドライバー番号 1 のように動作します。

3.  割り当ての削除 (によってアンスウィズル)

    割り当てがシステム メモリによってアンスウィズルで既に場合は、ビデオ メモリ マネージャーは、さらに処理することがなく既存の割り当てのポインターを返します。

    GPU されていたによってアンスウィズル割り当てを使用するためには、割り当てがあります reswizzled GPU がこれを使用する前にします。 そのため、サーフェスの障害でビデオ メモリ マネージャーとディスプレイのミニポート ドライバー動作は、次の方法で。

    -   メモリのセグメント (CPU の開口部によってその場でによってアンスウィズル) の割り当て

        割り当ては、GPU で処理できるスィズルの形式で既には。 そのため、さらに処理は必要ありません、ビデオ メモリ マネージャー。

    -   システム メモリ (によってアンスウィズル) に移動された割り当て

        割り当てのページでは、によってアンスウィズル データが含まれ、aperture セグメントにマップすることはできません。 そのため、割り当ては、メモリのセグメントをページングする必要があります。 ビデオ メモリ マネージャーが、表示ミニポート ドライバーを呼び出すときに[ **DxgkDdiBuildPagingBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)関数で割り当て、ビデオ メモリ マネージャー ページを要求する、ディスプレイのミニポート ドライバースィズル割り当てです。

**注**  スィズル割り当ては、CPU aperture を通じて CPU へのアクセスが、そのまま削除できるユーザー モードのディスプレイ ドライバーが、CPU へのアクセスを終了する前にします。 この場合は、番号 2 のように処理されます。 ユーザー モードのディスプレイ ドライバーとアプリケーションを表示できないような方法で、削除が実行されます。
No-overwrite ロックではまた、(設定してロックを取得、 **IgnoreSync**のメンバー [ **D3DDDICB\_LOCKFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddicb_lockflags))、スィズルでは使用できません割り当てです。 のみの CPU または GPU は、任意の時点で、このような割り当てにアクセスできます。

 

 

 





