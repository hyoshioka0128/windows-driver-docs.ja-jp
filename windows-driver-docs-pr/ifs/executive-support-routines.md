---
title: エグゼクティブサポートルーチン
description: エグゼクティブサポートルーチン
ms.assetid: f86b942c-9a3f-495b-9623-fd0656ec4a7a
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: b652b6a837e587d2df429c8379e1060bfc64ae9d
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955796"
---
# <a name="executive-support-routines"></a>エグゼクティブサポートルーチン

次のシステムによって提供される executive サポート関数とマクロは、カーネルモードのファイルシステムおよびミニフィルターとレガシフィルタードライバーによって呼び出すことができますが、デバイスドライバーでは呼び出せません。 システムで使用するために予約されている関数もあります。

ここに記載されているルーチンに加えて、ファイルシステムとフィルタードライバーは、 *ntifs*で宣言されているカーネルモードドライバーアーキテクチャリファレンスセクションで説明されているすべての**Ex**_Xxx_ルーチンを呼び出すこともできます。

**ヘッダーファイル:** *ntifs*

** プレフィックス:Ex * Xxx @ no__t-0 @ no__t

| 関数またはマクロ | 説明 |
| ----------------- | ----------- |
| **ExAdjustLookasideDepth** | システム用に予約されています。 |
| **ExDisableResourceBoost スト** | システム用に予約されています。 |
| **Exdisableresourceブー Stlite** | システム用に予約されています。 |
| **ExInitializeWorkItem** | 呼び出し元が指定したコンテキストとコールバックルーチンを使用して、システムワーカースレッドに制御が与えられたときに実行のためのキューに登録される作業キュー項目を初期化します。 このルーチンは細心の注意を払って使用してください。|
| **ExQueryPoolBlockSize** | 使われていません。 |
| **ExQueueWorkItem** | 指定された作業項目をキューに挿入します。このキューから、システムワーカースレッドが項目を削除し、呼び出し元が ExInitializeWorkItem に指定したルーチンに制御を与えます。 このルーチンは細心の注意を払って使用してください。 |
