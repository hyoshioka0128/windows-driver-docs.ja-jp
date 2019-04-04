---
title: フレームワーク割り込みオブジェクト
description: フレームワーク割り込みオブジェクト
ms.assetid: FA2B8C11-69D2-4A9E-8F57-C7295DA4EE44
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec7f4a83b88e801d217216703c04431b02c182f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579258"
---
# <a name="framework-interrupt-object"></a>フレームワーク割り込みオブジェクト


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーによってフレームワークの割り込みオブジェクトが公開されている、 [ **IWDFInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/hh451283)インターフェイス。 これは、ハードウェア割り込みを表します。 割り込みオブジェクトの子である[UMDF デバイス オブジェクト](framework-device-object.md)します。 ドライバーを呼び出すことができます、 [ **IWDFDevice3::CreateInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/hh451208)割り込みオブジェクトを作成するメソッド。

ドライバーは、割り込みを作成するときに、インターフェイスに関連するイベントが発生した場合、ドライバーに通知するフレームワークから呼び出されるコールバック関数のインターフェイスを提供できます。 詳細については、[UMDF 割り込みオブジェクト イベントのコールバック関数](https://msdn.microsoft.com/library/windows/hardware/hh463979)を参照してください。

割り込みオブジェクトの詳細については、[処理割り込み](handling-interrupts.md)を参照してください。

 

 





