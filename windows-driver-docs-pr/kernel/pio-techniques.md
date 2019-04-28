---
title: PIO の手法
description: PIO の手法
ms.assetid: bd673e43-c864-416b-b0d0-23c4ba1b870c
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fd5f6a1a9051d8b2bbc0178807a38ceabe24ae5f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369254"
---
# <a name="pio-techniques"></a>PIO の手法


一部のコンピューターのハードウェア アーキテクチャ上、CPU (中央処理装置) からデバイスへのデータの転送にによってプログラミング入力/出力 (PIO) は行われます。 PIO を使用するには、非常に非効率になることができますが、転送されるデータの CPU が待機する必要があります。 このテクノロジは置き換えられました最も多くのインスタンスにダイレクト メモリ アクセス (DMA) によって DMA 割り当てることがので、データの転送、ハードウェアのコント ローラーに CPU を他のタスクを実行できるようにすること。

PIO でキャッシュの使用方法の詳細については、次を参照してください。 [PIO 操作中にキャッシュされたデータをフラッシュ](flushing-cached-data-during-pio-operations.md)します。

 

 




