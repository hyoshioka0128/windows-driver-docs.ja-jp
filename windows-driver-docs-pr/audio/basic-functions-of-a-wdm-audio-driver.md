---
title: WDM オーディオ ドライバーの基本機能
description: WDM オーディオ ドライバーの基本機能
ms.assetid: 88013d17-c28c-4c99-9c43-17532f03bfdd
keywords:
- WDM オーディオ ドライバー WDK、WDM オーディオ ドライバーについて
- オーディオ ドライバー WDK、オーディオ ドライバーについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 729bcad4081e9c24341b7a6511117c1d8a4e15f9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333915"
---
# <a name="basic-functions-of-a-wdm-audio-driver"></a>WDM オーディオ ドライバーの基本機能


## <span id="basic_functions_of_a_wdm_audio_driver"></span><span id="BASIC_FUNCTIONS_OF_A_WDM_AUDIO_DRIVER"></span>


Microsoft Windows Driver Model (WDM) ドライバーは、次の機能を提供します。

-   ドライバーは、すべての種類の入力と出力ストリーム、およびサポートできる各ストリームの種類のインスタンスの数を公開します。 ドライバーは、暗証番号 (pin) ファクトリとファクトリごとにインスタンス化できるピンの数の一連の形式では、この情報を提供します。 たとえば、単純なオーディオ デバイスは、1 つの PCM のオーディオ ストリームを入力して、1 つの PCM のオーディオ ストリームを出力することが。 このデバイスのフィルターには、出力ストリーム--の 2 つの pin ファクトリ - 入力ストリームのいずれかのいずれかが含まれていて、各ピン ファクトリは、ピンが 1 つのインスタンスのみをサポートします。 アダプター カードがこれらのデバイスの 1 つだけ含まれる場合、アダプターのドライバーは、これらの機能とフィルターの 1 つのインスタンスのみを含むフィルター ファクトリを提供します。

-   ドライバーは、1 つまたは複数のプロパティ セットをサポートします。 たとえば、すべてのオーディオ ドライバーがサポートする必要があります[KSPROPSETID\_オーディオ](https://msdn.microsoft.com/library/windows/hardware/ff537440)が、オーディオ ドライバーも追加のプロパティのセットをサポート可能性があります。 ドライバーのクライアントは、フィルターの機能を検出して、フィルターの構成可能な設定を変更するプロパティの要求を使用します。

-   必要に応じて、ドライバーには、ハードウェア クロックがサポートしています。 このクロックでは、ストリームは、同じまたは別のハードウェア上の他のストリームと同期できるように読み取りと書き込みをする必要があります。 詳細については、次を参照してください。 [KSPROPSETID\_クロック](https://msdn.microsoft.com/library/windows/hardware/ff566564)します。

-   ドライバーでメディアの他のインターフェイスをようサポート必要に応じて[ **KSINTERFACE\_標準\_ストリーミング**](https://msdn.microsoft.com/library/windows/hardware/ff563384)、 [ **KSINTERFACE\_メディア\_WAVE\_QUEUED**](https://msdn.microsoft.com/library/windows/hardware/ff563377)、または[ **KSINTERFACE\_標準\_るーぷさいせいぼたん\_ストリーミング**](https://msdn.microsoft.com/library/windows/hardware/ff563381).

 

 




