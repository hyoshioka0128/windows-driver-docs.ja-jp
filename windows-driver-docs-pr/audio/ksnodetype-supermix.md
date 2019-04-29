---
title: KSNODETYPE\_SUPERMIX
description: KSNODETYPE\_SUPERMIX
ms.assetid: fae4d315-b599-4226-8f1d-e1757320afb2
keywords:
- KSNODETYPE_SUPERMIX オーディオ デバイス
topic_type:
- apiref
api_name:
- KSNODETYPE_SUPERMIX
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8e3f390c24573021f12367d53711b613e7ce359
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333169"
---
# <a name="ksnodetypesupermix"></a>KSNODETYPE\_SUPERMIX


## <span id="ddk_ksnodetype_supermix_ks"></span><span id="DDK_KSNODETYPE_SUPERMIX_KS"></span>


KSNODETYPE\_SUPERMIX ノードが、supermixer を表します。 Supermixer が 1 つの入力ストリームの*m*チャネルと 1 つの出力ストリームに*n*チャネル。 各出力チャネル、supermixer は各出力チャネルでミックスに追加する入力チャネルのミックス レベルを指定します。 *M*-チャネルの入力ストリームの音声がまたはにダウン混合*n*チャネル。

KSNODETYPE\_SUPERMIX ノードは、次の必須プロパティをサポートする必要があります。

[**KSPROPERTY\_AUDIO\_MIX\_LEVEL\_TABLE**](ksproperty-audio-mix-level-table.md)

[**KSPROPERTY\_オーディオ\_混在\_レベル\_キャップ**](ksproperty-audio-mix-level-caps.md)

 

 





