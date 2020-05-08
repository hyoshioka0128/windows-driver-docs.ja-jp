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
ms.openlocfilehash: 533152cdd4a852ccbf2fa31e8ba976090e15594c
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925573"
---
# <a name="high-definition-audio-ddi"></a>High Definition Audio DDI


Windows Vista では、オペレーティングシステムの一部として次の2つのドライバーが提供されます。

-   Intel High Definition Audio (HD audio) バスインターフェイスコントローラーを管理するためのバスドライバー。

-   HD オーディオコントローラーに接続されている UAA 準拠のオーディオコーデック (または、場合によっては複数のコーデック) を管理するための[ユニバーサルオーディオアーキテクチャ](universal-audio-architecture.md)(uaa) クラスドライバー。

また、Windows Server 2003 および Windows XP を実行しているシステムについても、同様の HD オーディオバスドライバーと UAA HD オーディオクラスドライバーを開発します。 HD オーディオコントローラーアーキテクチャの詳細については、intel [HD audio](https://www.intel.com/content/www/us/en/standards/intel-standards-and-initiatives.html) web サイトの「Intel High Definition audio Specification」を参照してください。 Microsoft の UAA の概要については、ホワイトペーパー「[ユニバーサルオーディオアーキテクチャ](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn640534(v=vs.85))」 web サイトを参照してください。

Hd オーディオバスドライバーは、hd audio device driver interface (DDI) を実装しています。これは、HD オーディオコントローラーに接続されているハードウェアコーデックとの通信に、カーネルモードのオーディオおよびモデムドライバーが使用します。 HD audio bus ドライバーは、その子に HD Audio DDI を公開します。これは、コーデックを管理するオーディオおよびモデムドライバーのインスタンスです。

Windows Server 2003 および Windows XP で実行されている HD オーディオバスドライバーのバージョンでは、3種類の HD audio DDI がサポートされています。

-   [**Hdaudio\_BUS\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface)構造によって定義される DDI。 この DDI は、Windows Vista の HD Audio DDI と同じです。

-   [**Hdaudio\_\_BUS INTERFACE\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)構造体で定義されている DDI。 この DDI は、Windows Vista 以降のバージョンの Windows で使用できます。

-   [**Hdaudio\_BUS\_\_インターフェイスの bdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)構造によって定義される DDI。 この DDI は、windows XP 以降のバージョンの Windows で使用できます。

3つの DDIs の違いは軽微であり、 [HD AUDIO DDI のバージョンの違い](differences-between-the-hd-audio-ddi-versions.md)について説明しています。

Windows Vista では、HD オーディオバスドライバーは、\_hdaudio bus\_インターフェイスと hdaudio\_bus\_interface\_V2 構造体で定義されている DDI をサポートしています。

Windows Vista、Windows Server 2003、および Windows XP では、UAA クラスドライバーは、HDAUDIO\_BUS\_インターフェイス構造によって定義された DDI を使用して、uaa 準拠のオーディオコーデックを管理します。 また、ハードウェアベンダーは、これらの DDIs のいずれかまたは両方を使用するカスタムデバイスドライバーを作成して、オーディオとモデムのコーデックを管理することもできます。

ハードウェアベンダーは、UAA ハードウェア要件ドキュメント (公開対象) に準拠するようにオーディオコーデックを設計する必要があります。 ベンダーのカスタムオーディオドライバーが存在しない場合、ユーザーは、システムによって提供される UAA HD オーディオクラスドライバーを利用して、UAA 準拠のオーディオコーデックを管理できます。 ただし、オーディオコーデックには、ベンダーのカスタムドライバーを通じてのみアクセスできる独自の機能が含まれている場合があります。

このセクションでは、HD audio DDI の両方のバージョンに関する次の情報について説明します。

-   Intel の HD オーディオアーキテクチャと Microsoft の UAA HD オーディオクラスドライバーの背景について説明します。

-   HD audio DDI の両方のバージョンを使用してオーディオとモデムのコーデックを制御するためのプログラミングガイドライン。

ここでは、以下の内容について説明します。

[HD オーディオと UAA](hd-audio-and-uaa.md)

[HD オーディオ DDI のプログラミング ガイドライン](programming-guidelines.md)

 

 




