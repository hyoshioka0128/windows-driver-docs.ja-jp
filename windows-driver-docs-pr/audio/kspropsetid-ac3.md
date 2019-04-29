---
title: KSPROPSETID\_AC3
description: KSPROPSETID\_AC3
ms.assetid: 172d8ed8-2dd3-438d-8dc6-f4f1bb128811
keywords:
- KSPROPSETID_AC3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29e14507ab50297e4e77f191c059239e9d250427
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332558"
---
# <a name="kspropsetidac3"></a>KSPROPSETID\_AC3


## <span id="ddk_kspropsetid_ac3_ks"></span><span id="DDK_KSPROPSETID_AC3_KS"></span>


`KSPROPSETID_AC3`プロパティ セットが AC 3 デコードとエンコードされたオーディオ デバイス ドライバーの機能を公開します。

Ac-3 形式をサポートするオーディオ ドライバーには、幅広い ac-3 デコーダーとエンコーダーの機能を制御するためのプロパティを公開できます。 さらに、ストリームのプロパティを照会すると、AC で 3 でエンコードされたオーディオの特性が決まります。

オーディオ ハードウェアが特定の機能をサポートしていない場合、そのハードウェアのドライバーには、指定された関数を実行する別の方法を見つける必要がありますが、上位層のドライバーに通知するために、get および set プロパティの呼び出しは失敗します。 たとえば、ダイナミック レンジ圧縮をサポートしていないデコーダーのドライバーでは上位レイヤーは圧縮方法を次の ac-3 デコーダー ストリームに挿入する必要があることを認識できるようにその機能への呼び出しが失敗する必要があります。

Ac-3 圧縮については、ある ac-3 仕様を参照してください、 [Dolby Laboratories](https://go.microsoft.com/fwlink/p/?linkid=8730) web サイト。 仕様のタイトルは*デジタル オーディオの圧縮標準 (ac-3)* します。

このセット内のプロパティ項目が KSPROPERTY によって指定された\_AC3 列挙値。

KSPROPSETID\_AC3 プロパティ セットには、次のプロパティが含まれています。

[**KSPROPERTY\_AC3\_代替\_オーディオ**](ksproperty-ac3-alternate-audio.md)

[**KSPROPERTY\_AC3\_ビット\_ストリーム\_モード**](ksproperty-ac3-bit-stream-mode.md)

[**KSPROPERTY\_AC3\_ダイアログ\_レベル**](ksproperty-ac3-dialogue-level.md)

[**KSPROPERTY\_AC3\_ミックス ダウン**](ksproperty-ac3-downmix.md)

[**KSPROPERTY\_AC3\_エラー\_の非表示**](ksproperty-ac3-error-concealment.md)

[**KSPROPERTY\_AC3\_言語\_コード**](ksproperty-ac3-language-code.md)

[**KSPROPERTY\_AC3\_ルーム\_型**](ksproperty-ac3-room-type.md)

 

 





