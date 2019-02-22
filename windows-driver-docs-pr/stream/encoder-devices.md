---
title: エンコーダーのデバイス
description: エンコーダーのデバイス
ms.assetid: 156b1d6d-c6f6-4ab3-a91e-3124351c6ae5
keywords:
- エンコーダー デバイス WDK AVStream
- AVStream WDK、エンコーダーのデバイス
- 非圧縮データ ストリームの WDK AVStream
- エンコードされたストリーム WDK AVStream
- オーディオ エンコーダー デバイス WDK AVStream
- ビデオ エンコーダー デバイス WDK AVStream
- ソフトウェア ベースのエンコーダー WDK AVStream
- ハードウェア ベースのエンコーダー WDK AVStream
- 統合されたエンコーダー WDK AVStream
- スタンドアロン エンコーダー WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecaf4ff2257f0a6efb9c47d99158fbf2530a4733
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538837"
---
# <a name="encoder-devices"></a>エンコーダーのデバイス





エンコーダーには、非圧縮データ ストリーム (ビデオやオーディオ) を入力として受け取り、MPEG2 などの特定の形式にエンコード、および、エンコードされたストリームを出力するデバイスです。 エンコーダーのデバイスが組み合わせの TV チューナー/キャプチャ アダプターなどの別のデバイスの一部にすることがあります。 または異なる場合があります。 たとえば、エンコーダーを統合するアナログ テレビ チューナー/デコーダーなどキャプチャ デバイスからのデータ ストリームの受信し、エンコードされたストリームを生成し。 スタンドアロン エンコーダーは、圧縮されていないファイルから入力データを受信、データ、および、エンコードされた出力データを処理することがあります。

Microsoft では、DirectX 9.0 以降のオーディオ/ビデオ エンコーダーのハードウェア ベースのデバイスのサポートを提供します。 再頒布可能パッケージの DirectX 9.0 次の Microsoft Windows プラットフォームで提供されています。

-   Windows Media Center Edition 2004

-   Windows Server 2003

-   Windows XP Home および Professional

-   Windows 2000 Professional および Server

-   Windows Millennium Edition

-   Windows 98 Second Edition

オーディオ/ビデオ エンコーダーのデバイスをサポートするには、カーネル ストリーミング フィルター ミニドライバーでマイクロソフトによって定義されたエンコーダーのプロパティのサポートを実装する必要があります。 サポートは、エンコーダーのプロパティを実装することで、既存のストリーム クラスまたは AVStream ミニドライバーに追加可能性があります。 または、(スタンドアロン エンコーダーのいずれか) または統合の 1 つの新しいミニドライバーを作成する場合をお勧め AVStream アーキテクチャは、次のストリーム クラスが廃止され、不要になったサポートされているためです。 使用すること、 [AVStream シミュレートされたハードウェア ドライバーのサンプル (Avshws)](https://go.microsoft.com/fwlink/p/?LinkId=618052)開始点として。 Avshws ドライバーは、DMA 転送のサポートを実装する暗証番号 (pin) を中心とした AVStream 例です。

**注**   、エンコーダー ソフトウェア実装を作成しているかどうかは、フィルターをストリーミング カーネルとして記述しないでください。 代わりに、このようなフィルターは、Microsoft DirectShow フィルターまたは DirectX メディア オブジェクトとして記述する必要があります。 ソフトウェア ベースのエンコーダーの詳細については DirectShow の SDK のトピック「エンコーダー API」を参照してください。

 

クライアント アクセスのエンコーダーの機能によって、 [ **ICodecAPI** ](https://msdn.microsoft.com/library/windows/desktop/dd311953) COM インターフェイスです。 プロパティによって、ドライバーの INF ファイルで KsProxy を公開するインターフェイス、ミニドライバーの実装を指定します。 参照してください[エンコーダーの実装とサポート](encoder-implementation-and-support.md)については、マイクロソフトによって定義されたカーネル プロパティとイベントをストリーミングします。 参照してください[エンコーダーのコード例](encoder-code-examples.md)それらを実装する方法の例についてはします。 参照してください[エンコーダーのインストールと登録](encoder-installation-and-registration.md)エンコーダー フィルターをインストールする方法については、どの COM インターフェイスを KsProxy を公開する必要がありますを指定する方法を含むです。

エンコーダー デバイスは、すべてのデバイスに対応する汎用のロゴの要件に加え、Windows 認定プログラム」の説明に従ってメディアのストリーミングとブロードキャスト要件に準拠する必要があります。

 

 




