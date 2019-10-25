---
title: V4 プリンター ドライバー レンダリング アーキテクチャ
description: V4 プリンタードライバーモデルのレンダリングアーキテクチャは、XPSDrv アーキテクチャと同じです。
ms.assetid: 132BB5D5-426C-4449-8562-B5E43E331858
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0097f44af4762f9c2f068e5040edd2b84d74acf9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843612"
---
# <a name="v4-printer-driver-rendering-architecture"></a>V4 プリンター ドライバー レンダリング アーキテクチャ


V4 プリンタードライバーモデルのレンダリングアーキテクチャは XPSDrv アーキテクチャと同じであり、XPS フィルターパイプラインは、以前のバージョンの Windows で使用されていたのと同じ設計に従っており、注目すべきいくつかの追加点があります。

## <a name="rendering-architecture-diagram"></a>レンダリングアーキテクチャの図


次の図は、v4 プリンタードライバーのレンダリングアーキテクチャの選択肢を示しています。

![v4 プリンタードライバーのレンダリングアーキテクチャの選択肢](images/v4xpsdrvarch.png)

次の段落では、前の図の IHV フィルターの役割について説明します。また、このレンダリングアーキテクチャで動作する機能を開発するためのガイドラインも提供します。

## <a name="print-filter-pipeline-configuration-file"></a>印刷フィルターパイプライン構成ファイル


印刷フィルターパイプライン構成ファイルは、形式が変更されていません。 推奨される名前付け規則: vv&lt;PDL&gt;-pipelineconfig です。ここで、vv は製造元コードのプレースホルダーです。 Fapcl6-pipelineconfig の例。 XPS を印刷する Windows デスクトップアプリケーションとの互換性を確保するには、すべての印刷フィルターパイプライン構成ファイルを– pipelineconfig で終わらせる必要があります。

## <a name="ihv-rendering-filter"></a>IHV レンダリングフィルター


このフィルターは、XPS からデバイスの PDL 出力へのレンダリングを完了します。 必要に応じて、XPS ラスタライズサービスまたはサードパーティの RIP を使用できます。 レンダリングフィルターをデザインするためのガイドラインを次に示します。

**推奨される入力の種類:** IXpsDocumentProvider。
シリアル化の手順は、レンダリングプロセスを通じて多くの点で回避されるため、IXpsDocumentProvider インターフェイスを使用する方がストリームインターフェイスを使用するよりも高速です。

**推奨される出力の種類:** IPrintWriteStream.
このフィルターが完了したら、デバイスの PDL をストリームとして出力する必要があります。

**推奨される名前付け規則:** Vv&lt;PDL&gt;を使用します。
ここで、vv は製造元コードのプレースホルダーです。 例: Fabrikam が提供する PostScript レンダラー用の faps .dll。

XPS を PDL として使用できるデバイスは、レンダリングフィルターなしでサポートされる場合があります。 ただし、一部のデバイスでは、Microsoft 標準 UI で適切に動作しない PrintTickets が必要になる場合があります。 このような場合は、XPS レンダリングフィルターでデバイスと互換性のある PrintTicket に変換することをお勧めします。 これにより、標準 UI およびデバイスとの互換性が最大限に保たれます。

## <a name="ihv-feature-filter"></a>IHV 機能フィルター


IHV 機能フィルターを使用すると、N-up、ウォーターマーク、ページの並べ替えなどの機能を処理できます。 機能フィルターを使用すると、基になる PDL のレンダリングを変更せずに、ドライバーに機能を追加できます。 このような機能フィルターを設計するためのガイドラインを次に示します。

**推奨される入力の種類:** IXpsDocumentProvider。

**推奨される出力の種類:** IXpsDocumentConsumer。

複数の IHV 機能フィルターを使用している製造元については、これらのフィルターを別々の論理フィルターと同じ DLL に実装することをお勧めします。 これにより、コード共有が促進され、印刷中の作業セット全体が減少します。

## <a name="color-management"></a>色の管理


V4 印刷ドライバーでは、カラー管理がサポートされています。 ドライバーには、 [Windows カラーシステム](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)(WCS) 準拠のカラープロファイルまたは International color コンソーシアム (ICC) カラープロファイルが含まれている必要があります。 V4 印刷ドライバーでは、デバイス固有のカラーテーブルに対してドライバープロパティバッグを使用することもできます。

## <a name="related-topics"></a>関連トピック
[V4 プリンタードライバーのレンダリング](v4-driver-rendering.md)  
[Windows カラーシステム](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)  



