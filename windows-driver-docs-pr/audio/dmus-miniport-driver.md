---
title: DMus ミニポート ドライバー
description: DMus ミニポート ドライバー
ms.assetid: a0ce6545-2050-49fb-88b5-a75dcd4c7ebc
keywords:
- オーディオのミニポート ドライバー WDK、Dmu
- ミニポート ドライバー WDK オーディオ、Dmu
- DirectMusic WDK オーディオ、ミニポート ドライバー
- Dmu ミニポート ドライバー WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c703e8dba133d2b12eb5a54daf5a3d17ec11e25d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333756"
---
# <a name="dmus-miniport-driver"></a>DMus ミニポート ドライバー


## <span id="dmus_miniport_driver"></span><span id="DMUS_MINIPORT_DRIVER"></span>


Dmu のミニポート ドライバーでは、高度な MIDI デバイスのハードウェアに依存する機能を管理します。 これらのデバイスでは、有効桁数 sequencer のタイミング、ダウンロード可能なサウンド (DL) およびチャネル グループなどの DirectMusic 機能をサポートします。 Dmu のミニポート ドライバーでは、片方などのデバイスで高パフォーマンスを実現できます。 タイミングは、ミニポート ドライバーまたはハードウェアの機能に応じて、ポート ドライバーのいずれかで処理されることができます。 Dmu のミニポート ドライバーでは、シンセサイザー wave 出力ストリームを生成するソフトウェアもサポートできます。

MIDI ハードウェア デバイス用の Dmu ミニポート ドライバーには、2 つのインターフェイスをサポートする必要があります。

-   ミニポート インターフェイスは、ミニポート オブジェクトを初期化し、MIDI ストリームを作成します。

-   ストリーム インターフェイスでは、MIDI ストリームを管理し、ミニポート ドライバーの機能のほとんどを公開します。

ミニポート インターフェイス[IMiniportDMus](https://msdn.microsoft.com/library/windows/hardware/ff536699)でメソッドを継承、 [IMiniport](https://msdn.microsoft.com/library/windows/hardware/ff536698)インターフェイス。 **IMiniportDMus**次の追加のメソッドを提供します。

[**IMiniportDMus::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536700)

ミニポート オブジェクトを初期化します。

[**IMiniportDMus::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536701)

新しいストリーム オブジェクトを作成します。

[**IMiniportDMus::Service**](https://msdn.microsoft.com/library/windows/hardware/ff536702)

サービスに対する要求のミニポート ドライバーに通知します。

ストリーム インターフェイス、 [IMXF](https://msdn.microsoft.com/library/windows/hardware/ff536782)でメソッドを継承、 **IUnknown**インターフェイス。 **IMXF**次の追加のメソッドを提供します。

[**IMXF::ConnectOutput**](https://msdn.microsoft.com/library/windows/hardware/ff536785)

データ ソースが、このストリーム オブジェクトを接続、 **IMXF**データ シンクは、別のストリーム オブジェクトのインターフェイス。

[**IMXF::DisconnectOutput**](https://msdn.microsoft.com/library/windows/hardware/ff536787)

このストリーム オブジェクトからの切断、 **IMXF**データ シンクは、別のストリーム オブジェクトのインターフェイス。

[**IMXF::PutMessage**](https://msdn.microsoft.com/library/windows/hardware/ff536791)

パスを[ **DMU\_カーネル\_イベント**](https://msdn.microsoft.com/library/windows/hardware/ff536340)データ シンクへの構造体。

[**IMXF::SetState**](https://msdn.microsoft.com/library/windows/hardware/ff536792)

ストリームの状態を設定します。

さらに、Dmu のミニポート ドライバーの[ISynthSinkDMus](https://msdn.microsoft.com/library/windows/hardware/ff537011)インターフェイス ソフトウェア シンセサイザー DLS 機能を提供します。 **ISynthSinkDMus**基底インターフェイスでメソッドを継承**IMXF**します。 **ISynthSinkDMus**次の追加のメソッドを提供します。

[**ISynthSinkDMus::RefTimeToSample**](https://msdn.microsoft.com/library/windows/hardware/ff537013)

参照の時間をサンプル時間に変換します。

[**ISynthSinkDMus::Render**](https://msdn.microsoft.com/library/windows/hardware/ff537015)

Wave シンクのバッファーには、wave データを表示します。

[**ISynthSinkDMus::SampleToRefTime**](https://msdn.microsoft.com/library/windows/hardware/ff537018)

サンプルを参照の時刻に変換します。

[**ISynthSinkDMus::SyncToMaster**](https://msdn.microsoft.com/library/windows/hardware/ff537019)

マスターの時計をサンプルのクロックを同期します。

ポート ドライバーのウェーブ シンクを呼び出す**ISynthSinkDMus::Render** wave PCM を読み取り、MIDI からシンセサイザーを生成するデータの入力ストリーム。 Wave シンクの詳細については、次を参照してください。[カーネル モードのソフトウェアのシンセサイザーの A Wave シンク](a-wave-sink-for-kernel-mode-software-synthesizers.md)します。

ミニポート ドライバーでは、Dmu ポート ドライバーで、次のインターフェイスを呼び出します。

[IPortDMus](https://msdn.microsoft.com/library/windows/hardware/ff536879)

[IAllocatorMXF](https://msdn.microsoft.com/library/windows/hardware/ff536491)

[IMasterClock](https://msdn.microsoft.com/library/windows/hardware/ff536696)

PortCls には UART 関数を使用した、MIDI デバイス用の組み込み Dmu ミニポート ドライバーが含まれています。 詳細については、次を参照してください。 [ **PcNewMiniport**](https://msdn.microsoft.com/library/windows/hardware/ff537714)します。

 

 




