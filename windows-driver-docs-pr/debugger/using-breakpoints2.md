---
title: デバッガー エンジン API でのブレークポイントの使用
description: ブレークポイント デバッガー エンジン API - 設定および制御を使用します。
ms.assetid: d1880895-dc01-429b-af48-762cb24539f1
keywords:
- デバッガー エンジン、ブレークポイント
- ブレークポイント
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0937c06b35e2c1ec52629958fd9acf194d8a2a04
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371694"
---
# <a name="using-breakpoints-with-the-debugger-engine-api"></a>デバッガー エンジン API でのブレークポイントの使用


## <span id="ddk_breakpoints_dbx"></span><span id="DDK_BREAKPOINTS_DBX"></span>


ブレークポイントは、ブレークポイントの条件が満たされるは、ターゲットの実行を停止し、デバッガーを中断するイベントのトリガーです。 ブレークポイントを分析し、おそらく実行は、特定の時点または特定のメモリ位置がアクセスされるときに達すると、ターゲットを変更できます。

デバッガー エンジンが挿入、*ソフトウェア ブレークポイント*プロセッサの命令にブレークポイントの場所を変更することで、ターゲットにこの変更は、エンジンのクライアントに表示されません。 ターゲットは、ブレークポイントの場所に命令を実行するときは、ソフトウェアのブレークポイントがトリガーされます。 A*プロセッサ ブレークポイント*デバッガー エンジン; によって、ターゲットのプロセッサに挿入がその機能は、プロセッサ固有。 ブレークポイントの場所にメモリがアクセスされる; とプロセッサによってトリガーされます。アクセスの種類は、このブレークポイントをトリガーすると、ブレークポイントの作成時に指定されます。

このトピックには次が含まれます。

[ブレークポイントの設定](setting-breakpoints.md)

[ブレークポイントのフラグとパラメーターを制御します。](controlling-breakpoint-flags-and-parameters.md)

 

 





