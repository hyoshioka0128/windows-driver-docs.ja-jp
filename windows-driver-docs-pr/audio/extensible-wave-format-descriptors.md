---
title: 拡張可能な Wave 形式の記述子
description: 拡張可能な Wave 形式の記述子
ms.assetid: b80e651b-fb97-4502-8526-e844425805dc
keywords:
- wave 形式記述子の WDK オーディオ
- wave 形式の記述子
- WDK オーディオの wave 形式タグ
- wave ストリーム WDK オーディオ
- WDK のオーディオデータ形式
- データ形式 WDK オーディオ、wave 形式の記述子
- WDK オーディオ、wave 形式の記述子をフォーマットします
- KSDATAFORMAT 構造体
- WAVEFORMATEXTENSIBLE
- WAVEFORMATEX 構造体
- WDM オーディオデータ形式 WDK
ms.date: 06/30/2020
ms.localizationpriority: medium
ms.openlocfilehash: a8abb89c09fd78287ce21fce145124ef468a9d4f
ms.sourcegitcommit: a260b60c121b25f06e8672afaaa8a3b197b17534
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85839124"
---
# <a name="extensible-wave-format-descriptors"></a>拡張可能な Wave 形式の記述子

次の図は、wave オーディオストリームのデータ形式記述子を示しています。

![wave 形式の記述子を示す図](images/wavefmt.png)

図に示されているように、 [**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)構造体に続く追加の形式情報の量は、データ形式によって異なります。

オーディオシステムでは、次のようないくつかの方法でこの種類のフォーマット記述子を使用します。

- 前の図に示されているような書式記述子は、コールパラメーターとしてミニポートドライバーの**newstream**メソッドに渡されます (たとえば、「 [**IMiniportWaveCyclic:: newstream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclic-newstream)」を参照してください)。

- [**IMiniport::D ataRangeIntersection 部分**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-datarangeintersection)メソッドの*Result の書式*指定パラメーターは、前の図に示されているような書式記述子をメソッドが書き込むバッファーを指します。

- [**Ksk プロパティ \_ ピン \_ dataintersection**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataintersection)プロパティ要求は、前の図に示されているような形式記述子を取得します。

- [**Ksproperty \_ PIN \_ PROPOSEDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-proposedataformat)要求は、前の図に示されているような書式記述子を受け入れます。

- [**KsCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatepin)関数の*Connect* call パラメーターには、同様の形式が使用されます。 このパラメーターは、フォーマット記述子も含むバッファーの先頭にある[**Kspin \_ CONNECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_connect)構造体を指します。 KSPIN CONNECT 構造体の直後にある書式記述子は \_ 、前の図に示されているような KSDATAFORMAT 構造体から始まります。

KSDATAFORMAT 構造体の後に続く書式情報は、 [**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)構造体である必要があります。 WAVEFORMATEXTENSIBLE は、WAVEFORMATEX よりも広い範囲の形式を記述できる WAVEFORMATEX の拡張バージョンです。

WAVEFORMAT は互換性のために残されていますが、どのバージョンの Microsoft Windows でも WDM オーディオサブシステムではサポートされていません。 PCMWAVEFORMAT structure は、互換性のために残されている WAVEFORMAT の拡張バージョンです。

WAVEFORMAT、PCMWAVEFORMAT、WAVEFORMATEX、WAVEFORMATEXTENSIBLE という4つの wave 形式構造は、 **wFormatTag**から始まる5つのメンバーで始まります。 上の図は、これらの4つの構造体が互いに重ねて表示され、同一の構造体の部分を強調表示していることを示しています。

WAVEFORMATEXTENSIBLE**では、wValidBitsPerSample を先頭**に3つのメンバーを追加して WAVEFORMATEX を拡張します。 (**サンプル**は、一部の圧縮形式では、 **wValidBitsPerSample**の代わりに、他のメンバーである**wValidSamplesPerBlock**が使用されている共用体です)。バッファー内の KSDATAFORMAT 構造体の末尾の直後にある**wFormatTag**メンバーは、KSDATAFORMAT に続く形式情報の種類を指定します。

WAVEFORMATEX とは異なり、WAVEFORMATEXTENSIBLE は次の操作を実行できます。

