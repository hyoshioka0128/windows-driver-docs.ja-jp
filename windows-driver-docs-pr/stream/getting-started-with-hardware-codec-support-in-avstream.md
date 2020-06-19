---
title: AVStream のハードウェア コーデック サポートの概要
description: AVStream でのハードウェアコーデックのサポートの概要
ms.assetid: f8335285-e74f-4600-aee9-7e2881cb0764
keywords:
- ハードウェアコーデックは、を使用して WDK AVStream をサポートします。
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 077c8225ff1b617a3e742486dad82cc998e3f72a
ms.sourcegitcommit: 8143bb312ead6582b4b3e0ad34b6266dcfd74fb5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84992484"
---
# <a name="getting-started-with-hardware-codec-support-in-avstream"></a>AVStream でのハードウェアコーデックのサポートの概要

Windows 7 以降では、 [windows メディアファンデーション](https://docs.microsoft.com/windows/win32/medfound/media-foundation-programming-guide)は avstream ベースのメディアコンポーネントをユーザーモードのメディアファンデーション変換 (mfts) として表します。

この機能を使用すると、ベンダーは、ハードウェアベースのデコーダー、エンコーダー、ビデオプロセッサを MFTs として提供し、アプリケーションレベルで操作することができます。

AVStream モデルは Windows 7 で変更されていないため、この機能を有効にするために必要なのはミニドライバーにいくつかの追加機能です。

次の図は、トランスコードトポロジを示しています。

![トランスコードトポロジを示す図](images/hw-transcoding.png)

最適なパフォーマンスを得るには、図の一番下の行に表示されるメディア処理を専用のハードウェアで実行する必要があります。 このシナリオでは、専用のトランスコードハードウェアは、セキュリティで保護されたハードウェアエンコーダーデコーダー (熱心) と呼ばれています。 これは、マザーボードのプラグインモジュールとして、またはディスプレイアダプターの統合機能としてパッケージ化することができます。

Windows 7 では引き続きソフトウェアベースの変換がサポートされます。 ただし、システムは CPU ではなく専用のハードウェアでトランスコード処理を実行するため、ソフトウェアベースのソリューションと比較して、ユーザーエクスペリエンスが大幅に向上します。

前の図に示されているように、ユーザーモードのクライアントは、各 MFT で公開されている IMFTransform インターフェイスを使用して、ユーザーモードの変換にアクセスできます。 IMFTransform は、Vista 以降のバージョンの Windows で使用できますが、ハードウェアベースのメディア処理をユーザーモードアプリケーションに公開するメカニズムは、Windows 7 以降でのみ使用できます。

システム指定のデバイスプロキシ (Devproxy) モジュールは、DirectShow streaming モデルの Ksk プロキシと同じ役割を果たします。 ユーザーモードでのカーネルモードと MFT コンポーネントの*Ks.sys*間での devproxy ブローカーの通信。

結果として得られるハードウェアメディア処理機能は、デバイスプロキシ MFT と呼ばれます。 このメカニズムを活用するために、AVStream ミニドライバーは次のことを行う必要があります。

- AVStream ミニドライバーの一部である個々の KS フィルターとして変換関数を公開します。 たとえば、デバイスにデコード、エンコード、およびビデオ処理機能がある場合、これらの関数は3つの異なる KS フィルターとして表す必要があります。

  - **エンコーダー**: 圧縮されていない形式から圧縮形式に変換するために使用します。

  - **デコーダー**: 圧縮形式から圧縮されていない形式に変換するために使用します。この形式には、NV12 を含める必要があります。

  - **ビデオプロセッサ**: スケーリング、インターレース/インターレース解除、および書式変換を実行するために使用されます。 デコーダーまたはエンコーダーフィルターにビデオ処理サポートを含めないでください。

    Microsoft では、ベンダーがハードウェアベースのスケーリングサポートを提供することを強くお勧めします。 ただし、ハードウェアベースのスケーリングのサポートを提供しない場合は、システムによって提供されるビデオ処理 MFT を使用して、スケーリング操作を低レベルのパフォーマンスで実行できます。 ハードウェアベースのスケーリングをサポートしていない場合は、メディアファンデーショントポロジビルダーによって、システムによって提供されるスケーリング MFT がトポロジに自動的に挿入されます。

- Windows 7 以降のバージョンの Windows で利用可能な次のいずれかの KS カテゴリの下に、メディア処理 KS フィルターを登録します。

  - [**KSMFT \_ カテゴリ \_ ビデオ \_ デコーダー**](https://docs.microsoft.com/windows-hardware/drivers/install/ksmft-category-video-decoder)

  - [**KSMFT \_ カテゴリ \_ ビデオ \_ エンコーダー**](https://docs.microsoft.com/windows-hardware/drivers/install/ksmft-category-video-encoder)

  - [**KSMFT \_ カテゴリ \_ ビデオ \_ プロセッサ**](https://docs.microsoft.com/windows-hardware/drivers/install/ksmft-category-video-processor)

  - [**KSMFT \_ カテゴリ \_ オーディオ \_ デコーダー**](https://docs.microsoft.com/windows-hardware/drivers/install/ksmft-category-audio-decoder)

  - [**KSMFT \_ カテゴリ \_ オーディオ \_ エンコーダー**](https://docs.microsoft.com/windows-hardware/drivers/install/ksmft-category-audio-encoder)

  さらに、次のカテゴリは、他のトランスコードシナリオで使用するためにも定義されています。

  - [**KSMFT \_ カテゴリの \_ ビデオ \_ 効果**](https://docs.microsoft.com/windows-hardware/drivers/install/ksmft-category-video-effect)

  - [**KSMFT \_ カテゴリ \_ マルチプレクサー**](https://docs.microsoft.com/windows-hardware/drivers/install/ksmft-category-multiplexer)

  - [**KSMFT \_ カテゴリ \_ デマルチプレクサー**](https://docs.microsoft.com/windows-hardware/drivers/install/ksmft-category-demultiplexer)

  - [**KSMFT \_ カテゴリの \_ オーディオ \_ 効果**](https://docs.microsoft.com/windows-hardware/drivers/install/ksmft-category-audio-effect)

  - [**KSMFT \_ カテゴリ \_ OTHER**](https://docs.microsoft.com/windows-hardware/drivers/install/ksmft-category-other)

- これで、Media foundation アプリケーションは、以前に説明したカテゴリを使用して、 [Mftenumex](https://docs.microsoft.com/windows/win32/api/mfapi/nf-mfapi-mftenumex)関数を使用して、mfts として登録されているデバイスを列挙できます。
