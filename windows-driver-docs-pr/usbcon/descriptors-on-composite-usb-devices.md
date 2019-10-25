---
Description: USB 複合デバイスの記述子
title: USB 複合デバイスの記述子
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c29ff848daba9517d440293164c67a92a9ef0c85
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842397"
---
# <a name="descriptors-on-usb-composite-devices"></a>USB 複合デバイスの記述子


USB 仕様で説明されているように、すべての USB デバイスは、その機能を定義する一連の階層的な記述子を提供します。 最上位レベルでは、各デバイスに1つ以上の USB 構成記述子があり、それぞれに1つ以上のインターフェイス記述子があります。 USB 構成記述子の詳細については、「 [Usb 構成記述子](usb-configuration-descriptors.md)」を参照してください。 構成は相互に排他的であるため、一度に操作できる構成は1つだけです。

Windows Vista より前の場合、Microsoft が提供するドライバーでは、[構成] 1 のみが選択されます。 Windows Vista およびそれ以降のバージョンの Windows では、レジストリ値を設定して、 [USB 汎用親ドライバー (Usbccgp)](usb-common-class-generic-parent-driver.md)で使用する構成を指定できます。 複合デバイスでデバイス構成を選択する方法の詳細については、「 [USB デバイスの構成を選択する方法](how-to-select-a-configuration-for-a-usb-device.md)」を参照してください。

構成内では、インターフェイスとインターフェイスコレクションは個別に管理されます。 各インターフェイスは、記述子レベルで、その[**USB\_インターフェイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_interface_descriptor)構造体の**bInterfaceNumber**メンバーの一意の値によって表されます。

インターフェイスの関数は、同じ構造体の**bInterfaceClass**、 **BInterfaceSubClass**、および**binterfaceprotocol**メンバーによって示されますが、その後に続くクラス固有の記述子と共に表示されます。

記述子の詳細については、「 [USB 記述子](usb-descriptors.md)」を参照してください。

## <a name="related-topics"></a>関連トピック
[USB 汎用親ドライバー (Usbccgp)](usb-common-class-generic-parent-driver.md)  
[Microsoft 提供の USB ドライバー](system-supplied-usb-drivers.md)  



