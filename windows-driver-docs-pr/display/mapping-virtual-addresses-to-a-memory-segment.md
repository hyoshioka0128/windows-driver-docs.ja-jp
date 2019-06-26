---
title: メモリ セグメントへの仮想アドレスのマッピング
description: メモリ セグメントへの仮想アドレスのマッピング
ms.assetid: 3ff64e33-eceb-4603-a3d9-11cb2f7dac85
keywords:
- メモリのセグメントの WDK 表示、仮想アドレスのマッピング
- 仮想アドレスのマッピング
- 仮想アドレスのマッピングの WDK の表示
- CPU 仮想アドレスのマッピングの WDK の表示
- 線形 aperture 領域セグメント WDK の表示
- aperture 空間セグメントの WDK の表示
- 線形のメモリ領域のセグメントの WDK の表示
- メモリ空間のセグメントの WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f06316df0f57bff1757a7542d981aa07e4b067a8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370118"
---
# <a name="mapping-virtual-addresses-to-a-memory-segment"></a>メモリ セグメントへの仮想アドレスのマッピング


## <span id="ddk_mapping_virtual_addresses_to_a_memory_segment_gg"></span><span id="DDK_MAPPING_VIRTUAL_ADDRESSES_TO_A_MEMORY_SEGMENT_GG"></span>


ディスプレイのミニポート ドライバーを指定できます、メモリ スペースまたは aperture スペース、各セグメントの定義する CPU 仮想アドレスを割り当てに直接マップできるかどうかセグメントに存在を設定して、 **CpuVisible**ビット フィールドフラグ、**フラグ**のメンバー、 [ **DXGK\_SEGMENTDESCRIPTOR** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)セグメントの構造体。

CPU の仮想アドレス セグメントに割り当てると、セグメントの PCI aperture で線形のアクセスが必要です。 つまり、すべての割り当てが、セグメント内のオフセットでは、PCI aperture 内のオフセットと同じである必要があります。 そのため、ビデオ メモリ マネージャーは、特定のセグメント内の割り当てのオフセットに基づくすべての割り当てのバスの相対物理アドレスを計算できます。

次の図は、仮想アドレス セグメントを線形のメモリ領域にマップされます。

![線形のメモリ領域のセグメントにマップされている仮想アドレスを示す図](images/vrtlmap.png)

次の図は、仮想アドレス線形 aperture 領域セグメントの基になるページにマップされます。

![線形 aperture 領域セグメントの基になるページにマップされている仮想アドレスを示す図](images/vrtlmap2.png)

仮想アドレス セグメントの部分にマップする前にビデオ メモリ マネージャーには、ディスプレイのミニポート ドライバーの[ **DxgkDdiAcquireSwizzlingRange** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_acquireswizzlingrange)機能、ドライバー設定できるように、スィズル可能性のある割り当てのビットへのアクセスに使用される開口部。 ドライバーは、割り当てのアクセス、PCI aperture へのオフセットでも、開口部に、割り当てが占める領域のサイズを変更できます。 ドライバーが CPU からアクセス可能なこれらの制約の割り当てを行うことはできないかどうか (たとえば、ハードウェア可能性がありますが不足アンスィズル aperture)、ビデオ メモリ マネージャーは、システム メモリへの割り当てを削除でき、アプリケーションからアクセス ビットがあります。

ユーザー モード ドライバーの呼び出しを表示するときに、以前に作成した割り当てのコンテンツがシステム メモリ内ではかどうか、 [ **pfnLockCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb)メモリ、ビデオ メモリ マネージャーに直接アクセスを要求する関数割り当てにアクセスするのには、ユーザー モードのディスプレイ ドライバーとディスプレイのミニポート ドライバーには、システム メモリ バッファーは関係しないを返します。 したがって、割り当てのコンテンツは、ディスプレイのミニポート ドライバーによっては変更されません、によってアンスウィズル形式のままになります。 つまり、ビデオ メモリから CPU アクセスの割り当てが削除されると、ときにディスプレイのミニポート ドライバーする必要がありますすべて割り当て結果のシステム メモリのビットは、アプリケーションで直接アクセスできるようにします。

