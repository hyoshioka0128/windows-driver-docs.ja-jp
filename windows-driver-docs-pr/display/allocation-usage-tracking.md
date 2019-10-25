---
title: 割り当ての使用状況の追跡
description: 割り当て一覧が表示されなくなると、ビデオメモリマネージャーは特定のコマンドバッファーで参照されている割り当てを認識できなくなります。
ms.assetid: F913C9A3-535F-4DA0-8895-7A05CBF4D4AC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eab671084e032857dd80be464bd31ea5b361d251
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839076"
---
# <a name="allocation-usage-tracking"></a>割り当ての使用状況の追跡


割り当て一覧が表示されなくなると、ビデオメモリマネージャーは特定のコマンドバッファーで参照されている割り当てを認識できなくなります。 このため、ビデオメモリマネージャーは、割り当ての使用状況を追跡し、関連する同期を処理するための位置ではなくなりました。 この責任は、ユーザーモードドライバーに分類されるようになります。 特に、ユーザーモードドライバーは、割り当てへの直接の CPU アクセスと名前の変更に関して、同期を処理する必要があります。

割り当ての破棄では、ビデオメモリマネージャーは、呼び出し元のスレッドの非ブロッキングと非常に高いパフォーマンスの両方になる安全な方法で、これらを非同期的に遅延させます。 このようなユーザーモードドライバーでは、割り当ての破棄を延期する必要がありません。 割り当て破棄要求を受信すると、ビデオメモリマネージャーは既定で、破棄要求の前にキューに置かれたコマンドが破棄される割り当てにアクセスし、キューに置かれるまで破棄操作を遅延させる可能性があることを前提としています。コマンドが完了します。 保留中のコマンドが破棄されている割り当てにアクセスしないことをユーザーモードドライバーが認識している場合、 [*Deallocate2*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_deallocate2cb) [**を呼び出すときに AssumeNotInUse フラグを設定することによって、待機せずにビデオメモリマネージャーが要求を処理するように指示することができます。DestroyAllocation2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtdestroyallocation2)。

## <a name="span-idlock2spanspan-idlock2spanspan-idlock2spanlock2"></a><span id="Lock2"></span><span id="lock2"></span><span id="LOCK2"></span>Lock2


ユーザーモードドライバーは、直接の CPU アクセスに対する適切な同期を処理する役割を担います。 特に、次の機能をサポートするには、ユーザーモードドライバーが必要です。

1.  No-overwrite および破棄ロックセマンティクスをサポートします。 これは、ユーザーモードドライバーが独自の名前変更スキームを実装する必要があることを意味します。
2.  同期を必要とするマップ操作 (つまり、上記の上書きなしまたは破棄) の場合、ユーザーモードドライバーは次の操作を行う必要があります。

    -   現在ビジー状態の割り当てにアクセスしようとしたときに、呼び出し元が、呼び出し元のスレッドを**ブロックしない**ことを要求した場合は、 **WasStillDrawing**を返します (**D3D11\_MAP\_フラグ\_\_実行されません @no__ 待機**)。\_
    -   または、 **D3D11\_MAP\_\_フラグ**が設定されていない場合は\_\_待機フラグが設定されていない場合は、割り当てが CPU アクセスに使用できるようになるまで待機します。 ユーザーモードドライバーは、ポーリング以外の待機を実装する必要があります。 ユーザーモードドライバーは、新しいコンテキスト監視メカニズムを使用します。

現時点では、ユーザーモードドライバーは引き続き[*Lockcb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb)/[*UnlockCb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_unlockcb)を呼び出して、ビデオメモリマネージャーに CPU アクセスの割り当てを設定するように求める必要があります。 ほとんどの場合、ユーザーモードドライバーは、割り当てを有効期間全体にわたってマップしたままにすることができます。 ただし、今後、 *Lockcb*と*UnlockCb*は、新しい[*Lock2Cb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lock2cb)と[*Unlock2Cb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_unlock2cb)の呼び出しを優先して非推奨となる予定です。 これらの新しいコールバックの目的は、新しい完全な実装を提供し、新しい一連の引数とフラグを使用することです。

スウィズリングの範囲は Windows Display Driver Model (WDDM) v2 から削除されており、ドライバー開発者は、スウィズリング範囲の依存関係を[*Lockcb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb)の呼び出しから削除し[*ます。Lock2Cb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lock2cb)。

[*Lock2Cb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lock2cb)は、割り当てに仮想アドレスを取得するための簡単な方法として公開されています。 割り当ての種類と、現在現在存在している現在のセグメントに基づいて、いくつかの制限があります。

*Cpu を参照できる*割り当てには、次のものが適用されます。

