---
title: UsePositionLock
description: UsePositionLock レジストリ値は、PortCls が I/O をシリアル化する方法を変更します。
ms.assetid: AD5AF873-4129-4C82-B251-0469CF6149E9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fa3afab0ad8fd70495c57bc1a34bed946f5a27f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578499"
---
# <a name="usepositionlock"></a>UsePositionLock


*UsePositionLock*レジストリ値が PortCls が I/O をシリアル化する方法を変更します。 この設定を有効にすると役立つ可能性があります、オーディオ ドライバー、グローバル デバイスのロックに起因する問題に苦しんで場合その portcls がシリアル化に使用されます。 注意してくださいに*UsePositionLock*が有効にされます (必要な) 場合は、以下の一覧表示されているコールバックとその他のプロパティのコールバックの間でシリアル化を適用するオーディオ ドライバー。 既定では、このフラグが有効になっていません。 オンにする前に、そのことをドライバー、ドライバーのコールバック間で競合状態を確認してください。

この動作を有効にするのにには、次の INF 設定を使用します。

```inf
 
[MyAudioDevice.AddReg]
HKR, DispatchSettings, UsePositionLock, 3, 01, 00, 00, 00
```

この INF 設定は、次のレジストリ値を作成します。 メディア {4d36e96c-e325-11ce-bfc1-08002be10318} の GUID と&lt;インスタンス\#&gt;オーディオ デバイスのレジストリ エントリのパスで使用されます。

```text
\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4d36e96c-e325-11ce-bfc1-08002be10318}\<instance#>\DispatchSettings\UsePositionLock 
```

この値は、1 以上に設定されて、portcls を以下に示すコールバックをシリアル化ストリームの位置のロックを使用します。 表示または 0 に設定しないの場合は、既定の動作は、グローバル デバイスのロックを使用しては。 この値は、読み取り、最初の時間、デバイスが追加されます。

*UsePositionLock* WaveRT 設定のみサポートされ、トポロジをフィルター処理します。 Portcls でこのレジストリ値、デバイス追加時と設定は、保持機能のデバイス オブジェクト (FDO) が削除されるまでを読み取ります。

Portcls では、このフラグがオンにするが検出される場合、シリアル化されませんグローバル デバイスのロックでは、次のプロパティ。

-   {KSPROPSETID\_RtAudio [ **KSPROPERTY\_RTAUDIO\_GETREADPACKET**](ksproperty-rtaudio-getreadpacket.md)}

-   {KSPROPSETID\_RtAudio, [**KSPROPERTY\_RTAUDIO\_SETWRITEPACKET**](ksproperty-rtaudio-setwritepacket.md)}

-   {KSPROPSETID\_RtAudio [ **KSPROPERTY\_RTAUDIO\_プレゼンテーション\_位置**](ksproperty-rtaudio-presentation-position.md)}

-   {KSPROPSETID\_RtAudio [ **KSPROPERTY\_RTAUDIO\_PACKETCOUNT**](ksproperty-rtaudio-packetcount.md)}

-   {KSPROPSETID\_オーディオ、[**KSPROPERTY\_オーディオ\_位置**](ksproperty-audio-position.md)}

-   {KSPROPSETID\_オーディオ、 [ **KSPROPERTY\_オーディオ\_POSITIONEX**](ksproperty-audio-positionex.md)}

つまり、次のミニポートのコールバックは、他のプロパティ要求 (要求の状態の設定を含む) とはシリアル化されません。

-   [**IMiniportWaveRTInputStream::GetReadPacket**](https://msdn.microsoft.com/library/windows/hardware/dn946533)

-   [**IMiniportWaveRTOutputStream::SetWritePacket**](https://msdn.microsoft.com/library/windows/hardware/dn946537)

-   [**IMiniportWaveRTOutputStream::GetOutputStreamPresentationPosition**](https://msdn.microsoft.com/library/windows/hardware/dn946535)

-   [**IMiniportWaveRTOutputStream::GetPacketCount**](https://msdn.microsoft.com/library/windows/hardware/dn946536)

-   [**IMiniportWaveRTStream::GetPosition**](https://msdn.microsoft.com/library/windows/hardware/ff536749)

 

 





