---
title: DirectSound クライアントの詳細
description: DirectSound クライアントの詳細
ms.assetid: 95ef53d3-572d-478b-839b-0555e9051129
keywords:
- DirectSound WDK オーディオでは、非 PCM のウェーブ フォーマットします。
- 非 PCM オーディオの形式、WDK DirectSound
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97552b3be3ad5c5362903a6f073c8a55cbcb9a54
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354301"
---
# <a name="specifics-for-directsound-clients"></a>DirectSound クライアントの詳細


## <span id="specifics_for_directsound_clients"></span><span id="SPECIFICS_FOR_DIRECTSOUND_CLIENTS"></span>


Microsoft Windows 2000 および Windows 98 では、DirectSound は DirectSound バージョンに関係なく、PCM 以外の形式をサポートしていません。 (ただし、DirectSound 8 はサポート非 PCM 形式両方の Windows 2000 SP2 および Windows 98 SE + 修正プログラム。 また、Windows XP 以降に付属する DirectSound と Windows Me のバージョン形式をサポート PCM 以外。)

WDM ドライバーが特定のウェーブ フォーマットをサポートしているかどうかを確認するのにはクライアントを DSBCAPS を作成する試行できます\_LOCHARDWARE ドライバーでは、その形式でバッファリングしてから、試行が成功したかどうかを参照してください。 DirectSound API には、どの PCM 以外のデータ形式がサポートされているを検出するには、その他の方法はありません。

DirectSound は、セカンダリ DSBCAPS\_が任意の有効な LOCHARDWARE バッファー [ **WAVEFORMATEX** ](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)または[ **WAVEFORMATEXTENSIBLE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-waveformatextensible)選択したドライバーをサポートする形式。 DirectSound は、KSDATAFORMAT を含む形式に対してのみチェックは、サポートされている形式のドライバーの一覧の形式を検索する場合\_指定子\_DSOUND 指定子。

最初に、形式を説明する WAVEFORMATEX または WAVEFORMATEXTENSIBLE 構造を作成して PCM 以外の形式を使用する DirectSound アプリケーションを拡張することができます。 次に構造体へのポインターを読み込む、 **lpwfxFormat**に渡される DSBUFFERDESC 構造体のメンバー、 **CreateSoundBuffer**メソッド。 PCM 以外の形式を使用するには、DirectSound の既存のコードの変更は必要ありません。 PCM のデータの通常のドライバーをサポートするコントロールがいくつかの非 PCM 形式のサポートされる可能性がありますいないことに注意してください。 Ac-3 または WMA Pro 形式でエンコードされたデータのデジタル出力をサポートするカードが、DSBCAPS をサポートしている可能性など\_CTRLPAN または DSBCAPS\_そのデータに対して CTRLVOLUME コントロール。 したがって、これらのフラグを使用して、DirectSound のバッファーを作成しようは失敗します。

VxD ドライバーまたはレガシ waveOut ドライバーによる DirectSound 再生は PCM; に制限されます。PCM 以外の形式がサポートされていません。

 

 




