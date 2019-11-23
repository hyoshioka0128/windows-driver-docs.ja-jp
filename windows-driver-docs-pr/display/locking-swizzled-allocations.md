---
title: スウィズル割り当てのロック
description: スウィズル割り当てのロック
ms.assetid: c9be52d9-36b2-4a0f-9629-01b31293af38
keywords:
- スィズル割り当てロックの WDK ディスプレイ
- スィズル割り当てのロックの WDK ディスプレイ
- 未スィズル割り当て WDK 表示
- メモリセグメント WDK 表示、スィズル割り当てのロック
- allocation swizzle locks の WDK 表示
- 削除した割り当ての WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0089975bb28eead2e58131df202db298a093f654
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840598"
---
# <a name="locking-swizzled-allocations"></a>スウィズル割り当てのロック


ビデオメモリマネージャーでは、スィズルされた割り当てへの直接 CPU アクセス (つまり、ディスプレイミニポートドライバーの[**DxgkDdiCreateAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)関数によって、 [ **\_DXGK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)の**Flags**メンバーにある**スィズル**フラグが設定される割り当て) に対して特別なサポートを提供します。

ビデオメモリマネージャーが、ドライバーによってマークされていない CPU アクセス可能な割り当てをメモリセグメントから見つけした場合、ディスプレイミニポートドライバーは、常にそれらを線形形式で格納する必要があります。 そのため、このような割り当ては、アパーチャセグメントに配置されている間はスィズルできません。また、ドライバーの[**DxgkDdiBuildPagingBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)関数によって常にスィズルまたはスィズル解除される必要があります。

一方、スィズルとしてマークされている割り当ては、メモリセグメントから削除されるときに常に線形形式で格納される必要はありません。 このような割り当ての場合、ビデオメモリマネージャーはこれらの割り当てのスウィズリング状態を追跡し、特定の転送操作中に割り当てを unswizzle するにはドライバーの*DxgkDdiBuildPagingBuffer*関数のみを必要とします。

ユーザーモードディスプレイドライバーが Microsoft Direct3D ランタイムの[**Pfnlockcb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb)関数を呼び出すと、ビデオメモリマネージャーとディスプレイミニポートドライバーは、割り当ての状態に応じて次のように動作します。

1.  メモリセグメントに配置されている割り当て

    ビデオメモリマネージャーは、割り当てに対する直線的なアクセスを提供するために CPU のアパーチャを獲得しようとします。 ビデオメモリマネージャーが絞りを取得できない場合、ビデオメモリマネージャーは、 [**D3DDDICB\_LOCKFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddicb_lockflags)構造体のに**見つけメンバーを設定しない**限り、割り当てをシステムメモリに戻します。 ビデオメモリマネージャーがディスプレイミニポートドライバーの[**DxgkDdiBuildPagingBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)関数を呼び出して割り当てを転送すると、ディスプレイミニポートドライバーによって割り当てが unswizzle されます。

2.  割り当てが削除された (スィズルされている) か、またはアパーチャセグメントに配置されている

    CPU がアクセスできるようにするには、割り当てを解除する必要があります。 そのため、ビデオメモリマネージャーは、最初にメモリセグメントへの割り当てのページを試行します。 割り当てがメモリセグメントに配置されると、ビデオメモリマネージャーと表示ミニポートドライバーは、番号1と同じように動作します。

3.  割り当てを削除した (非スィズル)

    割り当てが既にシステムメモリに割り当てられていない場合、ビデオメモリマネージャーは、それ以上の処理を行わずに既存の割り当てポインターを返します。

    GPU で以前にスィズルされていなかった割り当てを使用するには、GPU がそれを使用する前に割り当てを reswizzled する必要があります。 そのため、surface エラーの場合、ビデオメモリマネージャーとディスプレイミニポートドライバーは、次のように動作します。

    -   メモリセグメント内の割り当て (CPU アパーチャによってすぐに非スィズル)

        この割り当ては、GPU が処理できるスィズルされた形式になっています。 そのため、ビデオメモリマネージャーではそれ以上の処理は必要ありません。

    -   割り当てがシステムメモリ (非スィズル) に対して削除された

        割り当てのページには、スィズルされていないデータが含まれているため、アパーチャセグメントにマップできません。 そのため、割り当てはメモリセグメント内でページングされている必要があります。 ビデオメモリマネージャーがディスプレイミニポートドライバーの[**DxgkDdiBuildPagingBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)関数を呼び出して割り当てのページを表示すると、ビデオメモリマネージャーは、ディスプレイミニポートドライバーが割り当てを swizzle するように要求します。

**  、** cpu アパーチャを介してスィズル割り当てが cpu アクセスを使用している場合は、ユーザーモードのディスプレイドライバーが cpu アクセスを終了する前に削除することができます。 このケースは、数値2のように処理されます。 削除は、アプリケーションおよびユーザーモードの表示ドライバーで非表示になるように実行されます。
また、非上書きロック ( [**D3DDDICB\_LOCKFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddicb_lockflags)の**IgnoreSync**メンバーの設定によって取得されたロック) は、スィズル割り当てでは許可されません。 特定の時点で、CPU または GPU だけがこのような割り当てにアクセスできます。

 

 

 





