---
title: シンセサイザー ミニポート ドライバーの概要
description: シンセサイザー ミニポート ドライバーの概要
ms.assetid: dbd6b95e-f8c8-49f1-ad90-b34821772391
keywords:
- ミニポートドライバー WDK オーディオ、シンセサイザー
- シンセサイザー WDK オーディオ、ミニポートドライバー
- wave シンク WDK オーディオ、ミニポートドライバー
- DirectMusic カーネルモード WDK オーディオ、ミニポートドライバー
- カーネルモード synths WDK オーディオ、ミニポートドライバー
- ポートドライバー WDK オーディオ、シンセサイザー
- ハードウェア高速化の WDK オーディオ
- ミニポートドライバー WDK オーディオ、カーネルモードハードウェアアクセラレーション
- シンセサイザー WDK オーディオ、カーネルモードハードウェアアクセラレーション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33933445ba62438969e246563f13b4d07171f3a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830018"
---
# <a name="synthesizer-miniport-driver-overview"></a>シンセサイザー ミニポート ドライバーの概要


## <span id="synthesizer_miniport_driver_overview"></span><span id="SYNTHESIZER_MINIPORT_DRIVER_OVERVIEW"></span>


DirectMusic のサポートには、シンセサイザーとシンクの両方が必要です。 各の既定の実装には、DirectMusic が用意されています。 ユーザーモードの Microsoft ソフトウェアシンセサイザーが既定のシンセサイザーとして提供され、DirectSound が既定の wave シンクです。 これらは完全なハードウェアエミュレーションを提供しますが、カーネルモードのソフトウェアまたはハードウェアの実装では、通常、パフォーマンスがさらに向上します。

ハードウェアのサポートを実装する場合、唯一の選択肢は、カーネルモードドライバーを作成することです。 カーネルモードでは、wave シンクは PortCls の DMus ポートドライバーによって提供されるため、カスタム実装で置き換える必要はありません (ユーザーモードで行われることがあります)。

カーネルモードの DirectMusic ドライバーの場合、最も重要なヘッダーファイルは dmusicks です。 これには、ミニポートドライバーを実装するために必要な、メインのカーネルモードインターフェイスが含まれています。 これらのインターフェイスは次のとおりです。

[IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus)

[ISynthSinkDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-isynthsinkdmus)

[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf)

[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iallocatormxf)

[IMasterClock](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imasterclock)

[IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)

これらのインターフェイスの最後の3つは、PortCls に実装されています。

対象となる他の2つのヘッダーファイルには、DirectMusic プロパティアイテムが含まれている dマス EVENTHEADER と、メインの IRP 構造体、DMUS\_が含まれている dマスダン h. h があります。

次の図は、IHV アダプタードライバーとその他の DirectMusic システムの関係を示しています。

![アダプタドライバと directmusic システムとの関係を示す図](images/dmkmbig.png)

最上位レベルでは、ドライバーは DirectMusic ポートドライバー ( **IDirectMusicPort**インターフェイスインスタンス) を介して公開されます。 これは、アプリケーションが DirectMusic と通信する方法です。 このポートドライバーは、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)関数 (Microsoft Windows SDK のドキュメントで説明されています) を使用して、標準のカーネルストリーム呼び出しを介してピンインスタンスに向かって通信します。

上の図では、"port" という用語は2つの競合する意味を持ちます。 上記のユーザーモードで、カーネルモードの DMus ポートドライバーを使用して、DirectMusic API によって使用されているという用語を混同しないようにしてください。 これらの用語は、2つのコンテキストで類似しているが若干異なる意味を持ちます。 特に、図の上部にある**IDirectMusicPort**インターフェイスでは、図の下半分で dmus ポートドライバーが実装する単一の pin インスタンスの抽象化が示されていることに注意してください。

各ミニポートドライバーオブジェクトは、一致するポートドライバーオブジェクトに接続されています。 ポートドライバーオブジェクトは、ミニポートドライバーに基本的なサービスを提供します。 デバイスの1つの開いているインスタンスにマップされる各 pin インスタンスには、形式変換、シーケンス処理、" **ThIDirectMusicThru** " などのサービスがあります (詳細については、Windows SDK のドキュメントでインターフェイスの説明を参照してください)。 ピンはターゲットまたはソースにすることができ、複数のデータ形式と範囲をサポートできます。 各 pin インスタンスはターゲットまたはソースを指定し、サポートされるデータ形式と範囲を指定します。

ミニポートドライバーオブジェクトは、IHV のアダプタードライバーによって作成されます。 ドライバーの開いているインスタンスごとに1つの pin インスタンスと sequencer がありますが、ハードウェアの一部 (または読み込まれたカーネルソフトウェアシンセサイザー) ごとにポートミニポートのドライバーペアが1つだけあります。 ミニポートドライバーとの通信は、ミニポートドライバーに渡されるイベントのストリームと、ミニポートドライバーによってサポートされるプロパティ項目によって行われます。

「 [Directmusic ミニポートドライバーのインターフェイス](directmusic-miniport-driver-interface.md)」では、directmusic ミニポートドライバーの実装の詳細を示しています。

 

 




