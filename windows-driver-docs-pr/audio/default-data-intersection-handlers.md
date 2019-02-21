---
title: 既定の交差部分のデータ ハンドラー
description: 既定の交差部分のデータ ハンドラー
ms.assetid: 5c70a6e4-702f-4fd0-bb3e-2cde2955b2ad
keywords:
- 交差部分のデータ ハンドラー WDK のオーディオ、既定値
- 既定の交差部分のデータ ハンドラー
- 最小限のデータの積集合ハンドラー WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aee3aeb9c615367bffd158854158373c757320e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532118"
---
# <a name="default-data-intersection-handlers"></a>既定の交差部分のデータ ハンドラー


## <span id="default_data_intersection_handlers"></span><span id="DEFAULT_DATA_INTERSECTION_HANDLERS"></span>


アダプターの独自のデータの積集合のハンドラー (ミニポート ドライバー オブジェクトの[ **IMiniport::DataRangeIntersection** ](https://msdn.microsoft.com/library/windows/hardware/ff536764)メソッド) を返すことによってデータ交差チェックを実行することができますを拒否しますステータス\_いない\_実装されている状態コード。 ここでは、ポート ドライバーの既定の交差部分のデータ ハンドラーは、アダプターに代わって、チェックを実行します。

最小限のデータの積集合のハンドラーを実装するには、アダプターのドライバーとして、 **DataRangeIntersection**状態を返すことによってデータの積集合のすべての要求を拒否したメソッド\_いない\_実装されていません。

ポート ドライバーの既定のハンドラーの現在の実装を処理できるデータ範囲の種類が制限されています。

-   PCM のデータ形式のみ

-   Mono とステレオ オーディオ ストリームのみ

PCM 以外またはマルチ チャネルの形式をサポートするアダプター ドライバーは、これらの形式のデータの交差部分を処理するためにポート ドライバーではなく独自のデータの積集合ハンドラーを実装する必要があります。

さらに、既定のハンドラーがで指定できるオーディオ形式のみをサポートする[ **KSDATAFORMAT\_DSOUND** ](https://msdn.microsoft.com/library/windows/hardware/ff537094)または[ **KSDATAFORMAT\_WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff537095)構造体。 任意の形式を含むことはできません、 [ **WAVEFORMATEXTENSIBLE** ](https://msdn.microsoft.com/library/windows/hardware/ff538802)に必要なたとえば、3 つ以上のチャネルを形式チャネル マスクを指定する構造体。

2 つのデータ範囲の交差部分から一般的な形式を選択するときにポート ドライバーの既定のハンドラーは常に積集合の各パラメーターの領域での最も大きい値を選択します。

-   交差部分が 1 つ以上の有効な頻度のサンプルにまたがるかどうか、既定のハンドラーは最高周波数を取得 (11、22、および例については、44 kHz)。

-   積集合は、1 つ以上の有効なサンプルあたりのビット値 (8、16、32 ビット、たとえば) にまたがっている場合、既定のハンドラーは、最大値を取得します。

-   Mono とステレオの両方の形式の交差部分にまたがっている場合、既定のハンドラーは、ステレオを取得します。

アダプター ドライバーが失敗したことで、形式を拒否するオプションで、既定のハンドラーが十分でない形式を選択した場合、 **NewStream**呼び出し (たとえばを参照してください[ **IMiniportWavePci::NewStream** ](https://msdn.microsoft.com/library/windows/hardware/ff536735)) SysAudio が形式でシンク暗証番号 (pin) を作成しようとしたとき。 呼び出しが失敗した場合、SysAudio にはデータの交差部分を探しては続行されません。 代わりに、アダプターのシンクの暗証番号 (pin) もサポートするものが見つかるまで KMixer などのシステムのフィルターでサポートされている PCM 形式のリストを反復処理する接続を作成することを試みます。 一覧より高い品質の形式に並んでいます。 失敗したことで、アダプターが不十分な形式の一覧でを拒否する前に、 **NewStream**それらの形式を呼び出します。

 

 




