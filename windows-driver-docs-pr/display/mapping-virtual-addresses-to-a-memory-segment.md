---
title: メモリ セグメントへの仮想アドレスのマッピング
description: メモリ セグメントへの仮想アドレスのマッピング
ms.assetid: 3ff64e33-eceb-4603-a3d9-11cb2f7dac85
keywords:
- メモリセグメント WDK 表示、仮想アドレスのマッピング
- 仮想アドレスのマッピング
- 仮想アドレスマッピング WDK ディスプレイ
- CPU 仮想アドレスマッピング WDK ディスプレイ
- 線形アパーチャ-スペースセグメントの WDK ディスプレイ
- アパーチャスペースセグメントの WDK ディスプレイ
- 線形メモリスペースセグメント WDK ディスプレイ
- メモリスペースセグメントの WDK ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 831f2687c6c2bae43c9b2c7ac33b3aff80a8d35b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840580"
---
# <a name="mapping-virtual-addresses-to-a-memory-segment"></a>メモリ セグメントへの仮想アドレスのマッピング


## <span id="ddk_mapping_virtual_addresses_to_a_memory_segment_gg"></span><span id="DDK_MAPPING_VIRTUAL_ADDRESSES_TO_A_MEMORY_SEGMENT_GG"></span>


ディスプレイミニポートドライバーは、定義されているメモリ空間またはスペースセグメントごとに、CPU 仮想アドレスが、フラグでの CPU の**可視**性ビットフィールドフラグを設定することによって、セグメントにある割り当てに直接マップできるかどうかを指定できます。セグメントの[**DXGK\_SEGMENTDESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)構造体のメンバー。

CPU 仮想アドレスをセグメントにマップするには、セグメントに PCI アパーチャを介した線形アクセスが必要です。 言い換えると、セグメント内の割り当てのオフセットは、PCI アパーチャのオフセットと同じである必要があります。 したがって、ビデオメモリマネージャーは、指定されたセグメント内の割り当てのオフセットに基づいて、割り当てのバス相対物理アドレスを計算できます。

次の図は、仮想アドレスを線形メモリ空間セグメントにマップする方法を示しています。

![線形メモリ空間セグメントにマップされた仮想アドレスを示す図](images/vrtlmap.png)

次の図は、仮想アドレスを、線形のアパーチャ空間セグメントの基になるページにマップする方法を示しています。

![線形的なアパーチャ空間セグメントの基になるページにマップされた仮想アドレスを示す図](images/vrtlmap2.png)

仮想アドレスをセグメントの一部にマッピングする前に、ビデオメモリマネージャーはディスプレイミニポートドライバーの[**DxgkDdiAcquireSwizzlingRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_acquireswizzlingrange)関数を呼び出して、割り当てのビットにアクセスするために使用されるアパーチャをドライバーが設定できるようにします。これはスィズルされる可能性があります。 ドライバーは、割り当てがアクセスされる PCI 絞りのオフセットと、割り当てによって絞り込まれる領域のサイズを変更できません。 これらの制約を指定して、ドライバーが割り当て CPU にアクセスできない場合 (たとえば、ハードウェアが unswizzling アパーチャを使い果たした場合など)、ビデオメモリマネージャーはシステムメモリに割り当てを見つけ、アプリケーションがそこにあるビットにアクセスできるようにします。

以前に作成した割り当ての内容がシステムメモリ内にある場合、ユーザーモード表示ドライバーが[**Pfnlockcb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb)関数を呼び出してメモリへの直接アクセスを要求したときに、ビデオメモリマネージャーがシステムメモリバッファーをユーザーモードディスプレイに返します。ドライバー、およびディスプレイミニポートドライバーは、割り当てへのアクセスには関与しません。 そのため、割り当てのコンテンツはディスプレイミニポートドライバーによって変更されず、非スィズル形式のままになります。 つまり、CPU アクセス可能な割り当てがビデオメモリから削除された場合、ディスプレイミニポートドライバーは、アプリケーションから結果のシステムメモリビットに直接アクセスできるように、割り当てを unswizzle する必要があることを意味します。

