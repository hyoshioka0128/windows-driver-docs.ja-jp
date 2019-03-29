---
title: リソース リストのオブジェクト
description: リソース リストのオブジェクト
ms.assetid: a7f18d28-b78f-4b00-8cbb-9f62f5e88dfd
keywords:
- ヘルパー オブジェクト WDK オーディオ、リソース リスト オブジェクト
- リソース リスト オブジェクトの WDK オーディオ
- IResourceList
- 構成リソースは、WDK のオーディオを一覧表示されます。
- スタートアップ時間のリソース割り当ての WDK オーディオ
- ハードウェア リソースの割り当ての WDK オーディオ
- リソース割り当ての WDK オーディオを開始します。
- デバイスの起動のルーチンの WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00f781a3ab77ca2e7fcd74e3b4a1cb2f4b5b697b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578515"
---
# <a name="resource-list-objects"></a>リソース リストのオブジェクト


## <span id="resource_list_objects"></span><span id="RESOURCE_LIST_OBJECTS"></span>


PortCls システム ドライバーの実装、 [IResourceList](https://msdn.microsoft.com/library/windows/hardware/ff536976)ミニポート ドライバーのためのインターフェイス。 IResourceList オブジェクトは、デバイスのスタートアップ時にデバイスに、プラグ アンド プレイ マネージャを代入するシステムのハードウェア リソースの一覧は、構成リソースの一覧を表します。 スタートアップ時にリソース割り当ての詳細については、次を参照してください。[関数ドライバーでは、デバイスを起動](https://msdn.microsoft.com/library/windows/hardware/ff563856)します。

リソースの一覧には、次の種類リソースにはが含まれています。

-   ベクトルを割り込み

-   DMA チャネル

-   I/O ポートのアドレス

-   バスの相対メモリ アドレスのブロック

リソースの種類については、次を参照してください。[ハードウェア リソース](https://msdn.microsoft.com/library/windows/hardware/ff547012)します。

[IResourceList](https://msdn.microsoft.com/library/windows/hardware/ff536976)オブジェクトには、リソースの一覧の翻訳と無変換 (または「生」) のバージョンがカプセル化します。 変換し、リソースを翻訳しないについての詳細についてを参照してください。 [Bus 相対アドレスを仮想のアドレスにマッピング](https://msdn.microsoft.com/library/windows/hardware/ff554399)します。

[IResourceList](https://msdn.microsoft.com/library/windows/hardware/ff536976)インターフェイスは、次のメソッドをサポートしています。

[**IResourceList::AddEntry**](https://msdn.microsoft.com/library/windows/hardware/ff536978)

[**IResourceList::AddEntryFromParent**](https://msdn.microsoft.com/library/windows/hardware/ff536981)

[**IResourceList::FindTranslatedEntry**](https://msdn.microsoft.com/library/windows/hardware/ff536982)

[**IResourceList::FindUntranslatedEntry**](https://msdn.microsoft.com/library/windows/hardware/ff536984)

[**IResourceList::NumberOfEntries**](https://msdn.microsoft.com/library/windows/hardware/ff536986)

[**IResourceList::NumberOfEntriesOfType**](https://msdn.microsoft.com/library/windows/hardware/ff536988)

[**IResourceList::TranslatedList**](https://msdn.microsoft.com/library/windows/hardware/ff536990)

[**IResourceList::UntranslatedList**](https://msdn.microsoft.com/library/windows/hardware/ff536991)

Portcls.h のヘッダー ファイルでは、リソース リスト オブジェクトの処理を簡略化するマクロのセットを定義します。 これらのマクロの呼び出しの生成、 [IResourceList](https://msdn.microsoft.com/library/windows/hardware/ff536976)メソッド。 詳細については、IResourceList を参照してください。

さらに、Portcls.h には、リソースの一覧を作成するための関数のペアを定義します。

[**PcNewResourceList**](https://msdn.microsoft.com/library/windows/hardware/ff537717)

[**PcNewResourceSublist**](https://msdn.microsoft.com/library/windows/hardware/ff537718)

アダプター ドライバーのデバイスの起動のルーチンを呼び出すと、オペレーティング システム オーディオのアダプター カード上のデバイスを起動する (を参照してください[スタートアップ シーケンス](startup-sequence.md)) し、入力パラメーターとして、リソース リスト オブジェクトで渡します。 この一覧には、アダプターのドライバーをオペレーティング システムが割り当てられているすべてのシステム リソースが含まれています。

デバイスの起動のルーチンでアダプタのドライバはすべてのアダプターのドライバーのデバイス (wave デバイスや、MIDI デバイス) を開始します。 各デバイスを管理するには、アダプターのドライバーは、ミニポート ドライバー オブジェクトとその関連付けられたポート ドライバー オブジェクトを作成します。 アダプターのドライバーはアダプター カード内のさまざまなデバイス間でリソース一覧内のリソースを分割します。 この目的で、ドライバーが通常は呼び出し[ **PcNewResourceSublist** ](https://msdn.microsoft.com/library/windows/hardware/ff537718)デバイスごとにリソースのリスト オブジェクトを作成します。 ドライバーを呼び出して[ **IResourceList::AddEntryFromParent** ](https://msdn.microsoft.com/library/windows/hardware/ff536981)に応じてさまざまな子リストに親の一覧から選択したリソースをコピーする回数。 さらに、アダプターのドライバーでは、それ自体にいくつかのリソースを割り当てることができます。

次に、各ポート ドライバーの呼び出し、デバイスの起動ルーチン[ **iport::init** ](https://msdn.microsoft.com/library/windows/hardware/ff536943)メソッドをデバイスのリソース リスト オブジェクト (子の一覧を含む) を入力パラメーターとして渡します。 各ポート ドライバーの**iport::init**メソッドは、対応するミニポート ドライバーの IMiniport*Xxx*:: Init メソッドは、次の 1 つです。

[**IMiniportDMus::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536700)

[**IMiniportMidi::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536709)

[**IMiniportTopology::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536713)

[**IMiniportWaveCyclic::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536722)

[**IMiniportWavePci::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536734)

[ **Iport::init** ](https://msdn.microsoft.com/library/windows/hardware/ff536943)メソッドは、IMiniport をそのリソースのリスト オブジェクトを渡します*Xxx*:: 入力パラメーターとしてメソッドを初期化します。 ミニポート ドライバーでは、DMA の利用をことができますし、チャネル、割り込み、およびリソースの一覧で他のシステム リソース。

コード例では、Sb16 サンプル オーディオ ドライバーで、Microsoft Windows Driver Kit (WDK) を参照してください。

 

 




