---
title: ストリーム クラスのデバッグ
description: ストリーム クラスのデバッグ
ms.assetid: 544b922b-58e4-4cbb-a76c-d8e13ae17e55
keywords:
- Stream.sys クラス ドライバー WDK Windows 2000 のカーネル デバッグ
- ミニドライバー WDK Windows 2000 のカーネルのストリーミング、デバッグ
- WDK Windows 2000 カーネル ストリーミング、ミニドライバーのデバッグ
- stream クラス ミニドライバー WDK Windows 2000 のカーネルのデバッグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2afff5ab5c84684411417be7acaf3d8aa2e0dd47
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391375"
---
# <a name="stream-class-debugging"></a>ストリーム クラスのデバッグ





チェック (デバッグ) バージョンを使用して、 *stream.sys*ミニドライバーでエラーが発生したときに、ミニドライバーとアサートの状態に関する情報メッセージを印刷します。

Stream クラス ミニドライバーをデバッグするときに、次に、追加のヒントを使用できます。

-   Wdeb386 デバッガーの使用 (または Softice) Windows Me システムで、デバッグ時にデバッグ情報が使用可能なデバッガーは、入力に分割しています。D. を NTKERN を選択し、オプションします。これには、時系列でエントリを表示するデバッグ ログが表示されます。 Windows 2000 では、デバッグ時に、デバッグ情報がリアルタイムでターミナルのデバッグに印刷されます。

-   デバッガーの出力レベルを調整するのには、読み込む*stream.sys*シンボル (*stream.sym* Windows Me 用と*stream.sys* Windows 2000 の場合) および変更、 *StreamDebug*変数を"e StreamDebug *xx*"。 既定では 00 で、重大なエラーのみを出力します。 すべてのメッセージを印刷する FF に設定します。

-   ミニドライバーは、独自のメッセージを印刷できるを使用して*stream.sys* 、呼び出すことで説明した施設[ **StreamClassDebugPrint**](https://msdn.microsoft.com/library/windows/hardware/ff568235)します。 呼び出しで選択した出力レベル以上にする前に説明したとして出力レベルを設定する必要がありますに注意してください。

 

 




