---
title: フレームワーク割り込みオブジェクト
description: フレームワーク割り込みオブジェクト
ms.assetid: FA2B8C11-69D2-4A9E-8F57-C7295DA4EE44
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7807dbe86efd9d531ae90f6b0b30586588c78ea2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368677"
---
# <a name="framework-interrupt-object"></a>フレームワーク割り込みオブジェクト


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーによってフレームワークの割り込みオブジェクトが公開されている、 [ **IWDFInterrupt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfinterrupt)インターフェイス。 これは、ハードウェア割り込みを表します。 割り込みオブジェクトの子である[UMDF デバイス オブジェクト](framework-device-object.md)します。 ドライバーを呼び出すことができます、 [ **IWDFDevice3::CreateInterrupt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt)割り込みオブジェクトを作成するメソッド。

ドライバーは、割り込みを作成するときに、インターフェイスに関連するイベントが発生した場合、ドライバーに通知するフレームワークから呼び出されるコールバック関数のインターフェイスを提供できます。 詳細については、次を参照してください。 [UMDF 割り込みオブジェクト イベントのコールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/)します。

割り込みオブジェクトの詳細については、次を参照してください。[処理割り込み](handling-interrupts.md)します。

 

 





