---
title: チューナー規格の検出
description: チューナー規格の検出
ms.assetid: 02923d8f-d8a2-427d-8957-2ffb0273b84a
keywords:
- WDK のビデオ キャプチャを書式設定します。
- テレビ信号の形式の WDK ビデオ キャプチャ
- KSPROPERTY_TUNER_STANDARD_MODE
- 検出のチューナー標準 WDK ビデオのキャプチャします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ab522d1ebec00571ce4db6db2c57ae4f30bc65e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374070"
---
# <a name="detecting-tuner-standards"></a>チューナー規格の検出


**このセクションでは、Microsoft Windows Vista 以降のオペレーティング システムにのみ適用されます。**

TV アプリケーション電子番組ガイド (EPG) 情報またはチャネルのテーブルからテレビ信号の実際の形式を取得するが困難な場合があります。 ビデオ キャプチャ ミニドライバーをサポートする必要があります、 [ **KSPROPERTY\_チューナー\_標準\_モード**](https://msdn.microsoft.com/library/windows/hardware/ff565909)をよりの TV アプリケーションを正確に有効にするプロパティを検出しますテレビ信号の形式です。 KSPROPERTY\_チューナー\_標準\_かどうか、ミニドライバーは、チューナーの標準テレビ信号自体からを識別できますアプリケーションに対してモードを示します。 ミニドライバーは、標準の検出、KSPROPERTY をサポートしている場合\_チューナー\_標準\_モード プロパティは、チューニングの信号から標準のチューナーを自動的に検出するデバイスを設定できます。 後の自動検出モードが設定されており、チューニング デバイス自体への要求を処理できる、 [ **KSPROPERTY\_チューナー\_標準**](https://msdn.microsoft.com/library/windows/hardware/ff565907)プロパティ。

KSPROPERTY をサポートするビデオ キャプチャ ミニドライバー\_チューナー\_標準\_モード プロパティは、チューニングのデバイスをサポートするすべてのアナログ標準を自動的に検出できる必要があります。 ただし、デジタルの標準は、現時点ではオプションです。

アナログ信号でオーディオの標準 (PAL\_B PAL/\_G - NICAM/BTSC) が検出するために最も困難です。 ただし、適切なロジックは、ミニドライバーに埋め込まれている場合、ミニドライバーはもこれらのオーディオの標準を自動的に検出することのようになります。

 

 




