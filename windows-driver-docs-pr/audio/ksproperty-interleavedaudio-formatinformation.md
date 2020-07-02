---
title: KSK プロパティ \_ INTERLEAVEDAUDIO_FORMATINFORMATION
description: KSK プロパティ \_ INTERLEAVEDAUDIO_FORMATINFORMATION プロパティは、ループバックオーディオとキャプチャオーディオのインターリーブに関する追加情報を提供します。
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
ms.openlocfilehash: e41fe6d8f4dd0550d3b74f19d2f129339f484bdf
ms.sourcegitcommit: 7a69c2e0abf91a57407b13a30faf24925f677970
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85829035"
---
# <a name="ksproperty_interleavedaudio_formatinformation"></a>KSK プロパティ \_ INTERLEAVEDAUDIO_FORMATINFORMATION

**Ksk プロパティ \_ INTERLEAVEDAUDIO_FORMATINFORMATION**プロパティは、ループバックオーディオとキャプチャオーディオのインターリーブに関する追加情報を提供します。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

 |取得|オン|Target|プロパティ記述子の型|プロパティ値の型|
|--- |--- |--- |--- |--- |
|はい|いいえ|Pin|[KS_PIN](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)|[INTERLEAVED_AUDIO_FORMAT_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_interleaved_audio_format_information)|

### <a name="return-value"></a>戻り値

 Get の場合、 **Ksk プロパティ \_ INTERLEAVEDAUDIO_FORMATINFORMATION**は[INTERLEAVED_AUDIO_FORMAT_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_interleaved_audio_format_information)構造体を返します。これには、オーディオストリームのループバックオーディオとキャプチャオーディオのインターリーブに関する追加情報が含まれています。

Windows 10 19H1 以降では、KSK プロパティ \_ INTERLEAVEDAUDIO_FORMATINFORMATION プロパティキーを設定する必要があります。これは、[ハードウェア] キーワードを使用して、マイクとループバックオーディオを1つのストリームに結合するシステムで、キーワードのバースト出力で AEC APO を使用するための要件です。 詳細については、「[音声ライセンス認証](voice-activation.md)」を参照してください。

## <a name="remarks"></a>Remarks

このプロパティは、ハードウェアキーワードをスポット留めすることのみを目的としています。また、ループバックオーディオをマイクオーディオに組み込む方法を提供します。 これを行うには、ハードウェアキーワードをインターリーブします。オーディオとループバックオーディオを1つの PCM オーディオストリームにピン留めし、このプロパティを介して、ループバックとマイクのオーディオを含むチャネルを通信します。

このプロパティを使用するサンプル APO を利用できます。 Sysvad サンプルドライバーの一部として GitHub にあり、 *Kwsapo*と呼ばれています。 サンプル APO は、ループバックオーディオを除去するだけで、プライマリマイクオーディオアップストリームのみを提供します。

## <a name="requirements"></a>必要条件

|要件|値|
|--- |--- |
|サポートされている最小のクライアント|Windows 10 バージョン19H1|
|Header|Ksmedia.h|

## <a name="see-also"></a>関連項目

[KSPROPSETID \_ INTERLEAVEDAUDIO](kspropsetid-interleavedaudio.md)

[KS_PIN](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

[INTERLEAVED_AUDIO_FORMAT_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_interleaved_audio_format_information)
