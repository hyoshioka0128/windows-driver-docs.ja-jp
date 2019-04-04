---
title: KSPROPERTY\_INTERLEAVEDAUDIO_FORMATINFORMATION
description: KSPROPERTY\_INTERLEAVEDAUDIO_FORMATINFORMATION プロパティは、ループバック オーディオとオーディオのキャプチャのインターリーブに関する追加情報を提供します。
keywords:
- KSPROPERTY_INTERLEAVEDAUDIO_FORMATINFORMATION オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_INTERLEAVEDAUDIO_FORMATINFORMATION
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 02/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4d1677ef926b8cdef3fa64933c3b67cabfaf8cb6
ms.sourcegitcommit: 5f4404a7010a6b26530f60144c5ea7cab846feec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2019
ms.locfileid: "56582957"
---
# <a name="kspropertyinterleavedaudioformatinformation"></a>KSPROPERTY\_INTERLEAVEDAUDIO_FORMATINFORMATION 

**KSPROPERTY\_INTERLEAVEDAUDIO_FORMATINFORMATION**プロパティはループバック オーディオとオーディオのキャプチャのインターリーブに関する追加情報を提供します。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

 |取得|Set|移行先|プロパティ記述子の型|プロパティ値の型|
|--- |--- |--- |--- |--- |
|はい|いいえ|Pin|[KS_PIN](https://msdn.microsoft.com/library/windows/hardware/ff566722(v=vs.85).aspx)|[INTERLEAVED_AUDIO_FORMAT_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-interleaved-audio-format-information)|

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

 Get、 **KSPROPERTY\_INTERLEAVEDAUDIO_FORMATINFORMATION**を返します、 [INTERLEAVED_AUDIO_FORMAT_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-interleaved-audio-format-information)に関する追加情報を格納する構造体、ループバック オーディオとオーディオのストリームでのオーディオのキャプチャのインターリーブします。 

Windows 10 以降 19 H 1、設定、KSPROPERTY\_INTERLEAVEDAUDIO_FORMATINFORMATION プロパティのキーが 1 つのストリームに、ハードウェア キーワード Spotter (HW KWS) その結合マイクとループバック オーディオをサポートするシステムの要件キーワードのバースト出力時に、AEC APO を使用するにはします。 詳細については、[音声をアクティブ化](voice-activation.md)を参照してください。


<a name="remarks"></a>コメント
-------

このプロパティは、専用ハードウェア キーワード Spotter pin ですし、ループバックのオーディオ、マイクのオーディオと交互に配置を追加する方法を提供します。 これはハードウェア キーワード Spotter 暗証番号 (pin) オーディオとオーディオのループバックをまとめて 1 つの PCM のオーディオ ストリームをインターリーブし、経由で通信するこのプロパティは、ループバックとマイクのオーディオを含むチャネルを実行します。

サンプル APO では、このプロパティを使用する使用できます。 Sysvad サンプル ドライバーの一部としては GitHub と呼びますが*KWSApo*します。 サンプル APO だけを取り除きループバック オーディオ、のみプライマリ マイク オーディオ アップ ストリームを提供します。


<a name="requirements"></a>必要条件
------------

|||
|--- |--- |
|サポートされている最小のクライアント|Windows 10 のバージョン 1 の 19 H|
|Header|Ksmedia.h|

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。

[KSPROPSETID\_INTERLEAVEDAUDIO](kspropsetid-interleavedaudio.md)

[KS_PIN](https://msdn.microsoft.com/library/windows/hardware/ff566722(v=vs.85).aspx)





