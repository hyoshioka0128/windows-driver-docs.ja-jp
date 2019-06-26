---
title: レジストリでのメッセージ シグナル割り込みの有効化
description: レジストリでのメッセージ シグナル割り込みの有効化
ms.assetid: 802ad994-51e7-4aef-a0f0-865dfaf4e6ce
keywords:
- メッセージ シグナル割り込み WDK のカーネルを有効にします。
- WDK のカーネルの割り込みメッセージ シグナルを有効にします。
- Msi WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b3c804ea0c3224e19461c7455925f278708056f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384940"
---
# <a name="enabling-message-signaled-interrupts-in-the-registry"></a>レジストリでのメッセージ シグナル割り込みの有効化


メッセージ シグナル割り込み (Msi) を受信するには、ドライバーの INF ファイルがインストール中にレジストリで Msi を有効にする必要があります。 使用して、**管理の割り込み\\MessageSignaledInterruptProperties** MSI サポートを有効にするデバイスのハードウェア キーのサブキー。

**MSISupported**エントリの**管理の割り込み\\MessageSignaledInterruptProperties** 21\_デバイスで Msi をサポートするかどうかを決定する DWORD 値です。 設定**MSISupported** MSI サポートを有効にするには 1 です。

自分のデバイスを割り当ての Msi の最大数を指定するのにレジストリを使用することもできます。 **MessageNumberLimit**エントリの**管理の割り込み\\MessageSignaledInterruptProperties** 21\_に Msi の最大数を指定する DWORD 値割り当てます。 PCI の 2.2 **MessageNumberLimit** 1、2、4、8、または 16 にする必要があります。 PCI の 3.0 **MessageNumberLimit** 2,048 までの任意の数を指定できます。

使用して、 [ **INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)デバイスのハードウェア キーの下のレジストリ キーを設定するドライバーの INF ファイルでします。 詳細については、次を参照してください。 [ **INF DDInstall.HW セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)します。

次のコード例は、設定する方法を示します、 **MSISupported**エントリ**管理の割り込み\\MessageSignaledInterruptProperties**デバイス。 作成する必要がありますに注意してください、**管理の割り込み**と**管理の割り込み\\MessageSignaledInterruptProperties**キーを設定する前に、 **MSISupported**エントリ。

```cpp
[mydevice.HW]
AddReg = mydevice_addreg

[mydevice_addreg]
HKR,Interrupt Management,,0x00000010
HKR,Interrupt Management\MessageSignaledInterruptProperties,,0x00000010
HKR,Interrupt Management\MessageSignaledInterruptProperties,MSISupported,0x00010001,1
```

 

 




