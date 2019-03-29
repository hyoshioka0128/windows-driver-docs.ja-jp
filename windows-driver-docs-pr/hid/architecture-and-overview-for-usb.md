---
title: HID の USB トランスポート経由でのアーキテクチャ
description: このセクションでは、USB トランスポート経由で HID をサポートするデバイスのドライバー スタックについて説明します。
ms.assetid: D0D87B86-AD36-442A-9D36-571D12A360D4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d33f5f44205c2ba8b05f649dabd2b4f417be878
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574082"
---
# <a name="architecture-and-overview"></a>アーキテクチャと概要


このセクションでは、USB トランスポート経由で HID をサポートするデバイスのドライバー スタックについて説明します。

USB ドライバー スタック上の HID は、Microsoft から提供される次のコンポーネントで構成されます。 次の図は、スタックとこれらのコンポーネントを示しています。

![hid usb ドライバーのアーキテクチャ ](images/transport-usb.png)

Windows 8 では、USB 経由でのバージョン 1.1 以降の HID プロトコルの仕様を実装する HID の WDF ベース ミニポート ドライバーを提供します。 このドライバーは、HIDUSB という名前です。SYS です。 Windows では、USB デバイス クラス互換性 ID の一致に基づくこのドライバーを読み込みます。

 

 