アクセスしてコンテンツを同じ仮想アプリケーションを続行するため、システム メモリを割り当てのコンテンツを転送する場合は、割り当てが直接のアプリケーション アクセス用に現在マップに関連付けられている GPU リソースが削除されると、アドレスが、別の物理メディア。 転送を設定するには、ビデオ メモリ マネージャーは、ディスプレイのミニポート ドライバーを呼び出します[ **DxgkDdiBuildPagingBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)ページング バッファーを作成する関数と GPU のスケジューラは、ドライバーのを呼び出す[。 **DxgkDdiSubmitCommand** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)関数 GPU 実行単位にページング バッファーをキューに登録します。 ハードウェア固有の転送のコマンドはページング バッファーです。 詳細については、次を参照してください。[コマンド バッファーを送信する](submitting-a-command-buffer.md)します。 ビデオ メモリ マネージャーにより、システム メモリへのビデオへの移行がアプリケーションに表示されないことです。 ただし、ドライバーことを確認します、バイト、バイトの順序付けの割り当て、割り当てが削除されるときに正確に PCI aperture を通じて割り当ての順序と一致します。

Aperture 領域のセグメントの割り当ての基になる bits は、既にシステムのメモリ内でため、削除プロセス中にデータの転送 (アンスィズル) は必要ありません。 そのため、aperture 領域、セグメントにある CPU からアクセス可能な割り当てはスィズルの場合は、アプリケーションから直接アクセスすることはできません。

サーフェスでは、アプリケーションが CPU から直接アクセスされますが、スィズル、aperture 領域セグメントになります場合、ディスプレイ ドライバーは、2 つの異なる割り当てとして、画面を実装する必要があります。 呼び出すことができます、ユーザー モードのディスプレイ ドライバーは、このような画面を作成するとき、 [ **pfnAllocateCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)関数を設定できる、 **NumAllocations**のメンバー、 [**D3DDDICB\_ALLOCATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddicb_allocate)構造体を 2 と**pPrivateDriverData**のメンバー、 [ **D3DDDI\_ALLOCATIONINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationinfo)内の構造体、 **pAllocationInfo** D3DDDICB の配列\_(など、スィズルと unswizzled 割り当てに関するプライベート データを指す割り当て形式)。 GPU によって使用される割り当てにスィズルの形式で bits が含まれており、アプリケーションによってアクセスされる割り当てには unswizzled 形式で bits が含まれています。 ビデオ メモリ マネージャーには、ディスプレイのミニポート ドライバーの[ **DxgkDdiCreateAllocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)の割り当てを作成する関数。 ディスプレイのミニポート ドライバーのプライベート データの解釈 (で、 **pPrivateDriverData**のメンバー、 [ **DXGK\_ALLOCATIONINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)ごとに構造体割り当て)、ユーザー モードのディスプレイ ドライバーから渡されます。 ビデオ メモリ マネージャーは、割り当て; の形式を認識しません。だけ、割り当ての特定のサイズとアラインメントのメモリのブロックを割り当てます。 ユーザー モードのディスプレイ ドライバーへの呼び出し*ロック*処理により、次の操作を画面をロックする関数。

1.  ユーザー モード ドライバーの呼び出しを表示する、 [ **pfnRenderCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb) Direct3D ランタイムとディスプレイのミニポート ドライバーにコマンド バッファー内のすべての操作を送信する関数。

2.  ユーザー モード ドライバーの呼び出しを表示する、 [ **pfnLockCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb)によってアンスウィズル割り当てをロックする関数。 ユーザー モードのディスプレイ ドライバーが、D3DDDILOCKCB を設定する必要がありますいないことに注意してください。\_DONOTWAIT フラグ、**フラグ**、D3DDDICB のメンバー\_ロック構造体。

3.  **PfnLockCb**関数は、割り当ての間で転送 (アンスィズル) が実行されるまで待機します。

4.  **PfnLockCb**関数を要求する、ディスプレイのミニポート ドライバーがによってアンスウィズル割り当ての仮想アドレスを取得し、仮想のアドレスでユーザー モードのディスプレイ ドライバーを返します、 **pData**メンバーの[ **D3DDDICB\_ロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddicb_lock)します。

5.  ユーザー モードのディスプレイ ドライバーでアプリケーションに、によってアンスウィズル割り当ての仮想アドレスを返します、 **pSurfData** D3DDDIARG のメンバー\_ロックします。

 

 