アプリケーションに直接アクセスするためにマップされている割り当てに関連付けられている GPU リソースが削除された場合、アプリケーションが同じ仮想ネットワークにあるコンテンツに引き続きアクセスできるように、割り当ての内容がシステムメモリに転送されます。アドレスは、物理的なメディアは異なっています。 転送を設定するために、ビデオメモリマネージャーはディスプレイミニポートドライバーの[**DxgkDdiBuildPagingBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)関数を呼び出してページングバッファーを作成し、GPU スケジューラはドライバーの[**DxgkDdiSubmitCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)関数を呼び出してページングをキューに入れます。GPU 実行単位にバッファーします。 ハードウェア固有の転送コマンドは、ページングバッファーにあります。 詳細については、「[コマンドバッファーを送信する](submitting-a-command-buffer.md)」を参照してください。 ビデオメモリマネージャーを使うと、ビデオのシステムメモリへの移行がアプリケーションに対して非表示になります。 ただし、ドライバーでは、割り当てが削除されたときの割り当てのバイト順序と、PCI アパーチャによる割り当てのバイト順が正確に一致している必要があります。

アパーチャ領域セグメントの場合、割り当ての基になるビットが既にシステムメモリ内にあるため、削除処理中にデータの転送 (unswizzling) を行う必要はありません。 そのため、アプリケーションによって直接アクセスされる場合、アパーチャ空間セグメントにある CPU アクセス可能な割り当てをスィズルすることはできません。

アプリケーションによって CPU 経由でサーフェイスに直接アクセスできるが、アパーチャ空間セグメントでスィズルされる場合、ディスプレイドライバーは、2つの異なる割り当てとしてサーフェイスを実装する必要があります。 ユーザーモード表示ドライバーは、このような画面を作成するときに、 [**Pfnallocatecb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)関数を呼び出すことができます。また、 [ **\_D3DDDICB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_allocate)の**numallocations**メンバーを設定して、構造体を2に割り当て、の**pprivatedriverdata**メンバーに割り当てることができます。\_D3DDDICB の[**D3DDDI\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationinfo) **の配置**情報の構造体は、割り当てに関するプライベートデータ (スィズル形式や非スィズル形式など) を指すために割り当てられます。 GPU によって使用される割り当てには、スィズルされた形式のビットが含まれ、アプリケーションによってアクセスされる割り当てには、非スィズル形式のビットが含まれます。 ビデオメモリマネージャーは、ディスプレイミニポートドライバーの[**DxgkDdiCreateAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)関数を呼び出して、割り当てを作成します。 表示ミニポートドライバーは、ユーザーモードの表示ドライバーから渡されるプライベートデータ (各割り当ての[**DXGK\_ALLOCATION info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)構造体の**Pprivatedriverdata**メンバー) を解釈します。 ビデオメモリマネージャーは、割り当ての形式を認識していません。特定のサイズのメモリブロックと割り当ての配置を割り当てるだけです。 処理のために画面をロックするためのユーザーモード表示ドライバーの*ロック*関数の呼び出しでは、次の処理が行われます。

1.  ユーザーモードの表示ドライバーは、 [**Pfnrendercb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)関数を呼び出して、コマンドバッファー内の unswizzle 操作を Direct3D ランタイムに、表示ミニポートドライバーに送信します。

2.  ユーザーモード表示ドライバーは、 [**Pfnlockcb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb)関数を呼び出して、スィズルされていない割り当てをロックします。 ユーザーモードの表示ドライバーでは、D3DDDICB\_LOCK 構造体の**Flags**メンバーで D3DDDILOCKCB\_DONOTWAIT フラグを設定してはいけないことに注意してください。

3.  **Pfnlockcb**関数は、割り当て間の転送 (unswizzling) が実行されるまで待機します。

4.  **Pfnlockcb**関数は、ディスプレイミニポートドライバーが、非スィズル割り当ての仮想アドレスを取得し、 [**D3DDDICB\_LOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_lock)の**pData**メンバーのユーザーモード表示ドライバーに仮想アドレスを返すことを要求します。

5.  ユーザーモードの表示ドライバーは、D3DDDIARG\_LOCK の**P氏 Fdata**メンバー内のアプリケーションに、未スィズル割り当ての仮想アドレスを返します。

 

 





