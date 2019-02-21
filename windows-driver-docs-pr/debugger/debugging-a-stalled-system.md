---
title: デバッグを停止しているシステム
description: デバッグを停止しているシステム
ms.assetid: 83679dca-2477-4d03-9a89-5a5aebc7b9d9
keywords:
- 停止しているシステムのデバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 187712a6006aef96a60e99ff97d5469a07d2f08d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538543"
---
# <a name="debugging-a-stalled-system"></a>デバッグを停止しているシステム


## <span id="ddk_debugging_a_stalled_system_dbg"></span><span id="DDK_DEBUGGING_A_STALLED_SYSTEM_DBG"></span>


ときにコンピューターが実際にはバグ チェックを開始せずに応答を停止することができますもあります。 この「フリーズ」は、さまざまな形式で表示できます。

-   マウス ポインターを移動できますが、画面上の任意の windows には影響しません。

-   画面全体は引き続きとマウス ポインターが移動しませんが、メモリとディスク間でページングが続行されます。

-   画面はまだとディスクはサイレントで実行します。

マウス ポインターを移動またはがある場合、ディスクにページング、これは通常、クライアント サーバー ランタイム サブシステム (CSRSS) 内での問題によりします。

NTSD が CSRSS で実行している場合は、かどうかは特に変わったことを確認するには、f12 キーを押すと各スレッド ダンプをキーを押します。 (を参照してください[デバッグ CSRSS](debugging-csrss.md)の詳細)。

CSRSS の検査、何が判明している場合、問題の可能性があります、カーネルすべて。

マウスの動きやページングがない場合はほぼ確実にカーネルの問題です。

この種のカーネル クラッシュを分析することは困難な作業では一般的です。 KD 分割を開始 (で[ **CTRL + C**](ctrl-c--break-.md)) または WinDbg (で**CTRL + BREAK**)。 デバッガー コマンドを使用して、状況を確認することができますようになりました。

このケースで役に立つテクニックがいくつか:

[失敗したプロセスの検索](finding-the-failed-process.md)

[大量の割り込みのデバッグ](debugging-an-interrupt-storm.md)

 

 





