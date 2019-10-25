---
title: リソース リストのオブジェクト
description: リソース リストのオブジェクト
ms.assetid: a7f18d28-b78f-4b00-8cbb-9f62f5e88dfd
keywords:
- ヘルパーオブジェクト WDK オーディオ、リソースリストオブジェクト
- リソースリストオブジェクト WDK オーディオ
- IResourceList
- 構成リソースリスト WDK オーディオ
- スタートアップ時間リソース割り当て WDK オーディオ
- ハードウェアリソース割り当て WDK オーディオ
- リソース割り当ての開始 WDK オーディオ
- 起動デバイスルーチン WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 560cdc51eed20bf224f38a58a8726778193a149d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832433"
---
# <a name="resource-list-objects"></a>リソース リストのオブジェクト


## <span id="resource_list_objects"></span><span id="RESOURCE_LIST_OBJECTS"></span>


PortCls システムドライバーは、ミニポートドライバーの利点を得るために[Iresourcelist](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iresourcelist)インターフェイスを実装しています。 IResourceList オブジェクトは、構成リソースリストを表します。これは、デバイスの起動時にプラグアンドプレイマネージャーによってデバイスに割り当てられるシステムハードウェアリソースの一覧です。 スタートアップ時のリソース割り当ての詳細については、「[関数ドライバーでのデバイスの起動](https://docs.microsoft.com/windows-hardware/drivers/kernel/starting-a-device-in-a-function-driver)」を参照してください。

リソースリストには、次の種類のリソースが含まれています。

-   割り込みベクター

-   DMA チャネル

-   I/o ポートアドレス

-   バス相対メモリアドレスのブロック

リソースの種類の詳細については、「[ハードウェアリソース](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources)」を参照してください。

[Iresourcelist](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iresourcelist)オブジェクトは、リソースリストの翻訳されたバージョンと変換されていないバージョン (または "未加工") の両方をカプセル化します。 変換および変換されていないリソースの詳細については、「[バスの相対アドレスを仮想アドレスにマップする](https://docs.microsoft.com/windows-hardware/drivers/kernel/mapping-bus-relative-addresses-to-virtual-addresses)」を参照してください。

[Iresourcelist](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iresourcelist)インターフェイスは、次のメソッドをサポートしています。

[**IResourceList:: AddEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-addentry)

[**IResourceList:: AddEntryFromParent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-addentryfromparent)

[**IResourceList:: FindTranslatedEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-findtranslatedentry)

[**IResourceList:: FindUntranslatedEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-finduntranslatedentry)

[**IResourceList:: NumberOfEntries**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-numberofentries)

[**IResourceList:: Numberofて Oftype**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-numberofentriesoftype)

[**IResourceList:: TranslatedList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-translatedlist)

[**IResourceList:: UntranslatedList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-untranslatedlist)

ヘッダーファイル Portcls は、リソースリストオブジェクトの処理を簡略化するマクロのセットを定義します。 これらのマクロは、 [Iresourcelist](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iresourcelist)メソッドの呼び出しを生成します。 詳細については、「IResourceList」を参照してください。

さらに、Portcls は、リソースリストを作成するための関数のペアを定義します。

[**PcNewResourceList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcelist)

[**PcNewResourceSublist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcesublist)

オーディオアダプターカード上のデバイスを起動するために、オペレーティングシステムはアダプタードライバーの開始デバイスルーチン (「[スタートアップシーケンス](startup-sequence.md)」を参照) を呼び出し、リソースリストオブジェクトを入力パラメーターとして渡します。 この一覧には、オペレーティングシステムがアダプタドライバに割り当てたすべてのシステムリソースが含まれています。

開始デバイスルーチンでは、アダプタードライバーがアダプタードライバーのすべてのデバイス (wave デバイス、MIDI デバイスなど) を起動します。 各デバイスを管理するために、アダプタドライバはミニポートドライバオブジェクトとそれに関連付けられたポートドライバオブジェクトを作成します。 アダプタードライバーは、アダプターカード内のさまざまなデバイスのリソース一覧にあるリソースを分割します。 このため、ドライバーは通常、 [**PcNewResourceSublist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcesublist)を呼び出して、各デバイスのリソースリストオブジェクトを作成します。 次に、ドライバーは、選択したリソースを親リストからさまざまな子リストにコピーするために必要な回数だけ[**Iresourcelist:: AddEntryFromParent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iresourcelist-addentryfromparent)を呼び出します。 さらに、アダプタードライバーによって、一部のリソースがそれ自体に割り当てられる場合があります。

次に、開始デバイスルーチンは、各ポートドライバーの[**IPort:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init)メソッドを呼び出し、デバイスのリソースリストオブジェクト (子リストを含む) を入力パラメーターとして渡します。 各ポートドライバーの**IPort:: init**メソッドは、対応するミニポートドライバーの IMiniport*Xxx*:: init メソッドを呼び出します。これは次のいずれかになります。

[**IMiniportDMus:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-init)

[**IMiniportMidi:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidi-init)

[**IMiniportTopology:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiporttopology-init)

[**IMiniportWaveCyclic:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclic-init)

[**IMiniportWavePci:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-init)

[**IPort:: init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init)メソッドは、そのリソースリストオブジェクトを入力パラメーターとして IMiniport*Xxx*:: init メソッドに渡します。 その後、ミニポートドライバーは、リソースの一覧で DMA チャネル、割り込み、およびその他のシステムリソースを使用できます。

コード例については、Microsoft Windows Driver Kit (WDK) の Sb16 サンプルオーディオドライバーを参照してください。

 

 




