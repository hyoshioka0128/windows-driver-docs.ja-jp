---
title: カーネルモード メモリ リークの検出
description: カーネルモード メモリ リークの検出
ms.assetid: 7e707b89-8614-46d7-9c2e-bea2ddf16164
keywords:
- メモリ リーク、カーネル モード
- メモリ リーク、カーネル モードの概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5de6d820114d0f3af2b0b791b40cf0c0d135b28d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572583"
---
# <a name="finding-a-kernel-mode-memory-leak"></a>カーネルモード メモリ リークの検出


カーネル モードのメモリ リークの原因を特定するのにには、次の手法を使用します。

[PoolMon を使用してカーネル モードのメモリ リークを検出するには](using-poolmon-to-find-a-kernel-mode-memory-leak.md)

[カーネル デバッガーを使用してカーネル モード メモリ リークの検出](using-the-kernel-debugger-to-find-a-kernel-mode-memory-leak.md)

[Driver Verifier を使用してカーネル モードのメモリ リークを検出するには](using-driver-verifier-to-find-a-kernel-mode-memory-leak.md)

どのカーネル モード ドライバーまたはコンポーネントがリークの原因がわからない場合は、まず PoolMon 技法を使用する必要があります。 この手法は、メモリ リーク; に関連付けられているプール タグを表示します。このプール タグを使用するコンポーネント、ドライバーは、メモリ リークを担当します。

既に特定担当ドライバーまたはコンポーネント場合より具体的には、リークの原因を特定する上記のリストに 2 番目と 3 番目の手法を使用します。

 

 





