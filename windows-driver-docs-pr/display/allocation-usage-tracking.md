---
title: 割り当ての使用状況の追跡
description: 消滅の割り当てリスト、ビデオ メモリ マネージャーはなくなりました可視性を特定のコマンド バッファーで参照されている割り当て。
ms.assetid: F913C9A3-535F-4DA0-8895-7A05CBF4D4AC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5a6e169b040825ac1d2ab84e086ef16c02054c2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579494"
---
# <a name="allocation-usage-tracking"></a>割り当ての使用状況の追跡


消滅の割り当てリスト、ビデオ メモリ マネージャーはなくなりました可視性を特定のコマンド バッファーで参照されている割り当て。 このため、ビデオ メモリ マネージャーが割り当ての使用状況を追跡し、関連の同期を処理するために、位置。 この責任はユーザー モード ドライバーに今すぐ分類されます。 具体的には、ユーザー モード ドライバーは、割り当てと名前の変更に直接アクセスする CPU に対して同期を処理する必要があります。

割り当ての破棄のビデオ メモリ マネージャーは非同期的に延期がどちらも非ブロッキング呼び出し元のスレッドと非常に高いパフォーマンスの安全な方法でこれらします。 そのため、ユーザー モード ドライバーは、割り当ての破棄を延期することを気にするがありません。 ビデオ メモリ マネージャーが前提としています、既定で破棄要求する前にキューに置かれた可能性があります破棄されている割り当てのアクセス可能性のあるコマンドと、キューに置かれたまで、破棄操作を延期割り当て破棄要求を受信すると、コマンドが完了します。 ユーザー モード ドライバーを知っている保留中のコマンドを設定して、ビデオ メモリ マネージャー プロセスを待たず、要求するよう指示できますが、破棄されている割り当てにアクセスしない場合、 **AssumeNotInUse**フラグを呼び出すときに[ *Deallocate2* ](https://msdn.microsoft.com/library/windows/hardware/dn906353)または[ **DestroyAllocation2**](https://msdn.microsoft.com/library/windows/hardware/dn906772)します。

## <a name="span-idlock2spanspan-idlock2spanspan-idlock2spanlock2"></a><span id="Lock2"></span><span id="lock2"></span><span id="LOCK2"></span>Lock2


ユーザー モード ドライバーは、CPU への直接アクセスに関して適切な同期の処理になります。 具体的には、ユーザー モード ドライバーは、以下をサポートする必要があります。

1.  サポートは、no 上書きし、ロック セマンティクスを破棄します。 つまり、ユーザー モード ドライバーが、独自の名前の変更のスキームを実装する必要があるということです。
2.  マップ操作が同期されていない、上記 no-overwrite (破棄) することで、ユーザー モード ドライバーをする必要があります。

    -   返す**WasStillDrawing**割り当ては現在ビジー状態にアクセスしようし、する、呼び出し元が要求した場合、**ロック**操作呼び出し元のスレッドをブロック (**D3D11\_マップ\_フラグ\_は\_いない\_待機**)。
    -   または、 **D3D11\_マップ\_フラグ\_は\_いない\_待機**フラグが設定されていない、割り当てが CPU アクセス可能になるまで待機します。 ユーザー モード ドライバーは、非ポーリング待機を実装する必要があります。 ユーザー モードのドライバーのメカニズムを監視する新しいコンテキストを使用します。

ここでは、ユーザー モード ドライバーは引き続き呼び出す必要があります[ *LockCb*](https://msdn.microsoft.com/library/windows/hardware/ff568914)/[*UnlockCb* ](https://msdn.microsoft.com/library/windows/hardware/ff569011)ビデオ メモリを要求するにはCPU へのアクセスの割り当てを設定するマネージャー。 ほとんどの場合、ユーザー モード ドライバーは存続期間全体にマップされている割り当てを保持することになります。 ただし、今後で*LockCb*と*UnlockCb*新しい優先の廃止される予定[ *Lock2Cb* ](https://msdn.microsoft.com/library/windows/hardware/dn914483)と[ *Unlock2Cb* ](https://msdn.microsoft.com/library/windows/hardware/dn914484)呼び出し。 これらの新しいコールバックの目的は、引数とフラグの新しいセットを新しいクリーンな実装を提供することです。

スウィズ リング範囲は、Windows Display Driver Model (WDDM) v2 から削除されへの呼び出しからスウィズ リング範囲への依存関係を削除するドライバー開発者の責任は[ *LockCb* ](https://msdn.microsoft.com/library/windows/hardware/ff568914)として実装に基づいているに向かって移動[ *Lock2Cb*](https://msdn.microsoft.com/library/windows/hardware/dn914483)します。

[*Lock2Cb* ](https://msdn.microsoft.com/library/windows/hardware/dn914483)仮想アドレス割り当てを取得するための単純なメソッドとして公開されます。 割り当てと同様に現在常駐している現在のセグメントの種類に基づいて、いくつかの制限があります。

次の適用の*CPUVisible*割り当て。

-   キャッシュ*CPUVisible*割り当てする必要があります、aperture セグメント内に存在またはロックするには存在できません。 CPU と、グラフィックス プロセッシング ユニット (GPU) 上のメモリ セグメントの間のキャッシュの一貫性は保証できません。
-   *CPUVisible*内にある割り当てを完全に*CPUVisible* lockable と仮想のアドレスを返すことができません (サイズ変更可能なバーを使用してサイズ変更) メモリ セグメントが保証されます。 このシナリオでは、特殊な制約は必要ありません。
-   *CPUVisible*内に配置された割り当て、!*CPUVisible*メモリ セグメント (へのアクセスの有無、 *CPUHostAperture*) をさまざまな理由から、CPU の仮想アドレスにマップされることはできません。 場合、 *CPUHostAperture*領域または割り当てが aperture セグメントを指定していない、仮想のアドレスは、取得することはできませんが使用可能な外です。 このためする必要がありますすべて*CPUVisible*内の割り当て!*CPUVisible*メモリ セグメントは、私たちはシステム メモリ内で割り当てを配置し、仮想のアドレスを提供できることを保証する設定がサポートされているセグメントの絞りセグメントを含める必要があります。
-   *CPUVisible*割り当て既にシステム メモリ内にある (または aperture セグメントにマップされている) 動作することが保証されます。

次に適用されます。*CPUVisible*割り当て。

-   *CPUVisible* Gpu フレーム バッファーを直接指し示すことはできませんが、セクション オブジェクトによって割り当てがサポートされます。 ロックするために、!*CPUVisible*割り当てまたはいる必要が割り当てのサポートでサポートされているセグメントの開口部セグメント設定すると、(する必要がありますはないデバイスに存在)、システム メモリにあること。

割り当てが正常にロックされていると、割り当てが、デバイスに存在することはありませんが、絞りセグメントをサポートしていません、いないコミット メモリ セグメントにロックの期間中に、割り当てを保証する必要があります。

**Lock2**現在フラグがないと**占有**すべてのフラグのビットが 0 をする必要があります。

## <a name="span-idcpuhostaperturespanspan-idcpuhostaperturespanspan-idcpuhostaperturespancpuhostaperture"></a><span id="CPUHostAperture"></span><span id="cpuhostaperture"></span><span id="CPUHOSTAPERTURE"></span>CPUHostAperture


ロックに対する優れたサポート。*CPUVisible*バーのサイズ変更に失敗した場合は、メモリのセグメントを*CPUHostAperture* PCI aperture で提供されます。 *CPUHostAperture*経由でのビデオ メモリの領域に直接マップできるページ ベースのマネージャーとして動作、 [ *DxgkDdiMapCpuHostAperture*](https://msdn.microsoft.com/library/windows/hardware/dn906340)デバイス ドライバーインターフェイス (DDI) 関数。 不連続な範囲に直接仮想アドレス空間の範囲をマップできる、 *CPUHostAperture*、いて、 *CPUHostAperture*ビデオ メモリを必要としないにマップし、スウィズ リングの範囲です。

内に CPU によって参照可能なロック可能なメモリ量の最大!*CPUVisible*メモリ セグメントがのサイズに制限されていますが、 *CPUHostAperture*します。 公開するための詳細、 *CPUHostAperture* Microsoft DirectX のグラフィックスにカーネルで見つかる、 [CPU ホスト aperture](cpu-host-aperature.md)トピック。

## <a name="span-idiocoherencyspanspan-idiocoherencyspanspan-idiocoherencyspanio-coherency"></a><span id="I_O_coherency"></span><span id="i_o_coherency"></span><span id="I_O_COHERENCY"></span>I/O の一貫性


X86 または x64 で今日では、要求の読み取りまたは書き込みをキャッシュ可能なシステム メモリの画面におよび CPU との一貫性を維持するための GPU を許可するために、すべての Gpu が PCIe 経由で I/O の一貫性をサポートするします。 GPU の観点から一貫したキャッシュとしてサーフェスがマッピングされると、GPU は、画面にアクセスするとき、CPU キャッシュの内容を確認する必要があります。 このフォームの一貫性は、通常、CPU ステージング サーフェスの一部など、読み取ったりする必要のあるリソースの使用します。

一部の ARM プラットフォームで I/O の一貫性はハードウェアで直接サポートされていません。 これらのプラットフォームでは、I/O の一貫性が CPU のキャッシュ階層を手動で無効にすることをエミュレートする必要があります。 ビデオ メモリ マネージャーでは、今すぐこれを実現 (マップの操作、読み取り/書き込み) の CPU と GPU (一覧の読み取り/書き込み操作の割り当て) から割り当てに操作を追跡して、キャッシュがいずれかを決定したら、キャッシュの無効化の出力書き戻す必要があるデータを含む (書き込みの CPU、GPU の読み取り) または無効にする必要がある古いデータを含む (GPU 書き込み、CPU の読み取り)。

ありません I/O 一貫性でのプラットフォームでは、割り当てに CPU と GPU アクセスを追跡する必要がありますが、ユーザー モード ドライバーになります。 グラフィックスのカーネルが新しい公開*が無効になるキャッシュ*DDI ライトバック キャッシュ可能な割り当てに関連付けられている仮想アドレスの範囲が無効にして、ユーザー モード ドライバーを使用します。 I/O の一貫性のサポートがないプラットフォームでは、ユーザー モード ドライバーが CPU の書き込み後に GPU 読み取り前にだけでなく書き込み後と CPU を読み取る前に、この関数を呼び出す必要があります。 後者かもしれませんはわかりにくい最初は、CPU をメモリに GPU 前のデータの書き込み投機的読み可能性があります、ため、CPU が RAM からのデータを再読み込みを確実にすべての CPU キャッシュを無効にする必要しますですが、。

 

 





