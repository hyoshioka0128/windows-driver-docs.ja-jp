---
title: カーネル モードのハードウェア アクセラレータの DDI
description: カーネル モードのハードウェア アクセラレータの DDI
ms.assetid: f3af3caa-0d1f-4da5-8756-ce71c66d5fb6
keywords:
- DirectMusic カーネル モードの WDK オーディオ
- カーネル モード シンセサイザー WDK オーディオ、ハードウェア高速化
- カーネル モードの詳細について、DirectMusic カーネル モードの WDK オーディオ
- カーネル モード シンセサイザー WDK オーディオ、カーネル モードのシンセサイザーについて
- DirectMusic WDK オーディオ、ハードウェア アクセラレーション
- ハードウェア アクセラレータ WDK オーディオ
- ミニポート ドライバー WDK オーディオ、カーネル モード ハードウェア アクセラレーション
- シンセサイザー WDK オーディオ、カーネル モードのハードウェア アクセラレーション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4574b9bde77263e94aa93ea7f71e26ed4c961f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571503"
---
# <a name="kernel-mode-hardware-acceleration-ddi"></a>カーネル モードのハードウェア アクセラレータの DDI


## <span id="kernel_mode_hardware_acceleration_ddi"></span><span id="KERNEL_MODE_HARDWARE_ACCELERATION_DDI"></span>


設計ガイドのこの部分には、DirectMusic 対応のハードウェアまたはソフトウェアのシンセサイザーのカーネル モードの Dmu ミニポート ドライバーを作成するために必要な情報が含まれています。 ここで説明する機能はオプションで、基本レベル MIDI ミニポート ドライバーをサポートするだけでなく実装することができます、 **midiOut**と**midiIn** Microsoft Windows 95/98/Me の ApiWindows NT 4.0、Windows 2000、およびそれ以降。

カーネル モード コンポーネントを実装するには、ミニポート デバイス ドライバー インターフェイス (DDI) に WDM MIDI ドライバー DirectMusic ハードウェア アクセラレーションをサポートするために許可するようの追加する必要があります。 優れたデザイン戦略は、ユーザー モード ドライバーのバージョンを実装して、カーネル モードへの変換を開始する (を参照してください[ユーザー モードとカーネル モード](user-mode-versus-kernel-mode.md))。

カーネル モードの実装を実行する前に、ユーザー モードのバージョンを書き込んでいない場合は、カーネル モードの場合同様に適用されると、概念を理解するには、このドキュメントのユーザー モードのセクションを参照します。 カーネル モードのディスカッションは、ユーザー モードの例で導入された共通の概念をビルドします。

次の 2 つのセクションでは、WDM のストリームの簡単な背景とシンセサイザーのミニポート ドライバーを実装する方法の概要を与えます。

[DirectMusic WDM カーネル ストリーミングの背景](directmusic-wdm-kernel-streaming-background.md)

[シンセサイザー ミニポート ドライバーの概要](synthesizer-miniport-driver-overview.md)

このセクションが含まれています。

[DirectMusic ミニポート ドライバー インターフェイス](directmusic-miniport-driver-interface.md)

[音声の割り当て](voice-allocation.md)

[既定のサウンドのサンプル セット](default-sound-sample-sets.md)

[DirectMusic プロパティのサポート](support-for-directmusic-properties.md)

 

 




