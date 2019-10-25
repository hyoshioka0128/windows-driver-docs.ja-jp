---
title: オーディオ ヘルパー オブジェクトのインターフェイス
description: オーディオ ヘルパー オブジェクトのインターフェイス
ms.assetid: 94d3f7f3-7ccc-4f66-b5fa-95f18b8a0f17
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd9b7566d0d16c2b727a1b8d656918b28d7de518
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833678"
---
# <a name="audio-helper-object-interfaces"></a>オーディオ ヘルパー オブジェクトのインターフェイス


## <span id="ddk_audio_helper_object_interfaces_ks"></span><span id="DDK_AUDIO_HELPER_OBJECT_INTERFACES_KS"></span>


ポートクラスライブラリ (portcls) は、アダプタードライバーに一般的に使用される機能を提供するさまざまなヘルパーオブジェクトを実装します。 これらのヘルパーオブジェクトは、DMA チャネル、割り込み要求、レジストリアクセス、リソースリスト、デジタル権限、およびハードウェアイベントを管理するためのメカニズムを提供します。 ここでは、これらのオブジェクトによって公開されるインターフェイスの詳細について説明します。

このセクションでは、次のインターフェイスについて説明します。


[IDrmPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idrmport)

ミニポートドライバーが複合 DRM 権限を追跡するのに役立ちます。

[IDrmPort2](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idrmport2)

ミニポートドライバーが複合 DRM 権限を追跡するのに役立ちます。 これは、 **Idrmport**の拡張バージョンです。

[IInterruptSync](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iinterruptsync)

割り込みサービス要求への共有アクセスを調整するための同期機構。

[IMasterClock](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imasterclock)

マスタークロックから現在の参照時刻にアクセスできる DirectMusic ストリームを提供します。

[**IPortClsEtwHelper**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportclsetwhelper)

Windows イベントトレーシング (ETW) ヘルパー関数にアクセスするためにミニポートドライバーによって使用されます。
[IPortClsVersion](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportclsversion)

ドライバーが実行されている Microsoft Windows オペレーティングシステムのバージョンを識別します。

[IPortEvents](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportevents)

ミニポートドライバーによって、ハードウェアイベントのポートドライバーに通知するために使用されます。

[IPreFetchOffset](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iprefetchoffset)

プリフェッチオフセットを設定します。これは、Microsoft DirectSound ハードウェアバッファーの play カーソルから書き込みカーソルを分離するデータのバイト数です。

[IRegistryKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iregistrykey)

レジストリキーとそのサブキーへの読み取り/書き込みアクセスを提供します。

[IResourceList](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iresourcelist)

I/o ポート、DMA チャネル、割り込みなどのリソースの一覧を指定します。

[IServiceGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicegroup)

[Iservices ink](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)インターフェイスを使用して、割り込みサービス要求をオブジェクトの一覧に対して多重化するために使用されます。

[Iサービスインク](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)

割り込みサービス要求のターゲットを表します。

[IUnregisterPhysicalConnection](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iunregisterphysicalconnection)

同じオーディオアダプター内の2つのサブデバイス間、または2つの異なるアダプターにある物理接続の登録を削除します。

[IUnregisterSubdevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iunregistersubdevice)

オーディオアダプターの動的サブデバイスの登録を削除します。

 

 





