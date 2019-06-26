---
title: ストリームのカテゴリ
description: ストリームのカテゴリ
ms.assetid: dc2af282-4976-42d8-b07b-13b2a6dfb7d5
keywords:
- ビデオ キャプチャ WDK AVStream、ストリームのカテゴリ
- ビデオの WDK AVStream、ストリームのカテゴリのキャプチャ
- 暗証番号 (pin) の主な目的を識別します。
- ストリームのカテゴリについて、ストリーム カテゴリ WDK ビデオのキャプチャします。
- Guid の WDK ビデオのキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6967c6a6103196a62826e0fa2a6db0f1c90f1920
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361048"
---
# <a name="stream-categories"></a>ストリームのカテゴリ


KsProxy フィルターは、ストリームのカテゴリのいくつかの種類をサポートします。 次のサブセクションでは、テーブルには、さまざまな種類のカテゴリのストリームとビデオ キャプチャ ミニドライバーがカテゴリごとに指定する必要があります拡張ヘッダー サイズの値と同様に、カテゴリの各種類に関連付けられたデータ形式について説明します。

Stream クラスのビデオ キャプチャ ミニドライバーへの応答ストリームのカテゴリとコンテンツの情報を提供する、 [ **SRB\_取得\_ストリーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-stream-info)要求。 ミニドライバーは、各ストリームのカテゴリのサポートに関する情報を返します、 [ **HW\_ストリーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_information)構造体。

ハードウェア ベースの\_ストリーム\_情報の構造を**StreamFormatsArray**ミニドライバーは、指定したストリームのカテゴリを提供する各一意のデータ形式のエントリを持つメンバー。 各**StreamFormatsArray**エントリには形式の色ビット深度、トリミング、およびスケール情報などの画像の特徴を含む、ストリームの形式情報が含まれています。 含まれることも、 **StreamFormatsArray**メンバーが指定したストリームのカテゴリの使用可能な形式の範囲。

各ビデオ ストリームのカテゴリがありますが対応する[ **KSDATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)と[ **KSDATARANGE** ](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))するときに使用する構造体ハードウェア ベースのストリームを記述する\_ストリーム\_情報構造体。 ストリームのカテゴリに対応する構造体は、次のサブセクションでは、テーブルに表示されます。

ストリーム カテゴリ GUID と特定のビデオ キャプチャ ストリーム型用の pin 名 GUID は、通常と同じです。 これらの Guid がで指定された、**カテゴリ**と**名前**ハードウェア ベースのメンバー\_ストリーム\_それぞれの情報が構造体します。 これらの Guid が一致していない唯一のケースでは、指定したストリームのカテゴリには、フィルターの 1 つ以上のインスタンスが持っている場合です。 この場合は、カテゴリの Guid が一致する必要がありますが、各ピンに一意の pin 名 GUID を割り当てる必要があります。

次のサブセクションでは、別のビデオ キャプチャ ストリームのカテゴリのそれぞれに関する情報を格納します。 暗証番号 (pin) の名前の GUID とストリーム カテゴリ GUID は、カテゴリをサポートするために使用する必要があります構造体ととおりです。 必要なプロパティ セットのサポートは、カテゴリごとにも表示されます。 対応するユーザー モード DirectShow の型情報は、便宜上も表示されます。

 

 




