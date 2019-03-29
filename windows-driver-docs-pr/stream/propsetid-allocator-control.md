---
title: PROPSETID\_アロケーター\_コントロール
description: PROPSETID\_アロケーター\_コントロール
ms.assetid: a3e0a5e9-4357-4bc9-ba2a-098f344ed01e
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9ebc2aed40b72029a07e7f06298cfbead9150be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572169"
---
# <a name="propsetidallocatorcontrol"></a>PROPSETID\_アロケーター\_コントロール


## <span id="ddk_propsetid_allocator_control_ks"></span><span id="DDK_PROPSETID_ALLOCATOR_CONTROL_KS"></span>


PROPSETID\_アロケーター\_コントロール プロパティは、コントロールなどのビデオ ポートや Microsoft DirectDraw サーフェスのオーバーレイのサーフェイス上の割り当てを設定します。 割り当て済みの DirectDraw surface の数を制御するやをオーバーレイ Mixer にできないことを示すビデオ デコーダーでビデオのスケーリング可能なデバイスでは、このセットのプロパティを実装する必要があります。 オーバーレイ Mixer では、このセットのプロパティを使用して、Microsoft DirectDraw surface の割り当てとディメンションを制御します。

KSPROPERTY\_アロケーター\_内でコントロールの列挙*ksmedia.h*このセットのプロパティを指定します。

このプロパティ セットのサポートは省略可能で、オーバーレイのサーフェスを使用しているデバイスでのみ実装する必要があります。

[**KSPROPERTY\_アロケーター\_コントロール\_HONOR\_数**](ksproperty-allocator-control-honor-count.md)

[**KSPROPERTY\_アロケーター\_コントロール\_画面\_サイズ**](ksproperty-allocator-control-surface-size.md)

[**KSPROPERTY\_アロケーター\_コントロール\_キャプチャ\_キャップ**](ksproperty-allocator-control-capture-caps.md)

[**KSPROPERTY\_アロケーター\_コントロール\_キャプチャ\_インターリーブ**](ksproperty-allocator-control-capture-interleave.md)

### <a name="span-iddirectshowinterfacespanspan-iddirectshowinterfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow インターフェイス

このプロパティ セットへのアクセスを提供する DirectShow インターフェイスはありません。

 

 





