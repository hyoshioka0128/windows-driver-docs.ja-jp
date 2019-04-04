---
title: シリアル サービス用レジストリ設定
description: シリアル サービス用レジストリ設定
ms.assetid: 5c4a28ab-e2e5-45b4-8179-6f5d40e9c98c
keywords:
- シリアル サービス WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf34c958de7cdd09e6fabfbb5b913fbfb472381a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549751"
---
# <a name="registry-settings-for-the-serial-service"></a>シリアル サービス用レジストリ設定





このトピックでは、どのシリアルのすべてのシリアル デバイスに関数のドライバーまたは低レベル デバイス フィルター ドライバーは、シリアルが適用されるレジストリ設定について説明します。

シリアルは、それが読み込まれた後、サービスのエントリの値を照会します。 エントリの値が存在しない場合、シリアルはサービスのエントリの値を追加します。 シリアルは、エントリの値をシステム提供の際にドライバーで静的に定義されている既定値に設定します。 シリアルが読み込まれた後、サービスのエントリの値を変更する場合に、次回シリアルが読み込まれる新しい値が使用します。

シリアルが下にある次のサービスのエントリの値を使用して、 **.\\サービス\\シリアル**レジストリ キー。

<a href="" id="forcefifoenable--reg-dword-"></a>**ForceFifoEnable** (REG\_DWORD)  
Fifo を使用するシリアルを強制するかどうかを示すブール フラグを指定します。 場合**ForceFifofEnable**が 0 以外の場合、Fifo を使用するシリアルが Fifo の存在を検出するかどうかに関係なく。 それ以外の場合、Fifo は、シリアルが検出できる場合にのみ使用されます。 既定値は、0 以外の値です。 シリアルの設定、エントリの値が存在しない場合、 **ForceFifoEnable**エントリの値を既定値。 検出の詳細については、メソッドは、、[シリアル ドライバーのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=617962)GitHub でを参照してください。

<a href="" id="rxfifo--reg-dword-"></a>**RxFIFO** (REG\_DWORD)  
受信ポートの割り込みをトリガーする FIFO のバイト数を指定します。 有効な値は、Serial.h ヘッダー ファイルで定義されている定数を参照してください、[シリアル ドライバーのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=617962)GitHub でします。 既定値**RxFIFO**は 8 バイトです。 シリアルの設定、エントリの値が存在しない場合、 **RxFIFO**エントリの値を既定値。

<a href="" id="txfifo--reg-dword-"></a>**TxFIFO** (REG\_DWORD)  
送信ポートの割り込みをトリガーする FIFO のバイト数を指定します。 有効な値は、Serial.h ヘッダー ファイルで定義されている定数を参照してください、[シリアル ドライバーのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=617962)GitHub でします。 既定値**TxFIFO**は 14 バイトです。 シリアルの設定、エントリの値が存在しない場合、 **TxFIFO**エントリの値を既定値。

<a href="" id="permitshare--reg-dword-"></a>**PermitShare** (REG\_DWORD)  
システムを割り込みポートを使用する共有を許可するかどうかを示すブール フラグを指定します。 場合**PermitShare**が 0 以外の場合、割り込みを共有できます。 それ以外の場合、割り込みを共有することはできません。 既定値**PermitShare** 0x00000000 します。 シリアルの設定、エントリの値が存在しない場合、 **PermitShare**エントリの値を既定値。

<a href="" id="breakonentry--debuglevel--and-logfifo"></a>**BreakOnEntry**、 **DebugLevel**、および**LogFifo**  
デバッグに使用されるエントリの値を指定します。 これらのエントリの値の詳細については、WDK に含まれるシリアル サンプル コードを参照してください。

 

 




