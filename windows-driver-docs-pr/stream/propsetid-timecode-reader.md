---
title: PROPSETID\_タイムコード\_リーダー
description: PROPSETID\_タイムコード\_リーダー
ms.assetid: 7f115ba5-a6b7-4bae-a562-7e84a98ef420
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52a7a56f06ce0b21d2367c8896c0cd110f2de1ed
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325747"
---
# <a name="propsetidtimecodereader"></a>PROPSETID\_タイムコード\_リーダー


## <span id="ddk_propsetid_timecode_reader_ks"></span><span id="DDK_PROPSETID_TIMECODE_READER_KS"></span>


PROPSETID\_タイムコード\_リーダー プロパティ セットは、外部デバイスからタイムコード情報を取得します。

KSPROPERTY\_でタイムコード列挙*ksmedia.h*このセットのプロパティを指定します。

このプロパティを設定は省略可能と外部のビデオ キャプチャ デバイスをサポートするミニドライバーによってのみ実装する必要をサポートします。

[**KSPROPERTY\_タイムコード\_リーダー**](ksproperty-timecode-reader.md)

[**KSPROPERTY\_ATN\_リーダー**](ksproperty-atn-reader.md)

[**KSPROPERTY\_RTC\_READER**](ksproperty-rtc-reader.md)

### <a name="span-iddirectshowinterfacespanspan-iddirectshowinterfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow インターフェイス

DirectShow **IAMTimecodeReader**インターフェイスには、このセットのプロパティへのアクセスが用意されています (Microsoft Windows SDK の DirectShow のドキュメントを参照してください)。

 

 





