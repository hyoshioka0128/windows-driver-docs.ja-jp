---
title: CustomTimerDpc コンテキスト情報の提供
description: CustomTimerDpc コンテキスト情報の提供
ms.assetid: b4d711fb-63d4-45c6-8054-f934741ce340
keywords:
- タイマーオブジェクト WDK カーネル、CustomTimerDpc ルーチン
- CustomTimerDpc
- DeferredContext ルーチン
- コンテキスト情報 WDK 同期
- タイマーオブジェクト WDK カーネル、コンテキスト情報
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e6bfad906f08d3bda0cbb90a1c3ebe4998c2678
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827584"
---
# <a name="providing-customtimerdpc-context-information"></a>CustomTimerDpc コンテキスト情報の提供





[**Keinitializer Edpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedpc)に渡される*DeferredContext*ポインターは、他のドライバールーチン、および*customtimerdpc*ルーチン自体が状態を維持できるコンテキスト領域を指します。 カーネルは、DPC ルーチンへのすべての呼び出しで*DeferredContext*ポインターを渡します。

*Iotimer*ルーチンとは異なり、 *customtimerdpc*には、ドライバーによって作成されたデバイスオブジェクトとの特定の関連付けはありません。 ただし、ドライバーでは、コンテキスト領域にデバイスオブジェクトへのポインターを含めることによって、 *Customtimerdpc*ルーチンをドライバーによって作成されたデバイスオブジェクトに関連付けることができます。

コンテキスト領域は、ドライバーによって割り当てられた常駐メモリ内に存在する必要があります。 通常、このコンテキスト領域はデバイスの拡張機能に含まれていますが、非ページプールでもかまいません。 ドライバーがコントローラーオブジェクトを使用している場合は、コントローラー拡張機能に配置できます。 コンテキスト領域の内容は、ドライバーによって決まります。

*Customtimerdpc*ルーチンがコンテキスト情報をドライバーの ISR と共有する場合、 *Customtimerdpc*ルーチンは[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)を使用して、共有コンテキストにアクセスする*SynchCritSection*ルーチンを呼び出す必要があります。 詳細については、「[クリティカルセクションの使用](using-critical-sections.md)」を参照してください。

*Customtimerdpc*がコンテキスト情報を他の ISR 以外のドライバールーチンと共有する場合、 *DeferredContext*の領域は executive スピンロックによって保護されている必要があります。 詳細については、「[スピンロック](spin-locks.md)」を参照してください。

 

 




