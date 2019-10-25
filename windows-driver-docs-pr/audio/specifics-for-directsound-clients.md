---
title: DirectSound クライアントの詳細
description: DirectSound クライアントの詳細
ms.assetid: 95ef53d3-572d-478b-839b-0555e9051129
keywords:
- DirectSound WDK オーディオ、PCM 以外の wave 形式
- PCM 以外のオーディオ形式 WDK、DirectSound
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89761885dcca3e73779b3f60057fcfd2e806bb6a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830118"
---
# <a name="specifics-for-directsound-clients"></a>DirectSound クライアントの詳細


## <span id="specifics_for_directsound_clients"></span><span id="SPECIFICS_FOR_DIRECTSOUND_CLIENTS"></span>


Microsoft Windows 2000 および Windows 98 では、directsound のバージョンに関係なく、DirectSound は PCM 以外の形式をサポートしていません。 (ただし、DirectSound 8 では、Windows 2000 SP2 と Windows 98 SE + 修正プログラムの両方で PCM 以外の形式をサポートしています。 また、Windows XP 以降および Windows Me に付属している DirectSound のバージョンは、PCM 以外の形式をサポートしています)。

WDM ドライバーが特定の wave 形式をサポートしているかどうかを判断するために、クライアントはドライバーで DSBCAPS\_LOCHARDWARE バッファーを作成し、試行が成功したかどうかを確認することができます。 DirectSound API は、サポートされていない PCM データ形式を検出するための他の方法を提供しません。

DirectSound を使用すると、セカンダリ DSBCAPS\_、選択したドライバーがサポートしている有効な[**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)または[**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)形式を持つことができます。 ドライバーのサポートされている形式の一覧で形式を検索する場合、DirectSound は、DSOUND 指定子\_KSDATAFORMAT\_指定子を含む形式のみをチェックします。

まず、形式を記述した WAVEFORMATEX または WAVEFORMATEXTENSIBLE 構造体を作成して、PCM 以外の形式を使用するように DirectSound アプリケーションを拡張できます。 次に、 **CreateSoundBuffer**メソッドに渡される DSBUFFERDESC 構造体の**Lp xformat**メンバーに構造体へのポインターを読み込みます。 PCM 以外のフォーマットを使用するには、既存の DirectSound コードに対する他の変更は必要ありません。 通常、ドライバーが PCM データをサポートするコントロールは、一部の PCM 以外の形式ではサポートされないことに注意してください。 たとえば、AC-3 または WMA Pro 形式でエンコードされたデータのデジタル出力をサポートするカードでは、そのデータに対して CTRLVOLUME コントロール\_コントロールを使用して、DSBCAPS\_サポートすることはほとんどありません。 そのため、これらのフラグを使用して DirectSound バッファーを作成しようとすると、エラーが発生する可能性があります。

VxD ドライバーまたはレガシ waveOut ドライバーを使用した DirectSound 再生は、引き続き PCM に限定されます。PCM 以外の形式はサポートされていません。

 

 




