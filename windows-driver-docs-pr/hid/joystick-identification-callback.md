---
title: ジョイスティック識別コールバック
description: ジョイスティック識別コールバック
ms.assetid: d5e859d2-bfe4-41ef-9d09-ebb945d299bd
keywords:
- WDK ジョイスティックのコールバック
- WDK の HID ジョイスティック、ID 要求
- ID は、WDK のジョイスティックを要求します。
- コールバック WDK ジョイスティックの識別
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 209d6b25b3d9494f1566e00df1b698bcf4de5c7e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527556"
---
# <a name="joystick-identification-callback"></a>ジョイスティック識別コールバック





```cpp
int __stdcall JoyIdRoutine( int joyid, BOOL used );
```

VJoyD は、ユーザーを構成または 16 のジョイスティックの 1 つとして、ジョイスティックを構成解除するときに、JoyIDRoutine を呼び出します。 ようにミニドライバーに要求された ID をサポートできる場合*joyid*JoyIdRoutine が 0 以外の値を返します。 ミニドライバーは、ID をサポートできない場合、ルーチンは、値 0 を返します。

変更され、joyConfigChanged が呼び出され、ドライバーを更新する、VJoyD サイクルすべて 16 台のデバイスから JOYSTICKID1 以降します。 未使用にすべてのデバイスをリセットし、すべての人、システムが使用する必要があるを設定するには、もう一度をループ処理します。 コントロール パネルの操作中にこのプロセスは、初期化のためこのコールバックの使用方法で問題を作成する多数の呼び出しを伴うことができます。 これは他のサービスが利用できない場合は、システムのブートが完了する前に、呼び出しが行われた場合は特に当てはまります。

ジョイスティックの識別子を保持する 1 つ以上のデバイスのサービスのコールバックを試みる必要があるミニドライバーは、可能であれば、ユーザーの混乱を避けるために、1 つの物理デバイスに関連付けられます。 実装できますこの比較的簡単に 1 つのセッション中を再起動する必要はないでしょう。

 

 




