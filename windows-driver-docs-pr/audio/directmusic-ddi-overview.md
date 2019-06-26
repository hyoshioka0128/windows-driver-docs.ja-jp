---
title: DirectMusic DDI の概要
description: DirectMusic DDI の概要
ms.assetid: 95870103-197c-4b7c-b6ee-cac176b62dfc
keywords:
- DirectMusic WDK オーディオ、DirectMusic DDI について
- ユーザー モード シンセサイザー WDK オーディオ
- カーネル モード シンセサイザー WDK オーディオ
- ユーザー モード インターフェイス WDK オーディオ
- Dmu ポート ドライバー WDK オーディオ
- カーネル モード インターフェイス WDK オーディオ
- カスタムのシンセサイザー WDK オーディオ
- Dmu ミニポート ドライバー WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2194a22d2540aeac8d0c89890d879bb2a63ff2e2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359051"
---
# <a name="directmusic-ddi-overview"></a>DirectMusic DDI の概要


## <span id="directmusic_ddi_overview"></span><span id="DIRECTMUSIC_DDI_OVERVIEW"></span>


カーネル モードのシンセサイザーもに、通常ユーザー モードのシンセサイザー機能を実装するために必要なデザインの原則が適用されます。 このため、このガイドは、ユーザー モードの実装とカーネル モードの特定のトピックへの進行状況の説明で始まります。

最初に、DirectMusic のソフトウェアの実装を記述する最適な設計戦略では通常、*デバイス ドライバー インターフェイス (DDI)* ユーザー モードで実行します。 最終的な製品がカーネル モードの実装のハードウェア コンポーネントを使用する場合でも、このアプローチの使用をお勧めします。 ユーザー モードのバージョンが完了すると、ソフトウェアは、カーネル モード ドライバーとハードウェア、一度に 1 つの機能によって確立された接続に変換できます。 詳細については、次を参照してください。[ユーザー モードとカーネル モード](user-mode-versus-kernel-mode.md)します。

DirectMusic は、次のユーザー モード インターフェイスをユーザー モードのシンセサイザーのコントロールを使用して、カーネル ストリーミング ドライバーの通信。

[IDirectMusicSynth](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynth)

これは、カスタム ソフトウェア シンセサイザー機能を実装するため、ユーザー モード インターフェイスです。

[IDirectMusicSynthSink](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynthsink)

これは、Microsoft DirectX 6.1 と DirectX 7 でカスタム wave シンクを実装するため、ユーザー モード インターフェイスです。 DirectX 8 以降では、DirectMusic は常に、ユーザー モード シンセサイザーでそのプライベート wave シンクを使用し、ユーザー モード wave シンクのパブリック インターフェイスはサポートされていません。

[IKsControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nn-ksproxy-ikscontrol)

DirectMusic では、このインターフェイスを使用して、DirectX 6.1 以降のユーザー モードからカーネル ストリーミング ドライバーのプロパティにアクセスします。

カーネル モードの用語とは若干異なりますユーザー モード ポート ミニポート ドライバー モデルであるため (を参照してください[ポート クラスの概要](introduction-to-port-class.md))、カーネル ストリーミングの一般的なタスクを委任する、 [Dmu ポート ドライバー](dmus-port-driver.md)ハードウェア固有の関数を Dmu のミニポート ドライバーに割り当てます。 ポートおよびミニポート ドライバーではのシンセサイザーの責任を共有します。 カーネル モードのウェーブ シンクは、カーネル常駐ポート ドライバーの一部です。 カーネル モードのウェーブ シンクとは異なり、ユーザー モード wave のシンク DirectX 6.1 と DirectX 7 には、置き換え可能なされません。 カスタム カーネル モード ドライバーをビルドするために必要な作業のほとんどは、ミニポート ドライバーの執筆中です。 ほとんどの場合、ミニポート ドライバーはドライバー ライターがのハードウェアをサポートするために、または DirectMusic のカスタム ソフトウェア シンセサイザーを実装するために実装する必要がある唯一のコンポーネント。

カスタムの Dmu ミニポート ドライバーでは、次のカーネル モード インターフェイスを使用します。

[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iallocatormxf)

[IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iminiportdmus)

[ISynthSinkDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-isynthsinkdmus)

[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-imxf)

[IMasterClock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-imasterclock)

[IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iportdmus)

Dmu ミニポート ドライバーを実装して、 **IMiniportDMus**、 **ISynthSinkDMus**、および**IMXF**インターフェイス。 Dmu ポート ドライバーの実装、 **IAllocatorMXF**、 **IMasterClock**、および**IPortDMus**インターフェイスおよびミニポート ドライバーを許すことにします。

 

 




