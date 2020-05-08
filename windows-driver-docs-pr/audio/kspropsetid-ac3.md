---
title: KSPROPSETID\_AC3
description: KSPROPSETID\_AC3
ms.assetid: 172d8ed8-2dd3-438d-8dc6-f4f1bb128811
keywords:
- KSPROPSETID_AC3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebf120c907b890d06b8747bb78578b280b42fc0c
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925549"
---
# <a name="kspropsetid_ac3"></a>KSPROPSETID\_AC3


## <span id="ddk_kspropsetid_ac3_ks"></span><span id="DDK_KSPROPSETID_AC3_KS"></span>


プロパティ`KSPROPSETID_AC3`セットは、オーディオデバイスドライバーの AC 3 デコード機能とエンコード機能を公開します。

AC 3 形式をサポートするオーディオドライバーでは、AC 3 デコーダー/エンコーダーの機能を制御するためのさまざまなプロパティを公開できます。 さらに、ストリームのプロパティを照会して、AC 3 でエンコードされたオーディオの特性を確認できます。

オーディオハードウェアが特定の機能をサポートしていない場合、そのハードウェアのドライバーは get と set プロパティの呼び出しに失敗し、指定された関数を実行する別の方法を検索する必要があることを上位層ドライバーに通知します。 たとえば、ダイナミックレンジ圧縮がサポートされていないデコーダーのドライバーは、その機能に対する呼び出しを失敗させる必要があります。そのため、AC 3 デコーダーの後のストリームに圧縮を挿入する必要があることが上位レイヤーで認識されるようになります。

AC 3 圧縮の詳細については、 [Dolby 研究所](https://www.dolby.com/us/en/index.html)web サイトの「ac 3 仕様」を参照してください。 この仕様には、 *Digital Audio Compression Standard (AC-3)* というタイトルが付いています。

このセット内のプロパティ項目は、KSPROPERTY\_AC3 列挙値によって指定されます。

KSPROPSETID\_AC3 プロパティセットには、次のプロパティが含まれています。

[**KSK プロパティ\_AC3\_代替\_オーディオ**](ksproperty-ac3-alternate-audio.md)

[**KSK プロパティ\_AC3\_ビット\_ストリーム\_モード**](ksproperty-ac3-bit-stream-mode.md)

[**KSK プロパティ\_AC3\_ダイアログ\_レベル**](ksproperty-ac3-dialogue-level.md)

[**KSK プロパティ\_の\_AC3 ダウンミックス**](ksproperty-ac3-downmix.md)

[**KSK プロパティ\_AC3\_エラー\_CONCEALMENT**](ksproperty-ac3-error-concealment.md)

[**KSK プロパティ\_AC3\_言語\_コード**](ksproperty-ac3-language-code.md)

[**KSK プロパティ\_AC3\_ルーム\_の種類**](ksproperty-ac3-room-type.md)

 

 