1. サンプルコンテナーのサイズとは別に、サンプルあたりのビット数を指定します。 たとえば、20ビットのサンプルは、3バイトのコンテナー内に左揃えで格納できます。 WAVEFORMATEX はサンプルのコンテナーサイズからサンプルあたりのデータビット数を区別できません。このような形式を明確に記述することはできません。

2. マルチチャネルストリームのオーディオチャネルに特定のスピーカーの場所を割り当てます。 WAVEFORMATEX にはこの機能がないため、mono と (2 チャネル) ステレオストリームのみを適切にサポートできます。

## <a name="legacy-use-of-waveformatex"></a>WAVEFORMATEX の従来の使用

WAVEFORMATEX によって記述されるすべての形式は、WAVEFORMATEXTENSIBLE によって記述することもできます。 WAVEFORMATEX 構造体を WAVEFORMATEXTENSIBLE に変換する方法の詳細については、「[形式タグとサブ形式の Guid 間での変換](converting-between-format-tags-and-subformat-guids.md)」を参照してください。

WAVEFORMATEX は、サンプルサイズが8または16ビットの形式を記述するのに十分ですが、WAVEFORMATEXTENSIBLE は、16ビットを超えるサンプルの有効桁数を持つ形式を適切に記述するために必要です。 2 つの例を挙げます。

- サンプルの有効桁数が24ビットのストリームでは、効率的な処理に32ビットのコンテナーサイズを使用できますが、データを損失することなくストレージの効率を向上させるために24ビットのコンテナーを使用するように変換することができます。

- 24ビットのサンプルデータでストリームを処理する場合、20ビットの精度のみを提供するレンダリングデバイスでは、ディザリングを使用して出力信号の忠実性を向上させることができます。 ただし、ディザリングによって追加の処理時間が必要になります。また、元のストリームの精度が20ビットのみの場合は、追加の処理は必要ありません。

どちらの例でも、シグナル品質を維持しながら、処理とストレージの効率性のバランスを保つことができるのは、サンプルの有効桁数とコンテナーのサイズの両方がわかっている場合のみです。

単純な形式を WAVEFORMATEX または WAVEFORMATEXTENSIBLE 構造体で明確に記述できる場合、オーディオドライバーには、形式を説明するためのいずれかの構造を選択するオプションがあります。 ただし、通常、オーディオドライバーは、8ビットまたは16ビットのサンプルで mono および (2 チャネル) ステレオ PCM 形式を指定するために WAVEFORMATEX を使用しており、一部の古いアプリケーションでは、すべてのオーディオドライバーが WAVEFORMATEX を使用してこれらの形式を指定することを想定しています。

ドライバーが、WAVEFORMATEX または WAVEFORMATEXTENSIBLE 構造体として明確に指定できるオーディオ形式をサポートしている場合、クライアントアプリケーションまたはコンポーネントが構造を指定するために使用する2つの構造体のいずれかに関係なく、ドライバーはその形式を認識する必要があります。 たとえば、オーディオデバイスが 44.1 kHz、16ビット、ステレオ PCM 形式をサポートしている場合、ミニポートドライバーの KSK プロパティ \_ の \_ PROPOSEDATAFORMAT プロパティハンドラーと**newstream**メソッドの実装は、形式が WAVEFORMATEX または WAVEFORMATEXTENSIBLE のいずれの構造として指定されているかどうかに関係なく、その形式を受け入れる必要があります。

フォーマットデータの処理を簡単にするために、通常、ドライバーは WAVEFORMATEXTENSIBLE 構造体を使用して、内部的に形式を表します。 この方法では、入力 WAVEFORMATEX 構造を内部 WAVEFORMATEXTENSIBLE 表現に変換したり、内部 WAVEFORMATEXTENSIBLE 表現を出力 WAVEFORMATEX 構造体に変換したりすることが必要になる場合があります。

WAVEFORMATEXTENSIBLE では、 **dwBitsPerSample**はコンテナーのサイズ、 **wValidBitsPerSample**はサンプルあたりの有効なデータビット数です。 コンテナーは常にメモリにバイト単位で配置され、コンテナーのサイズは8ビットの倍数として指定する必要があります。
