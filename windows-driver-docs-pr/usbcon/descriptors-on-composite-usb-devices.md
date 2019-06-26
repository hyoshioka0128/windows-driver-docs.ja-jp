---
Description: 複合の USB デバイス上の記述子
title: 複合の USB デバイス上の記述子
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e7b320b524b9f3904942b276b12a0e506b0d551
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386271"
---
# <a name="descriptors-on-usb-composite-devices"></a>複合の USB デバイス上の記述子


USB 仕様で説明したとおり、すべての USB デバイスは、その機能を定義する階層型記述子のセットを提供します。 最上位のレベルは、各デバイスは、1 つまたは複数の USB 構成記述子、それぞれが 1 つまたは複数のインターフェイスの記述子を持つを持っています。 USB 構成記述子については、次を参照してください。 [USB 構成記述子](usb-configuration-descriptors.md)します。 構成は相互に排他的のみで動作する 1 つの構成を選択できます。

Windows Vista では、前に Microsoft から提供されたドライバーは 1 の構成を選択するだけです。 Windows Vista および Windows の以降のバージョンでは、構成を指定するレジストリ値を設定することができます、 [USB 汎用親ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)が使用されます。 複合デバイスでデバイスの構成を選択する方法についての詳細については、次を参照してください。 [USB デバイスの構成を選択する方法](how-to-select-a-configuration-for-a-usb-device.md)します。

内での構成では、インターフェイスおよびインターフェイスのコレクションは別に管理します。 各インターフェイスで表される、記述子レベルでは、一意の値が、 **bInterfaceNumber**のメンバー、 [ **USB\_インターフェイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbspec/ns-usbspec-_usb_interface_descriptor)構造体。

インターフェイスの機能が付いて、 **bInterfaceClass**、 **bInterfaceSubClass**、および**bInterfaceProtocol**の同じメンバー構造体、と共に、それに続く可能性がありますクラスに固有の記述子。

記述子の詳細については、次を参照してください。[の USB ディスクリプター](usb-descriptors.md)します。

## <a name="related-topics"></a>関連トピック
[一般的な親の USB ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)  
[Microsoft 提供の USB ドライバー](system-supplied-usb-drivers.md)  



