---
title: DLS ダウンロードのサポート
description: DLS ダウンロードのサポート
ms.assetid: be080b53-0a9d-47fc-b07b-88052efdf9a8
keywords:
- ダウンロード可能なサウンド WDK オーディオ
- カスタム レンダリング WDK オーディオ、ダウンロード可能なサウンドを DirectMusic
- ユーザー モードの WDK オーディオ、ダウンロード可能なサウンドでカスタムの表示
- DLS WDK オーディオ
- インストルメント化サウンド WDK オーディオ
- MIDI 注メッセージに変換します。
- MIDI 注変換 WDK オーディオ
- シンセサイザー WDK オーディオ、ダウンロード可能なサウンドをユーザー モード
- カスタムのシンセサイザーの WDK オーディオ、ダウンロード可能なサウンド
- シンセサイザー WDK オーディオ、ダウンロード可能なサウンド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 934edba559ecf21ffe2964314faeb2361b0cb686
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333759"
---
# <a name="dls-download-support"></a>DLS ダウンロードのサポート


## <span id="custom_dls"></span><span id="CUSTOM_DLS"></span>


独自のシンセサイザーを記述する場合は、アプリケーションが特定の楽器音に MIDI 注メッセージを変換できるように、ダウンロード可能なサウンド (DL) のサポートを提供する必要があります。 具体的には、実装する必要があります、 [ **IDirectMusicSynth::Download** ](https://msdn.microsoft.com/library/windows/hardware/ff536532)メソッドをシンセサイザーにインストルメント化 wave とアーティキュレーション データをダウンロードできます。 このメソッドは、(通常は、コレクション ファイル) から生データをそのまま使用し、レンダリング エンジンで使用できる形式で格納する必要があります。

DirectMusic が配布リストのデータをドライバーをダウンロードするときは、データ バッファーの形式がいくつかの DirectMusic 構造体の観点から定義されます。 ダウンロードされたデータは、2 つの構造で始まります。

<span id="DMUS_DOWNLOADINFO"></span><span id="dmus_downloadinfo"></span>DMU\_DOWNLOADINFO  
ダウンロードされている情報を記述する固定長のヘッダー。

<span id="DMUS_OFFSETTABLE"></span><span id="dmus_offsettable"></span>DMU\_OFFSETTABLE  
ヘッダーし、説明については、ダウンロードされたデータ内のさまざまなチャンクのオフセットをオフセット テーブル。

次の表に、オフセットは、実際のデータは、次のいずれかで始まることができます。

<span id="DMUS_INSTRUMENT"></span><span id="dmus_instrument"></span>DMU\_インストルメント化  
DLS インストルメント化を記述する構造体。

<span id="DMUS_WAVEDATA"></span><span id="dmus_wavedata"></span>DMU\_WAVEDATA  
PCM の形式で wave データのチャンクを含む構造体。

これらのデータ構造とデータ形式をインストルメント化および wave のデータをダウンロードするために使用する方法の詳細については、Microsoft Windows sdk で DirectMusic 低レベルの DL のディスカッションを参照してください。

DLS データ形式は、カーネル ユーザー モードと同じです。

[KSPROPSETID\_シンセサイザー\_Dls](https://msdn.microsoft.com/library/windows/hardware/ff537488) DLS サンプルと instruments DirectMusic シンセサイザーをダウンロードに使用されるプロパティがプロパティ セットに含まれています。 DLS レベル 1 および DLS レベル 2 の両方のデータのダウンロードには、このプロパティを設定を使用できます。 DLS レベル 1 ~ 2 でダウンロードしたデータの変更の形式のみです。

 

 




