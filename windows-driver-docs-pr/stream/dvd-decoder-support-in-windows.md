---
title: Windows での DVD デコーダーのサポート
description: Windows での DVD デコーダーのサポート
ms.assetid: 3a77b6d1-6095-4cf8-8cd4-2e6d80d171c8
keywords:
- DVD デコーダーミニドライバー WDK、Windows サポート
- デコーダーミニドライバー WDK DVD、Windows サポート
- DVD デコーダーミニドライバー WDK、書き込み
- デコーダーミニドライバー WDK DVD、書き込み
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a56932123c0a3c4e2d9be48635babb056029a26e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843216"
---
# <a name="dvd-decoder-support-in-windows"></a>Windows での DVD デコーダーのサポート





このトピックは、開発者を対象とし**て   ます**。 ソフトウェアデコーダーの一覧など、Windows 用の DVD デコーダーに関する一般的な情報については、Microsoft サポート技術情報の記事 Q306331 「windows[XP および Windows Vista 用の windows Media Player でサポートされているソフトウェアの MPEG-2 dvd デコーダー](https://go.microsoft.com/fwlink/p/?linkid=3100&ID=306331)」を参照してください。

 

DVD デコーダーは、windows 98/Me 以降および Windows 2000 以降でサポートされています。

DVD デコーダーミニドライバーを作成するには、ミニドライバーに、WDK で提供されている*ksk*および*ntddcdvd*ヘッダーファイルを含める必要があります。 ミニドライバーは *、.lib、* *ks*、 *ksguid*.lib、および*dxapi .lib*ライブラリにもリンクする必要があります。

Windows XP では、次のコンポーネントで DVD のデコードと再生がサポートされています。

-   **WDM ストリームクラスドライバー**

    WDM ストリームクラスドライバーは、ストリーミングデータ型と MPEG-2 および AC 3 ハードウェアデコーダーをサポートしています。 詳細については、「 [Streaming ミニドライバー](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)」を参照してください。

Microsoft では、Windows XP で MPEG-2 または AC 3 ソフトウェア/ハードウェアデコーダーのフィルターを提供していない**ことに注意**してください  。 ベンダーは、必要な各 DVD データストリームに対して、DirectShow 互換のソフトウェアデコーダーを提供するか、または、WDM ストリーミングと互換性のある DVD デコーダーミニドライバーを提供して、DVD ハードウェアデコーダーをサポートする必要があります。

 

-   **DVD-ROM クラスドライバー**

    Windows XP では、著作権保護および regionalization 用のコマンドを含む DVD-ROM コマンドセットのサポートが、更新された CD-ROM クラスドライバーによって提供されています。 このクラスドライバーを使用すると、DVD-ROM ドライブからデータセクターを読み取ることができます。

-   **UDF ファイルシステム**

    NT ベースのオペレーティングシステムは、UDF でインストール可能なファイルシステムを提供します。これは、FAT と NTFS に似ています。 このインストール可能なファイルシステムでは、UDF 形式の DVD ディスクがサポートされています。

-   Microsoft **DirectShow**

    DirectShow フィルターおよび関連サポートには、DVD ナビゲーター/スプリッター、video デコーダーミニドライバー for video、サブピクチャおよびオーディオストリーム、line21 デコーダー (クローズドキャプション)、ビデオミキサー、ビデオレンダラー、オーディオなどが含まれます。レンダラ.

    -   DirectShow DVD ナビゲーター/スプリッターフィルター

        Dvd ナビゲーター/スプリッターフィルターは、dvd ムービー、保護者による制限、複数の言語、および DVD 固有のほとんどのデータ構造に組み込まれているプログラミング言語を解釈します。 このフィルターは dvd ストリームを DVD ディスクから直接読み取り、オーディオ、ビデオ、サブピクチャなど、個々のメディアの種類の出力を生成します。 このフィルターは、ストリーム内のコマンドに応答し、すべてのユーザー入力を処理します。

    -   DirectShow プロキシフィルター

        このフィルターは、DirectShow インターフェイスを WDM 接続およびストリーミングアーキテクチャプロパティに変換します。 これにより、オーディオやビデオのデータ型など、ハードウェアでデコードされる各データ型のデバイスオブジェクトが作成されます (つまり、インスタンス化されます)。 このフィルターでは、新しいインターフェイスの展開を可能にするプラグインがサポートされています。

    -   DirectShow Closed-キャプションデコードフィルター

        このフィルターは、DVD ビデオストリーム内のクローズドキャプションデータをテキストイメージに変換します。

    -   DirectShow ビデオポートマネージャーとレンダリングフィルター

        これらのフィルターは、ハードウェアのビデオポートを使用してビデオを再生できるようにし、クローズドキャプションデコーダーの出力ストリームなどの低帯域幅のビデオストリームをブレンドするためのサポートを提供します。

-   Microsoft **DIRECTDRAW HAL と VPE**

専用バスは、MPEG 2 デコーダーからディスプレイカードにデコードされたビデオストリームを転送します。 Microsoft は、DirectDraw ハードウェアアブストラクションレイヤー (HAL) とビデオポート拡張 (VPE) を使用して、ハードウェアでデコードされたビデオをビデオグラフィックス配列 (VGA) に渡すことによって、これらのインターフェイスのソフトウェアをサポートしています。 ソフトウェアデコーダーでは、Accelerated Graphics Port (AGP) バスを使用して、デコードされたビデオを VGA に転送できます。

-   **著作権保護**

    DVD の著作権保護は、ディスク上のセクターを暗号化し、それらのセクターをデコードする前に復号化することによって提供されます。 Microsoft では、DVD ナビゲーター/スプリッターを使用して、ソフトウェアとハードウェアの両方の decrypters をサポートしています。これは、コンピューターのデコーダーと DVD-ROM ドライブの間の認証シーケンスを監視します。 キー交換シーケンスは、DVD デコーダーミニドライバーの入力ピンに送信されるプロパティを使用して実装されます。

DVD 再生には主に次の2つの形式があります。

[ハードウェアベースの DVD デコード](hardware-based-dvd-decoding.md)

[ソフトウェアベースの DVD デコード](software-based-dvd-decoding.md)

次のトピックでは、DVD デコーダーに関連するカーネルストリーミングのプロパティとイベントの概要を示します。

[DVD デコーダー関連の KS プロパティ](dvd-decoder-related-ks-properties.md)

[DVD デコーダー関連の KS イベント](dvd-decoder-related-ks-events.md)

 

 




