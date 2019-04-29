---
title: High Definition Audio DDI
description: High Definition Audio DDI
ms.assetid: d471777c-0002-4caa-a06e-c58e449b7678
keywords:
- HD オーディオ
- 高精細 (HD) オーディオ
- WDM オーディオ ドライバー WDK、HD オーディオ
- オーディオ ドライバー WDK、HD オーディオ
- Intel の高解像度オーディオ仕様
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94a6efb692b2b3697196b953f3e8c0faa4fe32c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333530"
---
# <a name="high-definition-audio-ddi"></a>High Definition Audio DDI


Windows Vista では、Microsoft はオペレーティング システムの一部として次の 2 つのドライバーを提供します。

-   Intel の高解像度オーディオ (HD オーディオ) バス インターフェイス コント ローラーを管理するためのバス ドライバー。

-   A[ユニバーサル オーディオ アーキテクチャ](universal-audio-architecture.md)UAA 準拠のオーディオ コーデック (または複数の可能性がある 1 つのコーデック) を管理するため (UAA) クラス ドライバー HD オーディオ コント ローラーに接続されています。

Microsoft も、開発と同様の HD オーディオ バス ドライバーと Windows Server 2003、および Windows XP を実行するシステムの UAA HD オーディオ クラス ドライバーをします。 HD オーディオ コント ローラーのアーキテクチャについてで Intel 高定義オーディオ仕様を参照して、 [Intel HD オーディオ](https://go.microsoft.com/fwlink/p/?linkid=42508)web サイト。 概要については microsoft の UAA、ホワイト ペーパー「ユニバーサル オーディオ アーキテクチャを参照してください、[オーディオ テクノロジ](https://go.microsoft.com/fwlink/p/?linkid=8751)web サイト。

HD オーディオ バス ドライバーでは、オーディオとモデムのカーネル モード ドライバーが HD オーディオ コント ローラーに接続されているハードウェアのコーデックとの通信に使用する HD オーディオ デバイス ドライバー インターフェイス (DDI) を実装します。 HD オーディオ バス ドライバーでは、その子では、オーディオとモデムのドライバー、コーデックを管理するのインスタンスに HD オーディオ DDI を公開します。

Windows Server 2003 および Windows XP で実行されている HD オーディオ バス ドライバーのバージョンには、HD オーディオ DDI の 3 つのバリエーションがサポートされています。

-   定義されている DDI、 [ **HDAUDIO\_BUS\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff536413)構造体。 この DDI は、Windows Vista では、HD オーディオ DDI と同じです。

-   定義されている DDI、 [ **HDAUDIO\_BUS\_インターフェイス\_V2** ](https://msdn.microsoft.com/library/windows/hardware/ff536418)構造体。 この DDI では、Windows Vista 以降のバージョンの Windows で使用できます。

-   定義されている DDI、 [ **HDAUDIO\_BUS\_インターフェイス\_BDL** ](https://msdn.microsoft.com/library/windows/hardware/ff536416)構造体。 この DDI では、Windows XP 以降のバージョンの Windows で使用できます。

3 つの Ddi 間の相違点はマイナーとは、後ほど[の相違点の間、HD オーディオ DDI バージョン](differences-between-the-hd-audio-ddi-versions.md)します。

Windows Vista では、HD オーディオ バス ドライバーは、HDAUDIO で定義されている DDI をサポートしています。\_BUS\_インターフェイスと、HDAUDIO\_BUS\_インターフェイス\_V2 構造体。

UAA クラス ドライバーでは、Windows Vista、Windows Server 2003 および Windows XP、HDAUDIO によって定義された DDI を使用して\_BUS\_UAA 準拠のオーディオ コーデックを管理するインターフェイス構造体。 さらに、ハードウェア ベンダーは、これら Ddi の一方または両方を使用して、オーディオとモデムのコーデックを管理するカスタムのデバイス ドライバーを作成できます。

ハードウェア ベンダーには、(パブリッシュ) する UAA ハードウェア要件のドキュメントに準拠するように、オーディオ コーデックを設計する必要があります。 仕入先からカスタム オーディオ ドライバーがない場合、ユーザーが、UAA 準拠のオーディオ コーデックを管理するシステム提供の UAA HD オーディオ クラス ドライバーで利用できます。 ただし、オーディオ コーデックには、仕入先のカスタム ドライバーを介してのみアクセス可能である専用の機能が含まれます。

このセクションでは、HD オーディオ DDI の両方のバージョンは、次の情報について説明します。

-   Intel の HD オーディオ アーキテクチャと Microsoft の UAA HD オーディオ クラス ドライバーの背景について説明します。

-   HD オーディオ DDI の両方のバージョンを使用して、オーディオとモデムのコーデックを制御するためのプログラミング ガイドライン。

このセクションの内容:

[HD オーディオおよび UAA](hd-audio-and-uaa.md)

[プログラミング ガイドライン](programming-guidelines.md)

 

 




