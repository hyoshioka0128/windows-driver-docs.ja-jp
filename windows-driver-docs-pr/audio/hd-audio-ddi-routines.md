---
title: HD オーディオ DDI ルーチン
description: HD オーディオ DDI ルーチン
ms.assetid: 2f360031-39bd-457e-8b64-04b37e21a7fe
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 571394fa686deb866253d5d9712f12de92a81d87
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560906"
---
# <a name="hd-audio-ddi-routines"></a>HD オーディオ DDI ルーチン


説明したよう[の相違点の間、HD オーディオ DDI バージョン](https://msdn.microsoft.com/library/windows/hardware/ff536258)、HD オーディオ DDI の 3 つのバージョンが存在します。 これら 3 つの DDI バージョンがによって定義されている、 [ **HDAUDIO\_BUS\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff536413)、 [ **HDAUDIO\_BUS\_インターフェイス\_V2**](https://msdn.microsoft.com/library/windows/hardware/ff536418)、および[ **HDAUDIO\_BUS\_インターフェイス\_BDL** ](https://msdn.microsoft.com/library/windows/hardware/ff536416)構造体。

DDI の 3 つのバージョンでは、カーネル モードでのみアクセスできます。

各 DDI バージョンでは、HD オーディオ バス コント ローラーを管理するハードウェア リソースへのアクセスを提供します。 これらのリソースには、コーデックには、DMA エンジンには、リンクの帯域幅には、リンク位置レジスタ、ウォール クロックの登録が含まれます。 HD オーディオ バス ドライバーでは、DDI を実装し、その子に DDI を公開します。 子は、DDI を使用して、HD オーディオ コント ローラーに接続されているハードウェアのコーデックを管理するカーネル モード機能のドライバーのインスタンスです。

DDI バージョンへのアクセスを取得するには、関数のドライバーが DDI コンテキスト オブジェクトの HD オーディオ バス ドライバーのクエリを実行する必要があります。 詳細については、次を参照してください[取得、HDAUDIO\_バス\_インターフェイス DDI オブジェクト](https://msdn.microsoft.com/library/windows/hardware/ff537589)、 [、HDAUDIO を取得する\_バス\_インターフェイス\_V2 DDI オブジェクト。](https://msdn.microsoft.com/library/windows/hardware/ff537592)、および[、HDAUDIO を取得する\_BUS\_インターフェイス\_BDL DDI オブジェクト](https://msdn.microsoft.com/library/windows/hardware/ff537586)します。

コンテキスト オブジェクトへのポインターは、3 つの DDI バージョンの各ルーチンは、その最初の呼び出しのパラメーターとして受け取ります。

HDAUDIO\_BUS\_インターフェイス構造体は、次のルーチンを含む DDI を定義します。

[**AllocateCaptureDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536177)

[**AllocateDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536179)

[**AllocateRenderDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536181)

[**ChangeBandwidthAllocation**](https://msdn.microsoft.com/library/windows/hardware/ff536229)

[**FreeDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536391)

[**FreeDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536393)

[**GetDeviceInformation**](https://msdn.microsoft.com/library/windows/hardware/ff536397)

[**GetLinkPositionRegister**](https://msdn.microsoft.com/library/windows/hardware/ff536398)

[**GetResourceInformation**](https://msdn.microsoft.com/library/windows/hardware/ff536399)

[**GetWallClockRegister**](https://msdn.microsoft.com/library/windows/hardware/ff536401)

[**RegisterEventCallback**](https://msdn.microsoft.com/library/windows/hardware/ff537803)

[**SetDmaEngineState**](https://msdn.microsoft.com/library/windows/hardware/ff537889)

[**TransferCodecVerbs**](https://msdn.microsoft.com/library/windows/hardware/ff538596)

[**UnregisterEventCallback**](https://msdn.microsoft.com/library/windows/hardware/ff538663)

HDAUDIO\_BUS\_インターフェイス\_V2 構造体には、Windows Vista および以降のバージョンの Windows、および、次のルーチンを含む DDI を定義します。

[**AllocateCaptureDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536177)

[**AllocateDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536179)

[**AllocateDmaBufferWithNotification**](https://msdn.microsoft.com/library/windows/hardware/ff536180)

[**AllocateRenderDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536181)

[**ChangeBandwidthAllocation**](https://msdn.microsoft.com/library/windows/hardware/ff536229)

[**FreeDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536391)

[**FreeDmaBufferWithNotification**](https://msdn.microsoft.com/library/windows/hardware/ff536392)

[**FreeDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536393)

[**GetDeviceInformation**](https://msdn.microsoft.com/library/windows/hardware/ff536397)

[**GetLinkPositionRegister**](https://msdn.microsoft.com/library/windows/hardware/ff536398)

[**GetResourceInformation**](https://msdn.microsoft.com/library/windows/hardware/ff536399)

[**GetWallClockRegister**](https://msdn.microsoft.com/library/windows/hardware/ff536401)

[**RegisterEventCallback**](https://msdn.microsoft.com/library/windows/hardware/ff537803)

[**RegisterNotificationEvent**](https://msdn.microsoft.com/library/windows/hardware/ff537809)

[**SetDmaEngineState**](https://msdn.microsoft.com/library/windows/hardware/ff537889)

[**TransferCodecVerbs**](https://msdn.microsoft.com/library/windows/hardware/ff538596)

[**UnregisterEventCallback**](https://msdn.microsoft.com/library/windows/hardware/ff538663)

[**UnregisterNotificationEvent**](https://msdn.microsoft.com/library/windows/hardware/ff538669)

HDAUDIO\_BUS\_HD オーディオ DDI のインターフェイスのバージョンが Windows Vista および Windows の以降のバージョンでサポートされています。 さらに、この DDI をサポートしている HD オーディオ バス ドライバーのバージョンは、Windows 2000、Windows XP、および Windows Server 2003 にインストールできます。

HDAUDIO\_BUS\_インターフェイス\_BDL 構造は、次のルーチンを含む DDI を定義します。

[**AllocateCaptureDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536177)

[**AllocateContiguousDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536178)

[**AllocateRenderDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536181)

[**ChangeBandwidthAllocation**](https://msdn.microsoft.com/library/windows/hardware/ff536229)

[**FreeContiguousDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536390)

[**FreeDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536393)

[**GetDeviceInformation**](https://msdn.microsoft.com/library/windows/hardware/ff536397)

[**GetLinkPositionRegister**](https://msdn.microsoft.com/library/windows/hardware/ff536398)

[**GetResourceInformation**](https://msdn.microsoft.com/library/windows/hardware/ff536399)

[**GetWallClockRegister**](https://msdn.microsoft.com/library/windows/hardware/ff536401)

[**RegisterEventCallback**](https://msdn.microsoft.com/library/windows/hardware/ff537803)

[**SetDmaEngineState**](https://msdn.microsoft.com/library/windows/hardware/ff537889)

[**SetupDmaEngineWithBdl**](https://msdn.microsoft.com/library/windows/hardware/ff537894)

[**TransferCodecVerbs**](https://msdn.microsoft.com/library/windows/hardware/ff538596)

[**UnregisterEventCallback**](https://msdn.microsoft.com/library/windows/hardware/ff538663)

HDAUDIO をサポートしている HD オーディオ バス ドライバーのバージョン\_BUS\_インターフェイス\_HD オーディオ DDI の BDL バージョンは、Windows 2000、Windows XP、および Windows Server 2003 にインストールできます。 ただし、Windows Vista にはこの DDI バージョンのサポートはありません。

2 つの Ddi のルーチンのほとんどは、名前と操作の両方で同じです。 ただし、HDAUDIO の一部である次の 2 つルーチン\_BUS\_DDI のバージョンのインターフェイスを HDAUDIO に含まれない\_BUS\_インターフェイス\_BDL バージョン。

[**AllocateDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536179)

[**FreeDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536391)

次に示す 3 つルーチン、HDAUDIO で同様に、\_BUS\_インターフェイス\_DDI の BDL バージョンは、HDAUDIO の一部ではない\_BUS\_インターフェイスのバージョン。

[**AllocateContiguousDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536178)

[**FreeContiguousDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536390)

[**SetupDmaEngineWithBdl**](https://msdn.microsoft.com/library/windows/hardware/ff537894)

このセクションでは、次の DDI ルーチンについて説明します。

[**AllocateCaptureDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536177)

[**AllocateContiguousDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536178)

[**AllocateDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536179)

[**AllocateRenderDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536181)

[**ChangeBandwidthAllocation**](https://msdn.microsoft.com/library/windows/hardware/ff536229)

[**FreeContiguousDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536390)

[**FreeDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536391)

[**FreeDmaEngine**](https://msdn.microsoft.com/library/windows/hardware/ff536393)

[**GetDeviceInformation**](https://msdn.microsoft.com/library/windows/hardware/ff536397)

[**GetLinkPositionRegister**](https://msdn.microsoft.com/library/windows/hardware/ff536398)

[**GetResourceInformation**](https://msdn.microsoft.com/library/windows/hardware/ff536399)

[**GetWallClockRegister**](https://msdn.microsoft.com/library/windows/hardware/ff536401)

[**RegisterEventCallback**](https://msdn.microsoft.com/library/windows/hardware/ff537803)

[**SetDmaEngineState**](https://msdn.microsoft.com/library/windows/hardware/ff537889)

[**SetupDmaEngineWithBdl** ](https://msdn.microsoft.com/library/windows/hardware/ff537894)効果的な[ **PHDAUDIO\_BDL\_ISR**](https://msdn.microsoft.com/library/windows/hardware/mt750609)

[**TransferCodecVerbs**](https://msdn.microsoft.com/library/windows/hardware/ff538596)

[**UnregisterEventCallback**](https://msdn.microsoft.com/library/windows/hardware/ff538663)

上記の一覧には、DDI のいずれかまたは両方のバージョンで表示されるすべてのルーチンが含まれています。

 

 





