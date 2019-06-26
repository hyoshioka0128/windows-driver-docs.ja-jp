---
title: オーディオ ヘルパー オブジェクトのインターフェイス
description: オーディオ ヘルパー オブジェクトのインターフェイス
ms.assetid: 94d3f7f3-7ccc-4f66-b5fa-95f18b8a0f17
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbd6a960d6932a30be10bb29eaf04262babd17c7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355687"
---
# <a name="audio-helper-object-interfaces"></a>オーディオ ヘルパー オブジェクトのインターフェイス


## <span id="ddk_audio_helper_object_interfaces_ks"></span><span id="DDK_AUDIO_HELPER_OBJECT_INTERFACES_KS"></span>


ポート クラス ライブラリ (portcls.sys) は、さまざまな一般的に使用するアダプターのドライバーの機能を提供するヘルパー オブジェクトを実装します。 これらのヘルパー オブジェクトは、DMA チャネル、割り込み要求、レジストリへのアクセス、リソースの一覧、デジタル著作権、およびハードウェアのイベントを管理するためのメカニズムを提供します。 ここでは、これらのオブジェクトによって公開されるインターフェイスの詳細を示します。

このセクションでは、次のインターフェイスがについて説明します。


[IDrmPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-idrmport)

ミニポート ドライバーが複合 DRM 権利の追跡に役立ちます。

[IDrmPort2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-idrmport2)

ミニポート ドライバーが複合 DRM 権利の追跡に役立ちます。 これは、拡張のバージョンの**IDrmPort**します。

[IInterruptSync](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iinterruptsync)

サービス要求を中断する共有アクセスを調整するための同期メカニズムです。

[IMasterClock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-imasterclock)

マスターのクロックからの参照の現在の時刻に、アクセス権を持つ DirectMusic ストリームを提供します。

[**IPortClsEtwHelper**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportclsetwhelper)

ミニポート ドライバーで Event Tracing for Windows (ETW) のヘルパー関数にアクセスするために使用します。
[IPortClsVersion](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportclsversion)

ドライバーが実行されている Microsoft Windows オペレーティング システムのバージョンを識別します。

[IPortEvents](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportevents)

ミニポート ドライバーによってハードウェア イベント ポート ドライバーに通知するために使用します。

[IPreFetchOffset](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iprefetchoffset)

Microsoft DirectSound ハードウェア バッファーで再生カーソルから書き込みカーソルを分離するデータのバイト数は、プリフェッチのオフセットを設定します。

[IRegistryKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iregistrykey)

レジストリ キーおよびそのサブキーを読み取り/書き込みアクセスを提供します。

[IResourceList](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iresourcelist)

I/O ポート、DMA チャネル、および割り込みなどのリソースの一覧を指定します。

[IServiceGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicegroup)

オブジェクトの一覧に割り込みサービスの要求を多重に使用される[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicesink)インターフェイス。

[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicesink)

割り込みサービス要求のターゲットを表します。

[IUnregisterPhysicalConnection](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iunregisterphysicalconnection)

2 つのサブデバイス同じのオーディオ アダプターまたは 2 つの異なるアダプター間の物理的な接続の登録を削除します。

[IUnregisterSubdevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iunregistersubdevice)

オーディオのアダプターで動的サブデバイスの登録を削除します。

 

 





