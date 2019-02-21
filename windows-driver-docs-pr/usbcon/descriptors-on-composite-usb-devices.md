---
Description: Descriptors on USB Composite Devices
title: 複合の USB デバイス上の記述子
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3b5c38a1a35404fc3c9bb6612fa81d9f374f1e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529673"
---
# <a name="descriptors-on-usb-composite-devices"></a>複合の USB デバイス上の記述子


USB 仕様で説明したとおり、すべての USB デバイスは、その機能を定義する階層型記述子のセットを提供します。 最上位のレベルは、各デバイスは、1 つまたは複数の USB 構成記述子、それぞれが 1 つまたは複数のインターフェイスの記述子を持つを持っています。 USB 構成記述子については、次を参照してください。 [USB 構成記述子](usb-configuration-descriptors.md)します。 構成は相互に排他的のみで動作する 1 つの構成を選択できます。

Windows Vista では、前に Microsoft から提供されたドライバーは 1 の構成を選択するだけです。 Windows Vista および Windows の以降のバージョンでは、構成を指定するレジストリ値を設定することができます、 [USB 汎用親ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)が使用されます。 複合デバイスでデバイスの構成を選択する方法についての詳細については、次を参照してください。 [USB デバイスの構成を選択する方法](how-to-select-a-configuration-for-a-usb-device.md)します。

内での構成では、インターフェイスおよびインターフェイスのコレクションは別に管理します。 各インターフェイスで表される、記述子レベルでは、一意の値が、 **bInterfaceNumber**のメンバー、 [ **USB\_インターフェイス\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff540065)構造体。

インターフェイスの機能が付いて、 **bInterfaceClass**、 **bInterfaceSubClass**、および**bInterfaceProtocol**の同じメンバー構造体、と共に、それに続く可能性がありますクラスに固有の記述子。

記述子の詳細については、次を参照してください。[の USB ディスクリプター](usb-descriptors.md)します。

## <a name="related-topics"></a>関連トピック
[一般的な親の USB ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)  
[Microsoft 提供の USB ドライバー](system-supplied-usb-drivers.md)  



