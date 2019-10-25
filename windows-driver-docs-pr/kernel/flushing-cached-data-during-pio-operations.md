---
title: PIO 操作中のキャッシュされたデータのフラッシュ
description: PIO 操作中のキャッシュされたデータのフラッシュ
ms.assetid: 8b15f1c4-d3c9-4d61-be37-ee1593f9d5e5
keywords:
- キャッシュされたデータのフラッシュ
- KeFlushIoBuffers
- PIO 転送操作 (WDK カーネル)
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0114b99c7a4d67c243b57c196d9117b253eaae01
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838687"
---
# <a name="flushing-cached-data-during-pio-operations"></a>PIO 操作中のキャッシュされたデータのフラッシュ





一部のプラットフォームでは、プロセッサの命令およびデータキャッシュが PIO 読み取り操作中にキャッシュの一貫性の異常を示しています。

**注**   読み取り操作中にデータの整合性を維持するには、PIO を使用するドライバーが、各読み取り操作の最後に[**Keflushiobuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers)を呼び出す必要があります。

たとえば、デバイスからシステムメモリへの PIO 転送を行うドライバーは、各デバイス転送操作の終了時に**Keflushiobuffers**を呼び出す必要があります。 別の例として、一連のデバイスレジスタをシステムメモリに読み込むドライバーは、シーケンスの最後に**Keflushiobuffers**を呼び出す必要があります。 それ以外の場合、このようなドライバーは、一部のプラットフォームでは、システムメモリではなく、プロセッサのデータキャッシュに残っているデータにアクセスしようとする可能性があります。

 

**Keflushiobuffers**は、プロセッサがキャッシュの一貫性を維持するために依存している場合は何も行いません。そのため、このサポートルーチンを呼び出すと、このようなプラットフォームではほとんどオーバーヘッドが発生しません。

 

 




