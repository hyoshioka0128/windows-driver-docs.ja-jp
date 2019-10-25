---
title: ストリームのカテゴリ
description: ストリームのカテゴリ
ms.assetid: dc2af282-4976-42d8-b07b-13b2a6dfb7d5
keywords:
- ビデオキャプチャ WDK AVStream、ストリームカテゴリ
- ビデオのキャプチャ WDK AVStream、ストリームカテゴリ
- pin の主な目的を特定する
- ストリームカテゴリ WDK ビデオキャプチャ、ストリームカテゴリについて
- Guid WDK ビデオキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6765308ec812d2d513737aa19a22a1b33e158b3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837687"
---
# <a name="stream-categories"></a>ストリームのカテゴリ


Ksk プロキシフィルターでは、いくつかの種類のストリームカテゴリがサポートされています。 次のサブセクションの表では、さまざまな種類のストリームカテゴリと、各カテゴリの種類に関連付けられているデータ形式、およびビデオキャプチャミニドライバーがカテゴリごとに指定する必要がある拡張ヘッダーサイズの値について説明します。

Stream クラス video capture ミニドライバーは、 [**SRB\_GET\_stream\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-stream-info)要求に応答して、ストリームカテゴリとコンテンツ情報を提供します。 ミニドライバーは、 [**HW\_ストリーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_information)構造でサポートされている各ストリームカテゴリに関する情報を返します。

HW\_ストリーム\_情報構造体は**StreamFormatsArray**メンバーで、指定されたストリームカテゴリに対してミニドライバーが提供する一意のデータ形式ごとにエントリがあります。 各**StreamFormatsArray**エントリには、画像の特性 (色の形式、ビットの深さ、トリミング、スケーリング情報など) を含むストリーム形式情報が含まれています。 また、 **StreamFormatsArray**メンバーには、指定されたストリームカテゴリで使用できる形式の範囲が含まれています。

各ビデオストリームカテゴリには、HW\_ストリーム\_情報構造体でストリームを記述するときに使用される、対応する[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)と[**ksk**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))の構造体があります。 ストリームカテゴリに対応する構造体は、次のサブセクションの表に一覧表示されます。

特定のビデオキャプチャストリームの種類のストリームカテゴリ GUID と pin 名 GUID は、通常は同じです。 これらの Guid は、HW\_ストリーム\_情報構造体の**カテゴリ**と**名前**のメンバーにそれぞれ指定されています。 これらの Guid が一致しないのは、特定のストリームカテゴリのフィルターに複数のインスタンスがある場合のみです。 この場合、カテゴリ Guid は一致している必要がありますが、各 pin には一意の pin 名 GUID を割り当てる必要があります。

次のサブセクションには、さまざまなビデオキャプチャストリームのカテゴリに関する情報が含まれています。 ストリームカテゴリの GUID と pin の名前の GUID、およびカテゴリをサポートするために使用する必要がある構造について説明します。 必須のプロパティセットのサポートは、カテゴリごとにも一覧表示されます。 対応するユーザーモードの DirectShow 型情報も、便宜上表示されます。

 

 




