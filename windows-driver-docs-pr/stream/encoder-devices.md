---
title: エンコーダー デバイス
description: エンコーダーデバイス
ms.assetid: 156b1d6d-c6f6-4ab3-a91e-3124351c6ae5
keywords:
- エンコーダーデバイス WDK AVStream
- AVStream WDK、エンコーダーデバイス
- 非圧縮データストリーム WDK AVStream
- エンコードされたストリーム WDK AVStream
- オーディオエンコーダーデバイス WDK AVStream
- ビデオエンコーダーデバイス WDK AVStream
- ソフトウェアベースのエンコーダー WDK AVStream
- ハードウェアベースのエンコーダー WDK AVStream
- 統合エンコーダー WDK AVStream
- スタンドアロンエンコーダー WDK AVStream
ms.date: 06/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: c4879b3fee037f88b4c3fb94663d0e012f1b1ee8
ms.sourcegitcommit: b481c9513a9ea7f824ecabd1ae18876548032252
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84879040"
---
# <a name="encoder-devices"></a>エンコーダーデバイス

エンコーダーは、非圧縮データストリーム (ビデオまたはオーディオ) を入力として受信し、ストリームを MPEG2 などの特定の形式にエンコードして、エンコードされたストリームを出力するデバイスです。 エンコーダーデバイスは、組み合わせたテレビチューナー/キャプチャアダプターなど、別のデバイスの一部である場合もあれば、独立している場合もあります。 たとえば、統合エンコーダーは、アナログテレビチューナー/デコーダーなどのキャプチャデバイスからデータストリームを受信し、エンコードされたストリームを生成します。 スタンドアロンエンコーダーは、圧縮されていないファイルから入力データを受け取り、データを処理して、エンコードされたデータを出力する場合があります。

Microsoft では、DirectX 9.0 以降でのハードウェアベースのオーディオ/ビデオエンコーダーデバイスのサポートを提供しています。

オーディオ/ビデオエンコーダーデバイスをサポートするには、カーネルストリーミングフィルターミニドライバーで Microsoft が定義したエンコーダーのプロパティのサポートを実装する必要があります。 エンコーダーのプロパティを実装することによって、既存のストリームクラスまたは AVStream ミニドライバーにサポートを追加できます。 また、新しいミニドライバー (スタンドアロンエンコーダーまたは統合されたエンコーダー用) を作成する場合は、ストリームクラスが互換性のために残されており、サポートされなくなったため、AVStream アーキテクチャに従うことをお勧めします。 Avstream のシミュレートされた[ハードウェアサンプルドライバー (Avshws)](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/avstream-simulated-hardware-sample-driver-avshws/)を出発点として使用することができます。 Avshws ドライバーは、DMA 転送のサポートを実装する、ピン中心の AVStream の例です。

> [!NOTE]
> ソフトウェアによって実装されたエンコーダーを作成する場合は、カーネルストリーミングフィルターとして記述しないでください。 代わりに、このようなフィルターは、Microsoft DirectShow フィルターまたは DirectX Media オブジェクトとして記述する必要があります。 ソフトウェアベースのエンコーダーの詳細については、DirectShow SDK のトピック「エンコーダー API」を参照してください。

クライアントは、 [**ICodecAPI**](https://docs.microsoft.com/previous-versions/ms784893(v%3dvs.85)) COM インターフェイスを使用してエンコーダーの機能にアクセスします。 ミニドライバーが実装するプロパティに応じて、ドライバーの INF ファイルでどのインターフェイスを公開するかを指定します。 Microsoft 定義のカーネルストリーミングのプロパティとイベントの詳細については、「[エンコーダーの実装とサポート](encoder-implementation-and-support.md)」を参照してください。 実装方法の例については、「[エンコーダーコード例](encoder-code-examples.md)」を参照してください。 エンコーダーフィルターをインストールする方法の詳細については、「[エンコーダーのインストールと登録](encoder-installation-and-registration.md)」を参照してください。これには、ksk プロキシで公開する COM インターフェイスを指定する方法も含まれます。

エンコーダーデバイスは、すべてのデバイスに対応する汎用的なロゴの要件に加えて、Windows 認定プログラムに記載されているストリーミングメディアとブロードキャストの要件に準拠している必要があります。
