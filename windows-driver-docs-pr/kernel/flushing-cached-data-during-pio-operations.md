---
title: PIO 操作中のキャッシュ データのフラッシュ
description: PIO 操作中のキャッシュ データのフラッシュ
ms.assetid: 8b15f1c4-d3c9-4d61-be37-ee1593f9d5e5
keywords:
- キャッシュされたデータのフラッシュ
- KeFlushIoBuffers
- PIO 転送操作の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5f1e04a3a4d4ccb1ed2b959b74fef150af06e17
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359962"
---
# <a name="flushing-cached-data-during-pio-operations"></a>PIO 操作中のキャッシュ データのフラッシュ





一部のプラットフォームでは、プロセッサの命令およびデータのキャッシュは、キャッシュ コヒレンシーの異常を PIO 読み取り操作中に発生します。

**注**   PIO を使用するドライバー、読み取り操作中にデータの整合性を維持するためにこのガイドラインに従う必要があります。呼び出す[ **KeFlushIoBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff552041)ごとの最後の読み取り操作。

たとえば、システム メモリへのデバイスから PIO 転送を行うドライバーを呼び出す必要があります**KeFlushIoBuffers**各デバイスの転送操作の最後にします。 別の例として、シーケンスを読み取り、デバイス登録のシステム メモリにドライバーを呼び出す必要があります**KeFlushIoBuffers**シーケンスの最後にします。 それ以外の場合、このようなドライバーは一部のプラットフォームでのシステム メモリ内ではなく、プロセッサのデータ キャッシュにまだがデータにアクセスしよう可能性があります。

 

**KeFlushIoBuffers**は何もに、プロセッサを使用する場合は、キャッシュの一貫性を維持、ためこのサポート ルーチンを呼び出し、このようなプラットフォームでオーバーヘッドはほとんどありません。

 

 




