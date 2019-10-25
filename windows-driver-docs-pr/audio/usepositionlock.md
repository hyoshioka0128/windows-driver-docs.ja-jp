---
title: UsePositionLock
description: UsePositionLock レジストリ値は、PortCls がその i/o をシリアル化する方法を変更します。
ms.assetid: AD5AF873-4129-4C82-B251-0469CF6149E9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 986e8e26c7edf29d37314f629c0c385a0ae38749
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830000"
---
# <a name="usepositionlock"></a>UsePositionLock


*Usepositionlock*レジストリ値は、PortCls がその i/o をシリアル化する方法を変更します。 この設定を有効にすると、portcls がシリアル化に使用するグローバルデバイスロックに対して、オーディオドライバーの異常が発生した場合に役立ちます。 *Usepositionlock*が有効になっている場合、下記のコールバックと他のプロパティコールバックの間にシリアル化が適用されるのは、オーディオドライバーによって異なります。 このフラグは、既定では有効になっていません。 有効にする前に、ドライバーのコールバック間の競合状態を確認してください。

次の INF 設定を使用して、この動作を有効にします。

```inf
 
[MyAudioDevice.AddReg]
HKR, DispatchSettings, UsePositionLock, 3, 01, 00, 00, 00
```

この INF 設定によって、次のレジストリ値が作成されます。 {4d36e96c-e325-11ce-bfc1-08002be10318} のメディア GUID と、オーディオデバイスの&gt;\#&lt;インスタンスは、レジストリエントリのパスで使用されます。

```text
\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4d36e96c-e325-11ce-bfc1-08002be10318}\<instance#>\DispatchSettings\UsePositionLock 
```

この値が1以上に設定されている場合、portcls はストリーミング位置ロックを使用して、以下に示すコールバックをシリアル化します。 この値が存在しない場合、または0に設定されている場合、既定の動作ではグローバルデバイスロックが使用されます。 この値は、デバイスが初めて追加されたときに読み取られます。

*Usepositionlock*設定は、wavert およびトポロジフィルターでのみサポートされています。 Portcls は、デバイスの追加時にこのレジストリ値を読み取ります。この設定は、機能デバイスオブジェクト (FDO) が削除されるまで保持されます。

Portcls がこのフラグがオンになっていることを検出すると、グローバルデバイスロックを使用して次のプロパティをシリアル化しません。

-   {KSPROPSETID\_RtAudio、 [**Ksk プロパティ\_rtaudio\_GETREADPACKET**](ksproperty-rtaudio-getreadpacket.md)}

-   {KSPROPSETID\_RtAudio、 [**Ksk プロパティ\_rtaudio\_SETWRITEPACKET**](ksproperty-rtaudio-setwritepacket.md)}

-   {KSPROPSETID\_RtAudio、 [**Ksk プロパティ\_rtaudio\_PRESENTATION\_POSITION**](ksproperty-rtaudio-presentation-position.md)}

-   {KSPROPSETID\_RtAudio、 [**Ksk プロパティ\_rtaudio\_PACKETCOUNT**](ksproperty-rtaudio-packetcount.md)}

-   {KSPROPSETID\_Audio、[**Ksk プロパティ\_オーディオ\_POSITION**](ksproperty-audio-position.md)}

-   {KSPROPSETID\_Audio、 [**Ksk プロパティ\_オーディオ\_POSITIONEX**](ksproperty-audio-positionex.md)}

これは、次のミニポートのコールバックが、他のプロパティ要求 (set state 要求を含む) でシリアル化されないことを意味します。

-   [**IMiniportWaveRTInputStream:: GetReadPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertinputstream-getreadpacket)

-   [**IMiniportWaveRTOutputStream:: SetWritePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertoutputstream-setwritepacket)

-   [**IMiniportWaveRTOutputStream:: Getoutputstreamプレゼンテーションの位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertoutputstream-getoutputstreampresentationposition)

-   [**IMiniportWaveRTOutputStream:: GetPacketCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertoutputstream-getpacketcount)

-   [**IMiniportWaveRTStream::GetPosition**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536749(v=vs.85))

 

 





