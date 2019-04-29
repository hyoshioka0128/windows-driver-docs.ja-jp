---
title: プログレッシブ スキャン モニターとインターリーブ データ
description: プログレッシブ スキャン モニターとインターリーブ データ
ms.assetid: 324d8b1f-5b7d-46b6-854a-e93b10db24e5
keywords:
- ビデオ WDK ビデオ ポートのインター レース拡張機能
- DirectX VPE サポート WDK DirectDraw、インター レースのビデオ
- ビデオをインター レース VPEs WDK DirectDraw を描画するには、
- DirectDraw VPEs WDK Windows 2000 の表示、インター レースのビデオ
- 拡張機能のビデオ ポート WDK DirectDraw、インター レースのビデオ
- VPEs WDK DirectDraw、インター レースのビデオ
- DirectX VPE サポート WDK DirectDraw、proscan モニター
- 描画 VPEs WDK DirectDraw、proscan モニター
- DirectDraw VPEs WDK Windows 2000 の表示、proscan モニター
- 拡張機能のビデオ ポート WDK DirectDraw、proscan モニター
- VPEs WDK DirectDraw、proscan モニター
- proscan モニター WDK ビデオ ポートの拡張機能
- プログレッシブは、WDK ビデオ ポートの拡張機能を監視します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51817f2b58d40677b65871db843fb92c910334e8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383910"
---
# <a name="progressive-scan-monitors-and-interleaved-data"></a>プログレッシブ スキャン モニターとインターリーブ データ


## <span id="ddk_progressive_scan_monitors_and_interleaved_data_gg"></span><span id="DDK_PROGRESSIVE_SCAN_MONITORS_AND_INTERLEAVED_DATA_GG"></span>


Proscan のモニターでは、行は、フレームとして表示されます - つまり、1 行目を表示し、行 2、し、第 3 の行に表示され、します。 標準的なテレビの設定が表示されます、 *2:1 ラスター* --これは、奇数行の最初のフレームのフィールドが表示されますおよびフレームの 2 番目のフィールドもの行を表示します。 マテリアルをテレビで再生するためのものは、proscan モニターに表示される前に処理する必要があります。

 

 





