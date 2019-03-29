---
title: シンセサイザー ミニポート ドライバーの概要
description: シンセサイザー ミニポート ドライバーの概要
ms.assetid: dbd6b95e-f8c8-49f1-ad90-b34821772391
keywords:
- ミニポート ドライバー WDK のオーディオ、シンセサイザー
- シンセサイザー WDK オーディオ、ミニポート ドライバー
- wave シンク WDK オーディオ、ミニポート ドライバー
- DirectMusic カーネル モードの WDK オーディオ、ミニポート ドライバー
- カーネル モードのシンセサイザー WDK オーディオ、ミニポート ドライバー
- ポート ドライバー WDK のオーディオ、シンセサイザー
- ハードウェア アクセラレータ WDK オーディオ
- ミニポート ドライバー WDK オーディオ、カーネル モード ハードウェア アクセラレーション
- シンセサイザー WDK オーディオ、カーネル モードのハードウェア アクセラレーション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53db733ab39d953b78b2787ec29193e631eadf8d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577894"
---
# <a name="synthesizer-miniport-driver-overview"></a>シンセサイザー ミニポート ドライバーの概要


## <span id="synthesizer_miniport_driver_overview"></span><span id="SYNTHESIZER_MINIPORT_DRIVER_OVERVIEW"></span>


シンセサイザーとシンクの両方は、DirectMusic サポートに必要なのです。 それぞれの既定の実装には、DirectMusic が提供されます。 ユーザー モードの Microsoft ソフトウェア シンセサイザーが既定のシンセサイザーとして提供されており、DirectSound は、既定のウェーブ シンク。 これらは完全なハードウェアのエミュレーションを提供しますが、さらにパフォーマンスの強化通常行うにはカーネル モードのソフトウェアまたはハードウェアの実装で。

ハードウェアのサポートを実装する場合、唯一の選択肢では、カーネル モード ドライバーを作成します。 カーネル モードでは、wave シンクは PortCls で Dmu ポート ドライバーによって提供され、(ユーザー モードで行うことがありますが)、カスタム実装を交換する必要はありません。

DirectMusic のカーネル モード ドライバー dmusicks.h は最も重要なヘッダー ファイルです。 ミニポート ドライバーを実装する必要がある主なカーネル モード インターフェイスが含まれています。 これらのインターフェイスは次のとおりです。

[IMiniportDMus](https://msdn.microsoft.com/library/windows/hardware/ff536699)

[ISynthSinkDMus](https://msdn.microsoft.com/library/windows/hardware/ff537011)

[IMXF](https://msdn.microsoft.com/library/windows/hardware/ff536782)

[IAllocatorMXF](https://msdn.microsoft.com/library/windows/hardware/ff536491)

[IMasterClock](https://msdn.microsoft.com/library/windows/hardware/ff536696)

[IPortDMus](https://msdn.microsoft.com/library/windows/hardware/ff536879)

これらのインターフェイスの最後の 3 つは、PortCls.sys で実装されます。

関心のあるその他の 2 つのヘッダー ファイルは dmusprop.h で、DirectMusic プロパティの項目が含まれていると、メインの IRP 構造の DMU を含む dmusbuff.h\_EVENTHEADER します。

次の図は、IHV アダプターのドライバーと DirectMusic システムの残りの部分間のリレーションシップを示します。

![directmusic システムにアダプタのドライバの関係を示す図](images/dmkmbig.png)

最上位のレベルでは、ドライバーは DirectMusic ポート ドライバーを介して公開されます (、 **IDirectMusicPort**インターフェイス インスタンス)。 これは、アプリケーションと DirectMusic との通信です。 このポート ドライバー下と通信する、暗証番号 (pin) のインスタンス経由の呼び出しをストリーミングする標準のカーネルを使用して、 [ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)関数 (Microsoft Windows SDK のドキュメントで説明)。

"Port"という用語に、上の図の 2 つの競合する意味があるに注意してください。 DirectMusic API で用語のポートの使用を混同しないように、上記のユーザー モードでカーネル モードで Dmu ポート ドライバー。 条件では、2 つのコンテキストで似ていますが、若干異なる意味があります。 具体的には、注意、 **IDirectMusicPort**図の上部にあるインターフェイスには、図の下半分で Dmu ポート ドライバーを実装するピンが 1 つのインスタンスの抽象化します。

各ミニポート ドライバー オブジェクトは、一致するポート ドライバー オブジェクトに接続されます。 ポートのドライバー オブジェクトは、ミニポート ドライバーに基本的なサービスを提供します。 デバイスの 1 つの開いているインスタンスにマップされる各の暗証番号 (pin) インスタンスには、形式変換、シーケンス、および"thruing"などのサービス (thruing の詳細については、の説明を参照して、 **IDirectMusicThru** Windows SDK のインターフェイスドキュメント)。 Pin では、ターゲットまたはソースを指定でき、複数のデータ形式と範囲をサポートできます。 各ピンのインスタンスがターゲットまたはソースを指定し、データ形式を指定し、範囲がサポートされます。

IHV のアダプターのドライバーによって、ミニポート ドライバー オブジェクトが作成されます。 ピン留めする 1 つのインスタンスと、ドライバーの開いているインスタンスごとの sequencer は、ハードウェア (または読み込まれたカーネル シンセサイザー ソフトウェア) の 1 台あたり 1 つだけのポート ミニポート ドライバーのペアがあります。 ミニポート ドライバーとの通信は、ミニポート ドライバーでサポートされているプロパティの項目、ミニポート ドライバーには、下位へ渡されるイベントのストリームします。

セクション[DirectMusic ミニポート ドライバー インターフェイス](directmusic-miniport-driver-interface.md)DirectMusic ミニポート ドライバーの実装の詳細を表示します。

 

 




