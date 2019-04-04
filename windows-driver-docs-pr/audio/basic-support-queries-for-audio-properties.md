---
title: オーディオのプロパティに対する基本的なサポート クエリ
description: オーディオのプロパティに対する基本的なサポート クエリ
ms.assetid: d08b6f86-e4fd-4b2c-bfaa-191bcbac3ff8
keywords:
- WDK、クエリが basic サポートのオーディオのプロパティ
- WDM オーディオ プロパティ WDK、basic のサポート クエリ
- basic - クエリ WDK オーディオをサポート
- WDK オーディオのプロパティの設定
- 有効な範囲の WDK オーディオ
- 範囲値の WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be69fde2d31986b3459dc859b123674dc3f215bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553315"
---
# <a name="basic-support-queries-for-audio-properties"></a>オーディオのプロパティに対する基本的なサポート クエリ


## <span id="basic_support_queries_for_audio_properties"></span><span id="BASIC_SUPPORT_QUERIES_FOR_AUDIO_PROPERTIES"></span>


フィルター、pin、またはノードに対するプロパティの設定要求のデータを指定するときに、プロパティの指定された値の有効なデータ範囲を把握する頻繁に、クライアントが必要です。 範囲には、同じデバイスでデバイスからデバイス、およびノードでも、おそらくは異なります。

一部のプロパティを定義して、プロパティの設定要求は範囲外の値を指定することができますが、ミニポート ドライバーがサイレント モードでサポートされている範囲をこれらの値をクランプ (たとえばを参照してください[ **KSPROPERTY\_オーディオ\_VOLUMELEVEL**](https://msdn.microsoft.com/library/windows/hardware/ff537309))。 同じプロパティに対して後続の get 要求では、値または値で、クライアントが要求のセットで指定する値の固定されたバージョンがあります。 ドライバーの実際の設定を取得します。

ただし、クライアントは、単に、範囲外の値を自動的にクランプするミニポート ドライバーに依存するのではなく、プロパティ値の範囲を把握する必要があります。 たとえば、オーディオ デバイスのボリューム コントロールのスライダーを表示するウィンドウを持つアプリケーションは、スライダーの長さに範囲をマップするために、デバイスのボリュームの範囲を把握する必要があります。

特定のプロパティ、ドライバーのハンドラー ルーチンは、範囲のプロパティの基本サポートの要求に応答の情報を提供できる必要があります (KSPROPERTY\_型\_BASICSUPPORT)。 クライアントはこれには、プロパティ ハンドラーはで構成される basic サポート情報を書き込みます値のバッファーを提供ドライバーに basic サポート プロパティ要求を送信するときに、 [ **KSPROPERTY\_の説明。**](https://msdn.microsoft.com/library/windows/hardware/ff565132)プロパティに固有のデータの後に指定する構造体。 このデータは通常、プロパティに応じて、1 つまたは複数のパラメーター範囲の仕様で構成されます。

一般に、クライアントは、この値のバッファーが事前にどれくらいあります把握していないと、値のサイズを決定するプロパティのハンドラーに 1 つまたは 2 つの準備要求を送信する必要があります。 これらの事前要求の形式が定義されています。 クライアントには、これらの規則に従う basic サポート要求を処理するときにドライバーが想定されます。

-   要求と値のサイズを指定する場合**sizeof**(ULONG) し、プロパティ ハンドラーの値を書き込む必要があります、 **AccessFlags** 、KSPROPERTY のメンバー\_に構造を説明しますULONG サイズの値のバッファー。 ハンドラーの設定、KSPROPERTY\_型\_BASICSUPPORT フラグ ビットの場合は、では、さらに basic サポート プロパティ要求。

-   要求と値のサイズを指定する場合**sizeof**(KSPROPERTY\_説明)、ハンドラーは、KSPROPERTY を記述する必要があります\_データ バッファーの構造を説明します。 ハンドラーのセット、 **DescriptionSize**構造体のサイズと、追加のプロパティに固有の情報のすべてのサイズと等しく、構造体のフィールド ハンドラーには、データ バッファーの次に読み込む構造体。 これは、クライアントは、プロパティの基本サポート情報の格納に割り当てる必要がある値のバッファーのサイズです。

-   要求が、両方の KSPROPERTY を格納するのに十分な大きさである値のサイズを指定する場合\_、ハンドラーが、KSPROPERTY を書き込む必要がありますの説明の構造とプロパティに固有の情報、\_説明の構造体の先頭にバッファー、また、KSPROPERTY の末尾に続くデータ バッファーの一部にプロパティに固有の情報を書き込む必要があります\_構造を定義します。 KSPROPERTY の書き込み中に\_説明構造体、ハンドラーを設定する必要があります、 **DescriptionSize**フィールドをその構造体のサイズ、構造に従ってプロパティに固有の情報のサイズの合計。

要求は、これら 3 つのケースのいずれかに一致しない値のサイズを指定する場合、プロパティ ハンドラーは要求は拒否され、ステータス コードの状態を返します\_バッファー\_すぎます\_小さい。

プロパティに固有の情報をハンドラーが値のバッファーに書き込むには、プロパティ値のデータ範囲を含めることができます。 **MembersSize** KSPROPERTY のメンバー\_MEMBERSHEADER では、データの範囲が含まれるかどうかを示します。

-   **MembersSize**範囲が必要ない場合は 0。 これは、場合は、たとえば、プロパティの値は、BOOL 型の場合です。

-   **MembersSize**が 0 でない場合、KSPROPERTY\_MEMBERSHEADER 構造体の 1 つまたは複数のプロパティ値の範囲の記述子が続きます。

、BOOL 型のプロパティの値の範囲の記述子は必要ありませんので、範囲は、値に暗黙的に限定**TRUE**と**FALSE**します。 ただし、整数型を持つプロパティ値の範囲を指定する範囲の記述子が必要です。

たとえば、basic サポート要求を[ **KSPROPERTY\_オーディオ\_VOLUMELEVEL** ](https://msdn.microsoft.com/library/windows/hardware/ff537309)ボリューム ノードのプロパティ ([**KSNODETYPE\_ボリューム**](https://msdn.microsoft.com/library/windows/hardware/ff537208)) そのノードの最小値と最大のボリュームの設定を取得します。 この場合、クライアントは、次の構造を格納するのに十分な大きさである値のバッファーを割り当てることが必要です。

[**KSPROPERTY\_の説明**](https://msdn.microsoft.com/library/windows/hardware/ff565132)

[**KSPROPERTY\_MEMBERSLIST**](https://msdn.microsoft.com/library/windows/hardware/ff565190)

[**KSPROPERTY\_ステッピング\_長**](https://msdn.microsoft.com/library/windows/hardware/ff565631)

上記の一覧で示されている順序で、バッファー内の隣接する場所には、次の 3 つの構造がまとめられます。 ミニポート ドライバー書き込みますに最小値と最大のボリューム レベルで要求を処理する際、**境界**、KSPROPERTY のメンバー\_ステッピング\_時間構造体します。

範囲の記述子の配列で basic サポート要求の例で図を参照してください。[マルチ チャネルのノードを公開する](exposing-multichannel-nodes.md)します。 Basic サポート プロパティ要求の詳細については、[KS プロパティ](https://msdn.microsoft.com/library/windows/hardware/ff567671)を参照してください。 コード例については、プロパティ ハンドラーの実装を参照してください、[オーディオ ドライバーのサンプル](sample-audio-drivers.md)Microsoft Windows Driver Kit (WDK)。

 

 




