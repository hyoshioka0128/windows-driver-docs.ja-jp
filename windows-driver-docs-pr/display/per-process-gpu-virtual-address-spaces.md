---
title: プロセスごとの GPU 仮想アドレス スペース
description: 各プロセスは、2 つのグラフィックス処理ユニット (GPU) の仮想アドレス空間、アプリケーション GPU 仮想アドレス空間と、特権を持つ仮想アドレス空間と関連付けられます。
ms.assetid: 6C7BF67B-217D-4E21-B425-5683C99B63A8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4eb3d10aff2362be3c6196b90d0d168bdcaab043
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385580"
---
# <a name="span-iddisplayper-processgpuvirtualaddressspacesspanper-process-gpu-virtual-address-spaces"></a><span id="display.per-process_gpu_virtual_address_spaces"></span>プロセスごとの GPU 仮想アドレス空間


各プロセスは、2 つのグラフィックス処理ユニット (GPU) の仮想アドレス空間、アプリケーション GPU 仮想アドレス空間と、特権を持つ仮想アドレス空間と関連付けられます。

## <a name="span-idapplicationgpuvirtualaddressspacespanspan-idapplicationgpuvirtualaddressspacespanspan-idapplicationgpuvirtualaddressspacespanapplication-gpu-virtual-address-space"></a><span id="Application_GPU_virtual_address_space"></span><span id="application_gpu_virtual_address_space"></span><span id="APPLICATION_GPU_VIRTUAL_ADDRESS_SPACE"></span>アプリケーションの GPU 仮想アドレス空間


アプリケーションの GPU 仮想アドレス空間では、ユーザー モードのドライバーによって生成されたコマンド バッファーが内で実行されるアドレス空間です。 このアドレス空間は、ビデオ メモリ マネージャーによって提供されるサービスを使用して、ユーザー モード ドライバーによって管理されます。 割り当ては、仮想モードで動作している GPU エンジンによってアクセスされることができます、前に、ユーザー モード ドライバーは、割り当てに GPU 仮想アドレスの範囲を割り当てる必要があります。 定期的な割り当ては、これは、新しい[ *MapGpuVirtualAddress* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_mapgpuvirtualaddresscb) 、ビデオ メモリ マネージャーによって公開されるサービスです。 *MapGpuVirtualAddress*ユーザー モード ドライバーは、いずれかの選択には、特定のアドレスを使用している場所、割り当てをマップする必要があるまたはビデオ メモリ マネージャーが使用可能な GPU 仮想アドレスを自動的に選択ができます。 ドライバーが、ビデオ メモリ マネージャーのアドレスを自動的に選択できるようにする必要があります一般的には、状況によっては、ドライバーの詳細に制御を必要があります。 リンクされたディスプレイ アダプターの構成で*MapGpuVirtualAddress*マッピングが現在の GPU 上で、またはピアの GPU での割り当てのインスタンスかどうかを指定できます。 *MapGpuVirtualAddress*ビデオ メモリ マネージャーに要求をキューに配置し、要求の処理中にすぐに、ユーザー モード ドライバーに戻されます。 デバイスのページングのキューの要求がキューにして、ユーザー モード ドライバーのフェンス値のページング、返されたデバイスに対して同期する必要があります確認してください。 [*FreeGpuVirtualAddress* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_freegpuvirtualaddresscb)を割り当てを解除し、GPU 仮想アドレスを解放するために使用できます。 ユーザー モード ドライバーが明示的にマップを解除する必要があるため、割り当てが破棄されるときに、割り当てに関連付けられているすべての仮想アドレスが自動的に解放されます。 ビデオ メモリ マネージャーでは、2 つのタイルがユーザー モード ドライバーにリソースに固有のサービスを提供します。 [*ReserveGpuVirtualAddress* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_reservegpuvirtualaddresscb)タイル リソースのアドレス空間を予約するユーザー モード ドライバーを使用し、 [ *UpdateGpuVirtualAddress* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_updategpuvirtualaddresscb)により、ユーザー モード ドライバーにマップするには特定のタイルのプールのページにタイル リソースのリージョンのマップを解除します。 *ReserveGpuVirtualAddress*デバイス ページング キューに対して実行中に*UpdateGpuVirtualAddress*プロセスの特権を持つアドレス空間内で実行される特殊なコンパニオン コンテキストで実行します。

## <a name="span-idprocessprivilegedvirtualaddressspacespanspan-idprocessprivilegedvirtualaddressspacespanspan-idprocessprivilegedvirtualaddressspacespanprocess-privileged-virtual-address-space"></a><span id="Process_privileged_virtual_address_space"></span><span id="process_privileged_virtual_address_space"></span><span id="PROCESS_PRIVILEGED_VIRTUAL_ADDRESS_SPACE"></span>プロセスの特権仮想アドレス空間


タイルのリソースを使用してプロセスは、最初の呼び出しに関連付けられている、2 つ目の仮想アドレス空間を取得[ *ReserveGpuVirtualAddress*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_reservegpuvirtualaddresscb)します。 このアドレス空間は、レンダリングでは、プロセスのページ テーブルを同期的に更新に使用されます。 このアドレス空間について説明します、[リソースのタイル](tile-resources.md)トピック。

## <a name="span-idvirtualaddressspaceonlinkeddisplayadaptersspanspan-idvirtualaddressspaceonlinkeddisplayadaptersspanspan-idvirtualaddressspaceonlinkeddisplayadaptersspanvirtual-address-space-on-linked-display-adapters"></a><span id="Virtual_address_space_on_linked_display_adapters"></span><span id="virtual_address_space_on_linked_display_adapters"></span><span id="VIRTUAL_ADDRESS_SPACE_ON_LINKED_DISPLAY_ADAPTERS"></span>リンクされたディスプレイ アダプター上の仮想アドレス空間


物理グラフィックス アダプターがリンクされている場合は、アダプターのチェーンを表示する、リンクされた、(ページング プロセス) を除くプロセスごとに 1 つ GPU 仮想アドレス領域が十します。 各物理アダプターの仮想アドレス空間は、独自のページ テーブルのセットによってマップされます。

 

 





