---
title: シリアル サービス用のレジストリ設定
description: シリアル サービス用のレジストリ設定
ms.assetid: 5c4a28ab-e2e5-45b4-8179-6f5d40e9c98c
keywords:
- Serial service WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7215bc17f2a69f60ac595ddec462b77a90040f6c
ms.sourcegitcommit: 6b09412f7bf562f7c01ffa94ac44a3d0ea895e3c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82086712"
---
# <a name="registry-settings-for-the-serial-service"></a>シリアル サービス用のレジストリ設定





このトピックでは、serial が関数ドライバーまたは下位レベルのデバイスフィルタードライバーとして使用されるすべてのシリアルデバイスに適用される、シリアルのレジストリ設定について説明します。

シリアルは、サービスエントリが読み込まれた後、その値をクエリします。 エントリ値が存在しない場合、シリアルによってサービスエントリ値が追加されます。 シリアルを設定すると、エントリ値は、システム指定のシリアル .sys ドライバーで静的に定義される既定値に設定されます。 シリアルの読み込み後にサービスエントリの値が変更された場合、次にシリアルが読み込まれるときに新しい値が使用されます。

Serial では、. の下にある次のサービスエントリ値を使用します。 **サービス\\のシリアルレジストリ\\**キー:

<a href="" id="forcefifoenable--reg-dword-"></a>**Forcefion enable** (REG\_DWORD)  
直列が Fifo を使用するように強制するかどうかを示すブール型のフラグを指定します。 **ForceFifofEnable**が0以外の場合、直列が fifo の存在を検出できるかどうかに関係なく、fifo が使用されます。 それ以外の場合は、直列が検出できる場合にのみ、Fifo が使用されます。 の既定値は0以外です。 エントリ値が指定されていない場合、シリアルは**Forcefiに有効**なエントリ値を既定値に設定します。 検出方法の詳細については、GitHub の[シリアルドライバーのサンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/serial/serial)を参照してください。

<a href="" id="rxfifo--reg-dword-"></a>**RxFIFO** (REG\_DWORD)  
ポートの割り込みをトリガーする receive FIFO のバイト数を指定します。 有効な値については、GitHub の[シリアルドライバーサンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/serial/serial)で、serial .h ヘッダーファイルで定義されている定数を参照してください。 **RxFIFO**の既定値は8バイトです。 エントリ値が存在しない場合は、 **RxFIFO**エントリ値が既定値に設定されます。

<a href="" id="txfifo--reg-dword-"></a>**Txfifo** (REG\_DWORD)  
ポートの割り込みをトリガーする送信 FIFO のバイト数を指定します。 有効な値については、GitHub の[シリアルドライバーサンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/serial/serial)で、serial .h ヘッダーファイルで定義されている定数を参照してください。 既定値の**Txfifo**は14バイトです。 エントリ値が存在しない場合、シリアルは**Txfifo**エントリ値を既定値に設定します。

<a href="" id="permitshare--reg-dword-"></a>**PermitShare** (REG\_DWORD)  
ポートが使用する割り込みをシステムが共有することを許可するかどうかを示すブール型のフラグを指定します。 **PermitShare**が0以外の場合は、割り込みを共有できます。それ以外の場合は、割り込みを共有できません。 **PermitShare**の既定値は0x00000000 です。 エントリ値が指定されていない場合、Serial は**PermitShare** entry 値を既定値に設定します。

<a href="" id="breakonentry--debuglevel--and-logfifo"></a>**Breakonentry**、 **Debuglevel**、および**logfifo**  
デバッグに使用するエントリ値を指定します。 これらのエントリ値の詳細については、「WDK」に記載されているシリアルサンプルコードを参照してください。

 

 




