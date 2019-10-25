---
title: KSK プロパティ\_INTERLEAVEDAUDIO_FORMATINFORMATION
description: KSK プロパティ\_INTERLEAVEDAUDIO_FORMATINFORMATION プロパティは、ループバックオーディオとキャプチャオーディオのインターリーブに関する追加情報を提供します。
keywords:
- KSPROPERTY_INTERLEAVEDAUDIO_FORMATINFORMATION オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_INTERLEAVEDAUDIO_FORMATINFORMATION
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 07/11/2019
ms.localizationpriority: medium
ms.openlocfilehash: dbe5bad0c640763188ca6d34ee14bcd590a3f652
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832750"
---
# <a name="ksproperty_interleavedaudio_formatinformation"></a>KSK プロパティ\_INTERLEAVEDAUDIO_FORMATINFORMATION 

**Ksk プロパティ\_INTERLEAVEDAUDIO_FORMATINFORMATION**プロパティは、ループバックオーディオとキャプチャオーディオのインターリーブに関する追加情報を提供します。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

 |[購入]|設定|対象|プロパティ記述子の型|プロパティ値の型|
|--- |--- |--- |--- |--- |
|[はい]|必須ではない|Pin|[KS_PIN](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)|[INTERLEAVED_AUDIO_FORMAT_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_interleaved_audio_format_information)|

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

 Get, **Ksk プロパティ\_INTERLEAVEDAUDIO_FORMATINFORMATION**は、 [INTERLEAVED_AUDIO_FORMAT_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_interleaved_audio_format_information)構造体を返します。これには、ループバックオーディオのインターリーブに関する追加情報が含まれています。オーディオストリーム。 

Windows 10 19H1 以降では、INTERLEAVEDAUDIO_FORMATINFORMATION プロパティキーに KSK\_プロパティを設定する必要があります。これは、マイクとループバックオーディオを1つのストリームに結合して、キーワードバースト出力で AEC APO を使用する順序。 詳細については、「[音声ライセンス認証](voice-activation.md)」を参照してください。


<a name="remarks"></a>注釈
-------

このプロパティは、ハードウェアキーワードをスポット留めすることのみを目的としています。また、ループバックオーディオをマイクオーディオに組み込む方法を提供します。 これを行うには、ハードウェアキーワードをインターリーブします。オーディオとループバックオーディオを1つの PCM オーディオストリームにピン留めし、このプロパティを介して、ループバックとマイクのオーディオを含むチャネルを通信します。

このプロパティを使用するサンプル APO を利用できます。 Sysvad サンプルドライバーの一部として GitHub にあり、 *Kwsapo*と呼ばれています。 サンプル APO は、ループバックオーディオを除去するだけで、プライマリマイクオーディオアップストリームのみを提供します。


<a name="requirements"></a>要件
------------

|||
|--- |--- |
|サポートされている最小のクライアント|Windows 10 バージョン19H1|
|Header|Ksmedia.h|

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目

[KSPROPSETID\_INTERLEAVEDAUDIO](kspropsetid-interleavedaudio.md)

[KS_PIN](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

[INTERLEAVED_AUDIO_FORMAT_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_interleaved_audio_format_information) 