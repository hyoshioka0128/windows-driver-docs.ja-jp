---
title: プロセスごとの GPU 仮想アドレス スペース
description: 各プロセスは、2つのグラフィックスプロセッシングユニット (GPU) 仮想アドレス空間、アプリケーション GPU 仮想アドレス空間、および特権仮想アドレス空間に関連付けられています。
ms.assetid: 6C7BF67B-217D-4E21-B425-5683C99B63A8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6c19f6b2219f0b24f0bcb74caf631e01d131a34
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829816"
---
# <a name="span-iddisplayper-process_gpu_virtual_address_spacesspanper-process-gpu-virtual-address-spaces"></a><span id="display.per-process_gpu_virtual_address_spaces"></span>プロセスごとの GPU 仮想アドレス空間


各プロセスは、2つのグラフィックスプロセッシングユニット (GPU) 仮想アドレス空間、アプリケーション GPU 仮想アドレス空間、および特権仮想アドレス空間に関連付けられています。

## <a name="span-idapplication_gpu_virtual_address_spacespanspan-idapplication_gpu_virtual_address_spacespanspan-idapplication_gpu_virtual_address_spacespanapplication-gpu-virtual-address-space"></a><span id="Application_GPU_virtual_address_space"></span><span id="application_gpu_virtual_address_space"></span><span id="APPLICATION_GPU_VIRTUAL_ADDRESS_SPACE"></span>アプリケーション GPU 仮想アドレス空間


アプリケーション GPU 仮想アドレス空間は、ユーザーモードドライバーによって生成されたコマンドバッファーが内で実行されるアドレス空間です。 このアドレス空間は、ビデオメモリマネージャーによって提供されるサービスを使用して、ユーザーモードドライバーによって管理されます。 仮想モードで動作している GPU エンジンが割り当てにアクセスできるようにするには、ユーザーモードドライバーが GPU 仮想アドレス範囲を割り当てに割り当てる必要があります。 通常の割り当てでは、これは、ビデオメモリマネージャーによって公開される新しい[*Mapgpuvirtualaddress*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_mapgpuvirtualaddresscb)サービスを使用して行われます。 *Mapgpuvirtualaddress*を使用すると、ユーザーモードドライバーは割り当てをマップする必要がある特定のアドレスを選択できます。また、ビデオメモリマネージャーが使用可能な GPU 仮想アドレスを自動的に選択することもできます。 通常、ドライバーではビデオメモリマネージャーが自動的にアドレスを選択する必要がありますが、状況によっては、ドライバーでより多くの制御が必要になる場合があります。 リンクされたディスプレイアダプターの構成では、 *Mapgpuvirtualaddress*を使用して、現在の gpu またはピア gpu 上の割り当てのインスタンスにマッピングがあるかどうかを指定することもできます。 *Mapgpuvirtualaddress*はビデオメモリマネージャーに要求をキューに置いて、要求が処理されている間、直ちにユーザーモードドライバーに戻ります。 要求はデバイスページングキューでキューに登録されており、ユーザーモードドライバーは、返されたデバイスのページングのフェンス値と同期する必要があります。 [*Freegpuvirtualaddress*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_freegpuvirtualaddresscb)を使用して割り当てを解除し、GPU 仮想アドレスを再利用することができます。 割り当てに関連付けられているすべての仮想アドレスは、割り当てが破棄されると自動的に解放されます。これにより、ユーザーモードドライバーは明示的にマップを解除する必要がなくなります。 ビデオメモリマネージャーでは、ユーザーモードドライバーに2つのタイルリソース固有のサービスが用意されています。 [*ReserveGpuVirtualAddress*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_reservegpuvirtualaddresscb)を使用すると、ユーザーモードドライバーはタイルリソースのアドレス空間を予約できます。また、 [*Updat puvirtualaddress*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_updategpuvirtualaddresscb)を使用すると、ユーザーモードドライバーはタイルリソースの領域を特定のタイルプールページにマップおよびマップ解除できます。 *ReserveGpuVirtualAddress*は、デバイスのページングキューに対して実行されます。一方、 *Updat puvirtualaddress*は、プロセスの特権アドレス空間内で実行される特殊な関連コンテキストで実行されます。

## <a name="span-idprocess_privileged_virtual_address_spacespanspan-idprocess_privileged_virtual_address_spacespanspan-idprocess_privileged_virtual_address_spacespanprocess-privileged-virtual-address-space"></a><span id="Process_privileged_virtual_address_space"></span><span id="process_privileged_virtual_address_space"></span><span id="PROCESS_PRIVILEGED_VIRTUAL_ADDRESS_SPACE"></span>特権仮想アドレス空間の処理


タイルリソースを使用するプロセスでは、 [*ReserveGpuVirtualAddress*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_reservegpuvirtualaddresscb)の最初の呼び出し時に、2つ目の仮想アドレス空間が関連付けられます。 このアドレス空間は、プロセスのページテーブルをレンダリングと同期的に更新するために使用されます。 このアドレス空間については、「[タイルリソース](tile-resources.md)」トピックで説明します。

## <a name="span-idvirtual_address_space_on_linked_display_adaptersspanspan-idvirtual_address_space_on_linked_display_adaptersspanspan-idvirtual_address_space_on_linked_display_adaptersspanvirtual-address-space-on-linked-display-adapters"></a><span id="Virtual_address_space_on_linked_display_adapters"></span><span id="virtual_address_space_on_linked_display_adapters"></span><span id="VIRTUAL_ADDRESS_SPACE_ON_LINKED_DISPLAY_ADAPTERS"></span>リンクされたディスプレイアダプターの仮想アドレス空間


物理グラフィックスアダプターがリンクされたディスプレイアダプターチェーンにリンクされている場合は、プロセスごとに1つの GPU 仮想アドレス空間が存在します (ページングプロセスを除く)。 ただし、各物理アダプターの仮想アドレス空間は、それぞれのページテーブルのセットによってマップされます。

 

 





