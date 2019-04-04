---
title: ドライバーの検証ツールを使用したカーネルモード メモリ リークの検出
description: ドライバーの検証ツールを使用したカーネルモード メモリ リークの検出
ms.assetid: d81a8b72-91d3-4132-9cc2-1cf1b597306a
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c34d767fe386a3c1982bc6bea1cb0e80a37b18b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577995"
---
# <a name="using-driver-verifier-to-find-a-kernel-mode-memory-leak"></a>ドライバーの検証ツールを使用したカーネルモード メモリ リークの検出


Driver Verifier は、カーネル モード ドライバーでメモリがリークしているかどうかを判断します。

Driver Verifier のプールの追跡機能は、指定したドライバーによって行われるメモリ割り当てを監視します。 ドライバーが読み込まれている時に、Driver Verifier は、ドライバーによって行われたすべての割り当てが解放されたことを確認します。 ドライバーの割り当ての一部は解放されていませんが、バグ チェックが発行されると、し、バグ チェックのパラメーターが、問題の性質を示します。

この機能がアクティブな間は、ドライバー検証マネージャーのグラフィカル インターフェイスを使用して、プールの割り当ての統計情報を監視します。 カーネル デバッガーがドライバーに接続されている場合を使用して、 [ **! verifier 0x3** ](-verifier.md)割り当ての統計情報を表示する拡張機能。

ドライバーは、ダイレクト メモリ アクセス (DMA) を使用して、Driver Verifier の DMA の検証機能がメモリ リークを見つけるに役立つもします。 さまざまな DMA ルーチン、一般的なバッファーとメモリ リークにつながる可能性があるその他のエラーを解放するための障害などの一般的なコーポレーションの DMA の検証をテストします。 カーネル デバッガーがこのオプションがアクティブな間を接続されている場合は、使用、 [ **! dma** ](-dma.md)割り当ての統計情報を表示する拡張機能。

Driver Verifier については、[Driver Verifier](https://go.microsoft.com/fwlink/p/?linkid=120480) Windows Driver Kit (WDK) ドキュメントを参照してください。

 

 





