---
title: ビデオのミニポート ドライバーでの割り込み
description: ビデオのミニポート ドライバーでの割り込み
ms.assetid: bf84a3fb-860a-4647-ac34-93f3a22b166b
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、割り込み
- WDK のビデオのミニポートを中断します。
- HwVidInterrupt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdcf2c0fea7d89b117c135238833bf0ae565746b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558996"
---
# <a name="interrupts-in-video-miniport-drivers"></a>ビデオのミニポート ドライバーでの割り込み


## <span id="ddk_interrupts_in_video_miniport_drivers_gg"></span><span id="DDK_INTERRUPTS_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


割り込みを生成するアダプターのビデオのミニポート ドライバーを実装する必要があります、 [ *HwVidInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/ff567349)ルーチン。 ミニポート ドライバーの[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff556159)ルーチンを初期化する必要があります、 **HwInterrupt**のメンバー、 [**ビデオ\_HW\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff570505)割り込みハンドラーを指す構造体。

ビデオ ポート ドライバーは、アダプターが割り込みを生成する場合、ビデオのミニポート ドライバーの割り込みオブジェクトを設定します。 割り込みオブジェクトが作成され、ビデオ ポート ドライバーによって管理されるためは、ビデオのミニポート ドライバー ライター必要割り込みオブジェクトに関する詳細情報はありません。

場合、ミニポート ドライバーの[ *HwVidFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff567332)関数は、ビデオ アダプターが割り込みを実際に発生していないこと、またはベクター/レベルのアダプターは、有効な割り込みを特定できないことを検索します。*HwVidFindAdapter*両方を設定する必要があります**InterruptLevel**と**InterruptVector**で、 [**ビデオ\_ポート\_CONFIG\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff570531)構造体をゼロにします。

ときに*HwVidFindAdapter*コントロールを返しますビデオ ポート ドライバーは、ビデオではメンバーの割り込みの構成を確認します\_ポート\_CONFIG\_情報と、どちらもゼロの場合に、割り込みが接続できません。ミニポート ドライバー。 割り込みで 0 にメンバーの構成の両方を明示的に設定*HwVidFindAdapter*を無効にします、 [ *HwVidInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/ff567349)エントリ ポイントであるによって設定されている場合、ミニポート ドライバーの[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff556159)関数。

なお*HwVidInterrupt* nonpaged であるため、ミニポート ドライバーのデバイスの拡張機能にアクセスできます。 ミニポート ドライバーの設計によってない可能性があるデバイスの拡張機能またはデバイスの拡張機能の特定の領域を共有するには、他のドライバー関数の考えられる*HwVidInterrupt*安全にします。

たとえば、ミニポート ドライバーの[ *HwVidStartIO* ](https://msdn.microsoft.com/library/windows/hardware/ff567367) 、アダプターの割り込みは、ときに、関数は、デバイスの拡張機能にアクセスする*HwVidInterrupt*上で実行別のプロセッサと*HwVidInterrupt*デバイス拡張機能にもアクセスできます。 このような状況が発生する場合*HwVidStartIO*呼び出す必要があります[ **VideoPortSynchronizeExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff570372)ドライバーによって提供されると[ *HwVidSynchronizeExecutionCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff567369)関数。

ビデオのミニポート ドライバーは、次の 2 つの規則に従う必要があります。

1.  たびに、ハードウェア、D0 以外の任意の状態で、ミニポート ドライバーとハードウェアが*決して*割り込みを生成します。

2.  ルール 1 のためデバイス ドライバー ISR 必要があります*決して*電源の状態が D3 の場合、割り込みの動作 (が返されます**FALSE**)。

 

 





