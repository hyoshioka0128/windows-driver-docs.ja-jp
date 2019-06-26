---
title: V4 プリンター ドライバー レンダリング アーキテクチャ
description: V4 プリンター ドライバー モデルのレンダリング アーキテクチャでは、XPSDrv アーキテクチャと同じです。
ms.assetid: 132BB5D5-426C-4449-8562-B5E43E331858
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 100d89678075dbca81bcd8e37d195f3fedacef7b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362692"
---
# <a name="v4-printer-driver-rendering-architecture"></a>V4 プリンター ドライバー レンダリング アーキテクチャ


V4 プリンター ドライバー モデルのレンダリング アーキテクチャは XPSDrv のアーキテクチャと同じであり、XPS フィルター パイプラインでは、いくつかの注目すべき追加内容を含む、Windows の以前のバージョンで使用されていた同じデザインもに従います。

## <a name="rendering-architecture-diagram"></a>レンダリング アーキテクチャ図


次の図は、v4 プリンター ドライバーのレンダリング アーキテクチャの選択肢を示します。

![v4 プリンター ドライバーのアーキテクチャの選択肢を表示](images/v4xpsdrvarch.png)

次の段落では、前の図では、IHV フィルターの役割を説明しもこのレンダリング アーキテクチャ内で作業する機能を開発するためのガイドラインを提供します。

## <a name="print-filter-pipeline-configuration-file"></a>印刷フィルター パイプライン構成ファイル


形式では、印刷フィルター パイプライン構成ファイルは変更されません。 名前付け規則を推奨: vv&lt;PDL&gt;-vv が製造元コードのプレース ホルダーを pipelineconfig.xml します。 例 fapcl6-pipelineconfig.xml します。 すべての印刷フィルター パイプラインの構成ファイルが XPS を印刷する Windows デスクトップ アプリケーションとの互換性のために –pipelineconfig.xml で終了する必要があります。

## <a name="ihv-rendering-filter"></a>IHV 表示フィルター


このフィルターは、デバイスの PDL 出力に XPS からレンダリングを完了します。 XPS ラスタライズ サービスまたはサード パーティ製の RIP を使用して、必要に応じて、その可能性があります。 表示フィルター デザインのガイドラインの一部を次に示します。

**入力の種類をお勧めします。** IXpsDocumentProvider します。
IXpsDocumentProvider インターフェイスを使用することは、レンダリング プロセスの点でシリアル化の手順を回避するために、ストリーム インターフェイスを使用するよりも高速です。

**出力の種類をお勧めします。** IPrintWriteStream します。
このフィルターが完了したら、デバイスの PDL ストリームとして出力にする必要があります。

**名前付け規則をお勧めします。** 使用して、vv&lt;PDL&gt;.dll です。
Vv は製造元コードのプレース ホルダーです。 Fabrikam で提供される PostScript レンダラーの例: faps.dll します。

表示フィルターなし PDL として XPS を使用することができるデバイスをサポート可能性があります。 ただし、一部のデバイスでは、Microsoft 標準の UI でうまく動作しない PrintTickets を必要があります。 このような場合、XPS レンダリング フィルター デバイスと互換性のある PrintTicket を変換する必要があることをお勧めします。 これにより、標準の UI とデバイスの最適な互換性です。

## <a name="ihv-feature-filter"></a>IHV 機能フィルター


IHV 機能フィルターには、n-up などの機能の処理、透かし処理、またはページの並べ替えが有効にします。 使用して機能のフィルターは、機能を基になる PDL レンダリングを変更することがなく、ドライバーを追加する便利な方法です。 このような機能フィルター デザインのガイドラインの一部を次に示します。

**入力の種類をお勧めします。** IXpsDocumentProvider します。

**出力の種類をお勧めします。** IXpsDocumentConsumer します。

IHV 機能の複数のフィルターを使用した製造元は、これらのフィルターが別々 の論理フィルターと同じ DLL に実装されるをお勧めします。 これは、コードの共有を促進し、印刷時に設定する全体的な作業を減らすことができます。

## <a name="color-management"></a>色の管理


色の管理は、v4 印刷ドライバーでサポートされます。 ドライバーを含める必要があります[Windows カラー システム](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_print/index)(WCS) 準拠のカラー プロファイルまたは International Color Consortium (ICC) のカラー プロファイル。 V4 印刷ドライバーでは、デバイスに固有のカラー テーブルのドライバーのプロパティ バッグも使用可能性があります。

## <a name="related-topics"></a>関連トピック
[V4 プリンター ドライバーの表示](v4-driver-rendering.md)  
[Windows カラー システム](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_print/index)  



