---
title: PROPSETID\_EXT\_トランスポート
description: PROPSETID\_EXT\_トランスポート
ms.assetid: 2e96dec7-43a9-44a4-9636-4ccb5244d5bd
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f62a40a6bfa20f3487e7d5c52afbe751ad97bfb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342168"
---
# <a name="propsetidexttransport"></a>PROPSETID\_EXT\_トランスポート


## <span id="ddk_propsetid_ext_transport_ks"></span><span id="DDK_PROPSETID_EXT_TRANSPORT_KS"></span>


PROPSETID\_EXT\_トランスポートのプロパティ設定のコントロールのデータの転送と外部デバイスの間。

KSPROPERTY\_EXTXPORT 列挙体*ksmedia.h*このセットのプロパティを指定します。

このプロパティを設定は省略可能と外部のビデオ キャプチャ デバイスをサポートするミニドライバーによってのみ実装する必要をサポートします。

[**KSPROPERTY\_EXTXPORT\_機能**](ksproperty-extxport-capabilities.md)

[**KSPROPERTY\_EXTXPORT\_入力\_信号\_モード**](ksproperty-extxport-input-signal-mode.md)

[**KSPROPERTY\_EXTXPORT\_出力\_信号\_モード**](ksproperty-extxport-output-signal-mode.md)

[**KSPROPERTY\_EXTXPORT\_ロード\_中**](ksproperty-extxport-load-medium.md)

[**KSPROPERTY\_EXTXPORT\_MEDIUM\_情報**](ksproperty-extxport-medium-info.md)

[**KSPROPERTY\_EXTXPORT\_状態**](ksproperty-extxport-state.md)

[**KSPROPERTY\_EXTXPORT\_STATE\_NOTIFY**](ksproperty-extxport-state-notify.md)

[**KSPROPERTY\_EXTXPORT\_TIMECODE\_SEARCH**](ksproperty-extxport-timecode-search.md)

[**KSPROPERTY\_EXTXPORT\_ATN\_SEARCH**](ksproperty-extxport-atn-search.md)

[**KSPROPERTY\_EXTXPORT\_RTC\_SEARCH**](ksproperty-extxport-rtc-search.md)

[**KSPROPERTY\_RAW\_AVC\_CMD**](ksproperty-raw-avc-cmd.md)

### <a name="span-iddirectshowinterfacespanspan-iddirectshowinterfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow インターフェイス

DirectShow **IAMExtTransport**インターフェイス (Microsoft Windows SDK の DirectShow のドキュメントを参照してください)。 このセットのプロパティへのアクセスを提供します。 インターフェイスは、多くのメソッドを定義しますが、外部のデバイスのコントロールのサブセットのみが実装されます。

 

 





