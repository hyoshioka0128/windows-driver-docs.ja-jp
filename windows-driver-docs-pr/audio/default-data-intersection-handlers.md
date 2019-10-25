---
title: 既定のデータ交差ハンドラー
description: 既定のデータ交差ハンドラー
ms.assetid: 5c70a6e4-702f-4fd0-bb3e-2cde2955b2ad
keywords:
- データ交差ハンドラー WDK audio、既定値
- 既定のデータ積集合ハンドラー
- 最小データ交差ハンドラー WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe9d764e06dacfe4c2afd01acf701a2919acfc16
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833559"
---
# <a name="default-data-intersection-handlers"></a>既定のデータ交差ハンドラー


## <span id="default_data_intersection_handlers"></span><span id="DEFAULT_DATA_INTERSECTION_HANDLERS"></span>


アダプターの独自のデータの交差ハンドラー (ミニポートドライバーオブジェクトの[**IMiniport::D ataRangeIntersection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-datarangeintersection)ポート) は、実装された状態を\_\_ステータスを返すことによって、データの交差チェックを拒否することがあります。コード. この場合、ポートドライバーの既定のデータ積集合ハンドラーは、アダプターの代わりにチェックを実行します。

アダプタードライバーの最小データ共通部分を実装するには、状態\_\_を返すことによってすべてのデータの交差要求を拒否する**Datarangeintersection**集合メソッドとして実装します。

ポートドライバーの既定のハンドラーの現在の実装は、処理できるデータ範囲の種類によって制限されます。

-   PCM データ形式のみ

-   Mono およびステレオオーディオストリームのみ

PCM またはマルチチャネル形式をサポートするアダプタードライバーでは、ポートドライバーを使用してこれらの形式のデータの共通部分を処理するのではなく、独自のデータの共通部分ハンドラーを実装する必要があります。

また、既定のハンドラーは、 [**KSDATAFORMAT\_DSOUND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_dsound)または[**KSDATAFORMAT\_WAVEFORMATEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)構造体で指定できるオーディオ形式のみをサポートしています。 [**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)構造体を含むどの形式もサポートされていません。たとえば、3つ以上のチャネルを持つ形式のチャネルマスクを指定する場合などです。

2つのデータ範囲の交差部分から共通の形式を選択すると、ポートドライバーの既定のハンドラーによって、各パラメーターの共通部分の最大値が常に選択されます。

-   交差部分が複数の有効なサンプル周波数 (11、22、および 44 kHz など) にまたがっている場合、既定のハンドラーは最も高い頻度を選択します。

-   交差部分が複数の有効なサンプルのビットごとの値 (8、16、および32ビットなど) にまたがっている場合、既定のハンドラーは最大値を取得します。

-   交差部分が mono 形式とステレオ形式の両方にまたがっている場合、既定のハンドラーはステレオを選択します。

既定のハンドラーが使用できない形式を選択した場合、SysAudio がシンク pin を作成しようとしたときに、アダプタードライバーで**Newstream**の呼び出し (例[ **: IMiniportWavePci:: newstream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream)) を失敗させることで形式を拒否するオプションがあります。形式で指定します。 呼び出しが失敗した場合、SysAudio はデータの交差部分の検索を続行しません。 代わりに、アダプターのシンクピンがサポートできる PCM 形式の一覧を検索するまで、KMixer などのシステムフィルターでサポートされている PCM 形式のリストを反復処理することで、接続の作成が試行されます。 リストは、高い品質形式で並べ替えられます。 以前と同様に、アダプターは、これらの形式の**Newstream**呼び出しを失敗させることによって、一覧内の不足している形式を拒否します。

 

 




