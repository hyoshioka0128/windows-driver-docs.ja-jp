---
title: リムーバブル デバイス機能の概要
description: リムーバブル デバイス機能の概要
ms.assetid: c6dfb2ac-89a5-40fd-ae9a-1f2800af9ef8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08f474224ee7849f3bde6bb24c3f2ee2460d8717
ms.sourcegitcommit: 8d45beff38c5d3b695eadbf624b6726c797d9b97
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2019
ms.locfileid: "71271979"
---
# <a name="overview-of-the-removable-device-capability"></a>リムーバブル デバイス機能の概要


リムーバブルデバイスの機能は、バスドライバーが**DEVICE_CAPABILITIES**に設定するビット (**リムーバブル**) です。

バスドライバーは、コンピューターの実行中に、devnode とそのすべての子 devnodes が親 devnode から物理的に削除、切断、または切断できるデバイスを構成するときに、devnode のリムーバブルデバイス機能を設定します。 通常、devnode は、devnode トポロジで最上位の devnode である場合は、リムーバブルとしてマークする必要があります。

Devnode でリムーバブルデバイス機能を正しく設定することが重要です。 Devnode (PnP) マネージャープラグアンドプレイは、列挙しているのコンテナー ID を提供できない場合、リムーバブルデバイス機能を使用して、デバイス用に列挙されたすべての devnodes のコンテナー ID を生成します。

たとえば、マウスなどの単一関数デバイスが USB 経由でコンピューターに接続されているとします。 この場合、USB バスドライバーは新しいデバイスを検出し、それが USB ヒューマンインターフェイスデバイス (HID) であることを検出して、デバイス用の USB HID devnode を作成します。 また、hid devnode は、hid デバイスがマウスであることを検出し、HID に準拠したマウスの子 devnode を作成します。 この時点で、マウスがインストールされ、コンピューター上で機能しています。 どちらの新しい devnodes も、独立した*ドライバースタック*を使用します。

一般的な規則として、デバイスの最上位 (親) devnode はリムーバブルとして設定する必要がありますが、各子 devnodes をリムーバブルとして設定することはできません。 前の例では、usb バスドライバーによって USB HID devnode の**リムーバブル**ビットが**TRUE**に設定され、hid に準拠している子マウス devnode の**リムーバブル**ビットが**FALSE**に設定されています。

次のデバイスマネージャースクリーンショットは、一般的な USB マウスの devnode トポロジを示しています。また、マウスの devnodes がリムーバブルとしてマークされていることを示しています。

![usb マウスの devnode トポロジを示すデバイスマネージャーウィンドウのスクリーンショット](images/containerid-2.png)

 

 





