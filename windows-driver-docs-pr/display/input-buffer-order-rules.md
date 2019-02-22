---
title: 入力バッファーの順序ルール
description: 入力バッファーの順序ルール
ms.assetid: 2c588276-88c3-42e4-9f73-50a05e31c451
keywords:
- 入力バッファーの WDK DirectX VA
- デインター レースの WDK DirectX va なので、入力バッファーの順序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd66848fb10ff098da827566c1dd7e52e51f08ac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530764"
---
# <a name="input-buffer-order-rules"></a>入力バッファーの順序ルール


## <span id="ddk_input_buffer_order_rules_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_RULES_GG"></span>


**このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

内のサーフェスの順序、 **lpBufferInfo**配列は、次の規則に準拠しています。

-   配列内の最初の画面では、宛先表面です。 ドライバーは、宛先表面にのみ書き込みます。

-   次の一連の配列内のサーフェスは、前の変換先サーフェスのグループ、逆のデインター レース、デバイスが要求された一時的な順序は、そのアルゴリズムのインター レースを解除します。

-   次の一連の配列内のサーフェス インター レースの入力またはデバイスが実行するために必要なサーフェスをプログレッシブのコレクションは、その操作のインター レースを解除します。

-   次の一連の配列内のサーフェスは、Z オーダーにあるビデオ サブストリーム サーフェスのコレクションです。

 

 





