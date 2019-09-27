---
title: High Definition Audio DDI
description: High Definition Audio DDI
ms.assetid: d471777c-0002-4caa-a06e-c58e449b7678
keywords:
- HD オーディオ
- High Definition Audio (HD audio)
- WDM オーディオドライバー WDK、HD オーディオ
- オーディオドライバー WDK、HD オーディオ
- Intel High Definition Audio 仕様
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 578a3b3c419359223b7be49dfec6a20a349c8716
ms.sourcegitcommit: 8295a2b59212972b0f7457a748cc904b5417ad67
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71319920"
---
# <a name="high-definition-audio-ddi"></a>High Definition Audio DDI


Windows Vista では、オペレーティングシステムの一部として次の2つのドライバーが提供されます。

-   Intel High Definition Audio (HD audio) バスインターフェイスコントローラーを管理するためのバスドライバー。

-   HD オーディオコントローラーに接続されている UAA 準拠のオーディオコーデック (または、場合によっては複数のコーデック) を管理するための[ユニバーサルオーディオアーキテクチャ](universal-audio-architecture.md)(uaa) クラスドライバー。

また、Windows Server 2003 および Windows XP を実行しているシステムについても、同様の HD オーディオバスドライバーと UAA HD オーディオクラスドライバーを開発します。 HD オーディオコントローラーアーキテクチャの詳細については、intel [HD audio](https://go.microsoft.com/fwlink/p/?linkid=42508) web サイトの「Intel High Definition audio Specification」を参照してください。 Microsoft の UAA の概要については、 [audio テクノロジ](https://go.microsoft.com/fwlink/p/?linkid=8751)web サイトの「ユニバーサルオーディオアーキテクチャ」というホワイトペーパーを参照してください。

Hd オーディオバスドライバーは、hd audio device driver interface (DDI) を実装しています。これは、HD オーディオコントローラーに接続されているハードウェアコーデックとの通信に、カーネルモードのオーディオおよびモデムドライバーが使用します。 HD audio bus ドライバーは、その子に HD Audio DDI を公開します。これは、コーデックを管理するオーディオおよびモデムドライバーのインスタンスです。

Windows Server 2003 および Windows XP で実行されている HD オーディオバスドライバーのバージョンでは、3種類の HD audio DDI がサポートされています。

-   [**Hdaudio\_BUS\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface)構造によって定義される DDI。 この DDI は、Windows Vista の HD Audio DDI と同じです。

-   [**Hdaudio\_BUS\_INTERFACEV2構造体で定義されているDDI。\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2) この DDI は、Windows Vista 以降のバージョンの Windows で使用できます。

-   [**Hdaudio\_BUS\_インターフェイスのbdl構造によって定義されるDDI。\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl) この DDI は、windows XP 以降のバージョンの Windows で使用できます。

3つの DDIs の違いは軽微であり、 [HD AUDIO DDI のバージョンの違い](differences-between-the-hd-audio-ddi-versions.md)について説明しています。

Windows Vista では、HD オーディオバスドライバーは、hdaudio\_bus\_インターフェイスと hdaudio\_bus\_interface\_V2 構造体で定義されている DDI をサポートしています。

Windows Vista、windows Server 2003、および windows XP では、uaa クラスドライバーは、hdaudio\_BUS\_インターフェイス構造によって定義された DDI を使用して、uaa 準拠のオーディオコーデックを管理します。 また、ハードウェアベンダーは、これらの DDIs のいずれかまたは両方を使用するカスタムデバイスドライバーを作成して、オーディオとモデムのコーデックを管理することもできます。

ハードウェアベンダーは、UAA ハードウェア要件ドキュメント (公開対象) に準拠するようにオーディオコーデックを設計する必要があります。 ベンダーのカスタムオーディオドライバーが存在しない場合、ユーザーは、システムによって提供される UAA HD オーディオクラスドライバーを利用して、UAA 準拠のオーディオコーデックを管理できます。 ただし、オーディオコーデックには、ベンダーのカスタムドライバーを通じてのみアクセスできる独自の機能が含まれている場合があります。

このセクションでは、HD audio DDI の両方のバージョンに関する次の情報について説明します。

-   Intel の HD オーディオアーキテクチャと Microsoft の UAA HD オーディオクラスドライバーの背景について説明します。

-   HD audio DDI の両方のバージョンを使用してオーディオとモデムのコーデックを制御するためのプログラミングガイドライン。

このセクションの内容:

[HD audio および UAA](hd-audio-and-uaa.md)

[HD audio DDI プログラミングガイドライン](programming-guidelines.md)

 

 