-   キャッシュされた*cpu で表示*される割り当ては、アパーチャセグメント内に存在するか、またはロックするために常駐していない必要があります。 CPU とグラフィックス処理装置 (GPU) のメモリセグメントの間のキャッシュの整合性を保証することはできません。
-   (サイズ変更可能なバーを使用してサイズを変更して) 完全に*cpu*に表示されるメモリセグメントにある、 *cpu で参照*可能な割り当ては、ロック可能であり、仮想アドレスを返すことができることが保証されます。 このシナリオでは、特別な制約は必要ありません。
-   内に検出された、 *cpu を参照できる*割り当てCPU が*可視*であるメモリセグメント (Cpu*ホストアパーチャ*にアクセスしているか、使用されていないか) は、さまざまな理由で CPU 仮想アドレスにマップできません。 *Cpu ホスト*数が使用可能な領域を超えているか、割り当てによって絞りセグメントが指定されていない場合、仮想アドレスを取得することはできません。 このため、すべての Cpu が*可視*であることが必要です。*Cpu が参照*可能なメモリセグメントには、サポートされているセグメントセット内のアパーチャセグメントが含まれている必要があります。これにより、割り当てをシステムメモリ内に配置して仮想アドレスを指定できるようになります。
-   既にシステムメモリ内に存在する (または、アパーチャセグメントにマップされている) *cpu で参照可能*な割り当ては確実に動作します。

には、次のものが適用されます。*Cpu が参照可能*な割り当て:

-   *Cpu が参照できる*割り当ては、gpu フレームバッファーを直接指すことができないセクションオブジェクトによってバックアップされます。 をロックするには、*Cpu が参照可能*な割り当てでは、割り当てがサポートされているセグメントセット内のアパーチャセグメントをサポートしているか、既にシステムメモリに存在している必要があります (デバイスに常駐させることはできません)。

割り当てがデバイスに常駐しておらず、アパーチャセグメントをサポートしていないときに割り当てが正常にロックされている場合、ロックの期間中は、割り当てがメモリセグメントにコミットされないことが保証される必要があります。

現在、 **Lock2**にはフラグが含まれておらず、**予約済み**フラグのビットはすべて0である必要があります。

## <a name="span-idcpuhostaperturespanspan-idcpuhostaperturespanspan-idcpuhostaperturespancpuhostaperture"></a><span id="CPUHostAperture"></span><span id="cpuhostaperture"></span><span id="CPUHOSTAPERTURE"></span>Cpu ホストアパーチャ


を使用したロックのサポートを強化するには*Cpu が表示*されているメモリセグメントバーのサイズを変更できない場合は、PCI アパーチャで*cpu ホストアパーチャ*が提供されます。 *Cpu ホストアパーチャ*はページベースのマネージャーとして動作し、 [*DxgkDdiMapCpuHostAperture*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_mapcpuhostaperture)DEVICE driver interface (DDI) 機能を使用してビデオメモリの領域に直接マップできます。 これにより、仮想アドレス空間の範囲を*連続して*いない値の範囲に直接マップできるようになります。また、スウィズリングの範囲を必要とせずに、 *Cpu ホストのアパーチャ*をビデオメモリにマップすることができます。

内の CPU が参照できる、ロック可能なメモリの最大量。*Cpu が参照可能*なメモリセグメントは、 *cpu ホストアパーチャ*のサイズに制限されます。 Cpu ホストアパーチャを Microsoft DirectX グラフィックスカーネルに公開する方法の詳細については、「 [CPU ホストの絞り](cpu-host-aperature.md)」を参照してください。

## <a name="span-idi_o_coherencyspanspan-idi_o_coherencyspanspan-idi_o_coherencyspanio-coherency"></a><span id="I_O_coherency"></span><span id="i_o_coherency"></span><span id="I_O_COHERENCY"></span>I/o の一貫性


現在、x86/x64 では、すべての Gpu で、キャッシュ可能なシステムメモリサーフェイスに対して読み取りまたは書き込みを行い、CPU との一貫性を維持するために、PCIe に対する i/o の一貫性をサポートする必要があります。 サーフェイスが GPU の観点からキャッシュ整合性としてマップされている場合、GPU はサーフェイスにアクセスするときに CPU キャッシュを snoop する必要があります。 この形式の一貫性は通常、CPU が読み取りを想定しているリソース (ステージングサーフェスなど) に使用されます。

一部の ARM プラットフォームでは、i/o の一貫性はハードウェアで直接サポートされていません。 これらのプラットフォームでは、CPU キャッシュ階層を手動で無効にすることで、i/o の一貫性をエミュレートする必要があります。 ビデオメモリマネージャーは、GPU (割り当てリストの読み取り/書き込み操作) と CPU (マップ操作、読み取り/書き込み操作) の割り当てに対する操作を追跡し、キャッシュを決定するときにキャッシュの無効化を生成することによって、これを実現します。書き戻し (CPU 書き込み、GPU 読み取り)、または無効にする必要がある古いデータ (GPU 書き込み、CPU 読み取り) を含むデータを格納します。

I/o の一貫性がないプラットフォームでは、割り当てに対する CPU および GPU のアクセスを追跡する責任は、ユーザーモードドライバーによって異なります。 グラフィックスカーネルは、ユーザーモードドライバーがキャッシュ可能な割り当てに関連付けられた仮想アドレス範囲を書き戻して無効にするために使用できる、新しい*無効キャッシュ*DDI を公開します。 I/o の一貫性をサポートしていないプラットフォームでは、ユーザーモードドライバーは、CPU 書き込みの後、GPU が読み込まれる前、および CPU が読み込まれる前に、この関数を呼び出す必要があります。 後者は最初はにくいと思われるかもしれませんが、CPU はメモリに書き込むために GPU 書き込みの前にデータを投機的読み取る可能性があるため、すべての CPU キャッシュを無効にして、CPU が RAM からデータを再読み込みする必要があります。

 

 





