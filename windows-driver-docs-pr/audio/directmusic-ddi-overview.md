---
title: DirectMusic DDI の概要
description: DirectMusic DDI の概要
ms.assetid: 95870103-197c-4b7c-b6ee-cac176b62dfc
keywords:
- Directmusic WDK audio, DirectMusic DDI について
- ユーザーモード synths WDK オーディオ
- カーネルモード synths WDK audio
- ユーザーモードインターフェイス WDK オーディオ
- DMus ポートドライバー WDK オーディオ
- カーネルモードインターフェイス WDK オーディオ
- custom synths WDK audio
- DMus ミニポートドライバー WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f0e69c0db64e1281c607992de9464eec1808ab3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833545"
---
# <a name="directmusic-ddi-overview"></a>DirectMusic DDI の概要


## <span id="directmusic_ddi_overview"></span><span id="DIRECTMUSIC_DDI_OVERVIEW"></span>


ユーザーモードの synths を実装するために必要な設計原則は、通常、カーネルモードの synths にも適用されます。 このため、このガイドでは、ユーザーモードの実装について説明し、特定のカーネルモードのトピックに進みます。

通常、最良の設計方法は、ユーザーモードで実行される DirectMusic*デバイスドライバーインターフェイス (DDI)* のソフトウェア実装を作成することです。 このアプローチは、最終的な製品がハードウェアコンポーネントを使用するカーネルモードの実装である場合でも有益です。 ユーザーモードのバージョンが完了すると、ソフトウェアをカーネルモードに変換し、ハードウェアで確立された接続を一度に1つの機能に変換することができます。 詳細については、「[ユーザーモードとカーネルモード](user-mode-versus-kernel-mode.md)」を参照してください。

DirectMusic は、次のユーザーモードのインターフェイスを使用して、ユーザーモードのシンセサイザーを制御し、カーネルストリーミングドライバーと通信します。

[IDirectMusicSynth](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynth)

これは、カスタムソフトウェア synths を実装するためのユーザーモードインターフェイスです。

[IDirectMusicSynthSink](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynthsink)

これは、Microsoft DirectX 6.1 および DirectX 7 でカスタム wave シンクを実装するためのユーザーモードインターフェイスです。 DirectX 8 以降では、DirectMusic は常にユーザーモードのシンセサイザーでプライベート wave シンクを使用します。ユーザーモードの wave シンクでは、パブリックインターフェイスはサポートされていません。

[Iksk コントロール](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nn-ksproxy-ikscontrol)

DirectMusic は、このインターフェイスを使用して、DirectX 6.1 以降のユーザーモードからカーネルストリームドライバーのプロパティにアクセスします。

カーネルモードの用語は、ポートミニポートドライバーモデル (「 [Port クラスの概要](introduction-to-port-class.md)」を参照) によってユーザーモードと若干異なります。これは、一般的なカーネルストリーミングタスクを[dmus ポートドライバー](dmus-port-driver.md)に委任し、ハードウェア固有の割り当てを行います。DMus ミニポートドライバーに対して機能します。 ポートとミニポートドライバーは、シンセの役割を共有します。 カーネルモード wave シンクは、カーネル常駐ポートドライバーの一部です。 DirectX 6.1 および DirectX 7 のユーザーモードの wave シンクとは異なり、カーネルモードの wave シンクは置き換えられません。 カスタムカーネルモードドライバーを構築するために必要な作業の大部分は、ミニポートドライバーの書き込みです。 ほとんどの場合、ミニポートドライバーは、ドライバーライターがハードウェアをサポートするために実装する必要がある唯一のコンポーネントであるか、または DirectMusic 用のカスタムソフトウェアシンセサイザーを実装するために実装する必要があります。

カスタム DMus ミニポートドライバーは、次のカーネルモードインターフェイスを使用します。

[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iallocatormxf)

[IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus)

[ISynthSinkDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-isynthsinkdmus)

[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf)

[IMasterClock](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imasterclock)

[IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)

DMus ミニポートドライバーは、 **IMiniportDMus**、 **ISynthSinkDMus**、 **imxf**の各インターフェイスを実装します。 DMus ポートドライバーは、 **IAllocatorMXF**、 **Imasterclock**、および**iportdmus**の各インターフェイスを実装し、それらをミニポートドライバーに公開します。

 

 




