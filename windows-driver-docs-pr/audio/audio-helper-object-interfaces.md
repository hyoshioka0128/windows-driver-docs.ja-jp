---
title: オーディオのヘルパー オブジェクト インターフェイス
description: オーディオのヘルパー オブジェクト インターフェイス
ms.assetid: 94d3f7f3-7ccc-4f66-b5fa-95f18b8a0f17
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5a993a7dca6e1acf423b6870570416084e04bbf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537947"
---
# <a name="audio-helper-object-interfaces"></a>オーディオのヘルパー オブジェクト インターフェイス


## <span id="ddk_audio_helper_object_interfaces_ks"></span><span id="DDK_AUDIO_HELPER_OBJECT_INTERFACES_KS"></span>


ポート クラス ライブラリ (portcls.sys) は、さまざまな一般的に使用するアダプターのドライバーの機能を提供するヘルパー オブジェクトを実装します。 これらのヘルパー オブジェクトは、DMA チャネル、割り込み要求、レジストリへのアクセス、リソースの一覧、デジタル著作権、およびハードウェアのイベントを管理するためのメカニズムを提供します。 ここでは、これらのオブジェクトによって公開されるインターフェイスの詳細を示します。

このセクションでは、次のインターフェイスがについて説明します。


[IDrmPort](https://msdn.microsoft.com/library/windows/hardware/ff536571)

ミニポート ドライバーが複合 DRM 権利の追跡に役立ちます。

[IDrmPort2](https://msdn.microsoft.com/library/windows/hardware/ff536573)

ミニポート ドライバーが複合 DRM 権利の追跡に役立ちます。 これは、拡張のバージョンの**IDrmPort**します。

[IInterruptSync](https://msdn.microsoft.com/library/windows/hardware/ff536590)

サービス要求を中断する共有アクセスを調整するための同期メカニズムです。

[IMasterClock](https://msdn.microsoft.com/library/windows/hardware/ff536696)

マスターのクロックからの参照の現在の時刻に、アクセス権を持つ DirectMusic ストリームを提供します。

[**IPortClsEtwHelper**](https://msdn.microsoft.com/library/windows/hardware/dn265123)

ミニポート ドライバーで Event Tracing for Windows (ETW) のヘルパー関数にアクセスするために使用します。
[IPortClsVersion](https://msdn.microsoft.com/library/windows/hardware/ff536877)

ドライバーが実行されている Microsoft Windows オペレーティング システムのバージョンを識別します。

[IPortEvents](https://msdn.microsoft.com/library/windows/hardware/ff536884)

ミニポート ドライバーによってハードウェア イベント ポート ドライバーに通知するために使用します。

[IPreFetchOffset](https://msdn.microsoft.com/library/windows/hardware/ff536951)

Microsoft DirectSound ハードウェア バッファーで再生カーソルから書き込みカーソルを分離するデータのバイト数は、プリフェッチのオフセットを設定します。

[IRegistryKey](https://msdn.microsoft.com/library/windows/hardware/ff536965)

レジストリ キーおよびそのサブキーを読み取り/書き込みアクセスを提供します。

[IResourceList](https://msdn.microsoft.com/library/windows/hardware/ff536976)

I/O ポート、DMA チャネル、および割り込みなどのリソースの一覧を指定します。

[IServiceGroup](https://msdn.microsoft.com/library/windows/hardware/ff536994)

オブジェクトの一覧に割り込みサービスの要求を多重に使用される[IServiceSink](https://msdn.microsoft.com/library/windows/hardware/ff537006)インターフェイス。

[IServiceSink](https://msdn.microsoft.com/library/windows/hardware/ff537006)

割り込みサービス要求のターゲットを表します。

[IUnregisterPhysicalConnection](https://msdn.microsoft.com/library/windows/hardware/ff537022)

2 つのサブデバイス同じのオーディオ アダプターまたは 2 つの異なるアダプター間の物理的な接続の登録を削除します。

[IUnregisterSubdevice](https://msdn.microsoft.com/library/windows/hardware/ff537030)

オーディオのアダプターで動的サブデバイスの登録を削除します。

 

 





