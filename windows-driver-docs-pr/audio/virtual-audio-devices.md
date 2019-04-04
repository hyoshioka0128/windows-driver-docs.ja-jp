---
title: 仮想のオーディオ デバイス
description: 仮想のオーディオ デバイスは、レンダリング、オーディオ コンテンツをキャプチャするフィルター グラフを表しています。 システム オーディオ ドライバー (SysAudio) は、使用可能なハードウェアおよびソフトウェア コンポーネントを使用して、ビルドをフィルター グラフを決定します。
ms.assetid: 0f8ddd2d-f852-4b35-8a18-16416081d3c0
keywords:
- WDK 仮想オーディオ デバイス
- SysAudio
- システム オーディオ デバイス WDK
- 仮想デバイスのオーディオ WDK
- オーディオ フィルター グラフを WDK
- WDK のオーディオ、仮想のオーディオ デバイスをグラフでフィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 090b73c229940010c37955529ce65ff3eb1c0aac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537441"
---
# <a name="virtual-audio-devices"></a>仮想のオーディオ デバイス


仮想のオーディオ デバイスは、レンダリング、オーディオ コンテンツをキャプチャするフィルター グラフを表しています。 システム オーディオ ドライバー (SysAudio) は、使用可能なハードウェアおよびソフトウェア コンポーネントを使用して、ビルドをフィルター グラフを決定します。

システム オーディオ ドライバーの詳細については、[SysAudio システム ドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)を参照してください。

## <span id="virtual_audio_devices"></span><span id="VIRTUAL_AUDIO_DEVICES"></span>


SysAudio のクライアントは、DirectSound と[WDMAud システム ドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver)、WDM オーディオ ドライバー、オーディオに固有の Microsoft Windows のマルチ メディア Api の waveIn、waveOut、midiIn、midiOut、ミキサーの間のインターフェイスとして機能し、aux (Microsoft Windows SDK のドキュメントで説明)。

[KsStudio ユーティリティ](ksstudio-utility.md)Windows Driver Kit (WDK) で SysAudio をバイパスし、グラフのフィルターを手動で作成することができるアプリケーションの例に示します。

次の PnP デバイスの列挙 SysAudio はそのクライアントを必要とするさまざまなオーディオ フィルター グラフを作成する方法を決定するために登録されているオーディオ ハードウェアおよびソフトウェア コンポーネントの在庫を受け取ります。

決定した後は、フィルターの一覧は、こと使用可能なハードウェアからをビルドして SysAudio、ソフトウェア コンポーネントは、再生、録音、MIDI 入力/出力、および混合仮想のオーディオ デバイスとしてこれらのグラフを登録しますグラフ化します。 SysAudio 予約レジストリ カテゴリ KSCATEGORY\_オーディオ\_仮想オーディオ デバイス専用のデバイス。 アダプターのドライバーがする必要がありますこのカテゴリで自身を登録していません。

SysAudio クライアントでは、ハードウェアまたはソフトウェア コンポーネントのフィルター ファクトリを仮想デバイスのオーディオ フィルター ファクトリを同様に扱うことができます。 仮想デバイスで特定のピンをインスタンス化するクライアントによって要求されたときに、SysAudio は自動的にグラフを構築し、クライアントに透過的に、グラフのピン留めする内部接続を管理します。 これにより、フィルターの間の通信などのグラフの管理の複雑さを回避、1 つのフィルターとしてフィルター グラフを処理するクライアント。

 

 




