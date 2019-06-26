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
ms.openlocfilehash: 72d98502c42266a36ca4d90242b265b35af7f666
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386595"
---
# <a name="flushing-cached-data-during-pio-operations"></a>PIO 操作中のキャッシュ データのフラッシュ





一部のプラットフォームでは、プロセッサの命令およびデータのキャッシュは、キャッシュ コヒレンシーの異常を PIO 読み取り操作中に発生します。

**注**   PIO を使用するドライバー、読み取り操作中にデータの整合性を維持するためにこのガイドラインに従う必要があります。呼び出す[ **KeFlushIoBuffers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keflushiobuffers)ごとの最後の読み取り操作。

たとえば、システム メモリへのデバイスから PIO 転送を行うドライバーを呼び出す必要があります**KeFlushIoBuffers**各デバイスの転送操作の最後にします。 別の例として、シーケンスを読み取り、デバイス登録のシステム メモリにドライバーを呼び出す必要があります**KeFlushIoBuffers**シーケンスの最後にします。 それ以外の場合、このようなドライバーは一部のプラットフォームでのシステム メモリ内ではなく、プロセッサのデータ キャッシュにまだがデータにアクセスしよう可能性があります。

 

**KeFlushIoBuffers**は何もに、プロセッサを使用する場合は、キャッシュの一貫性を維持、ためこのサポート ルーチンを呼び出し、このようなプラットフォームでオーバーヘッドはほとんどありません。

 

 




