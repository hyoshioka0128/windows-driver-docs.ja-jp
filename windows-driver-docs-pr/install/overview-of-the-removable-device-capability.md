---
title: リムーバブル デバイスの機能の概要
description: リムーバブル デバイスの機能の概要
ms.assetid: c6dfb2ac-89a5-40fd-ae9a-1f2800af9ef8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c65e92ad0b95132a95afeb3bb60f158cb4042c73
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538153"
---
# <a name="overview-of-the-removable-device-capability"></a>リムーバブル デバイスの機能の概要


リムーバブル デバイスの機能が少し (**リムーバブル**) バス ドライバー設定されて、 **DEVICE_CAPABILITIES**)。

Devnode とその子 devnode デバイス、物理的に削除できることをすべて切断、またはコンピューターの実行中に、その親 devnode から電源が入っていないときに、バス ドライバーは devnode のリムーバブル デバイスの機能を設定します。 通常、devnode は、最上位の devnode devnode トポロジ内である場合は、リムーバブルとしてマークする必要があります。

Devnode をリムーバブル デバイスの機能を正しく設定することが重要です。 バス ドライバーでの列挙を devnode のコンテナーの ID を提供できない場合、プラグ アンド プレイ (PnP) マネージャーは、デバイスの列挙されたすべての devnode のコンテナー ID を生成するリムーバブル デバイスの機能を使用します。

たとえば、マウスなどの単一関数デバイスが USB 経由でコンピューターに接続されているとします。 ここでは、USB バス ドライバーは新しいデバイスが検出され、検出は USB ヒューマン インターフェイス デバイス (HID) とデバイスの USB HID devnode を作成します。 HID devnode もが検出された HID デバイス マウス HID 準拠のマウスの子 devnode を作成します。 この時点では、マウスがインストールされ、コンピューターの機能します。 新しい devnode の両方を使用して独立した*ドライバー スタック*します。

一般的な規則としては設定リムーバブルとその子 devnode の各である必要がありますにデバイスの最上位の (親) devnode リムーバブル、として設定する必要があります。 前の例では、USB バス ドライバーを設定、**リムーバブル**ビットを**TRUE** USB HID devnode、およびセットの**リムーバブル**ビットを**FALSE**子 HID 準拠のマウス devnode の。

次のデバイス マネージャーのスクリーン ショットでは、ジェネリックの USB マウス devnode トポロジを示していて、マウスのどの devnode がリムーバブルとマークされているを示します。

![usb マウス devnode トポロジを示すデバイス マネージャー ウィンドウのスクリーン ショット](images/containerid-2.png)

 

 





