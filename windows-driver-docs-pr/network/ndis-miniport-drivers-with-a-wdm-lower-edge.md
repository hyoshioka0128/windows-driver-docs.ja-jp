---
title: NDIS ミニポート ドライバー WDM がエッジを削減します。
description: NDIS ミニポート ドライバー WDM がエッジを削減します。
ms.assetid: b371a267-c57d-4d6d-81a1-53f4b51cacea
keywords:
- ミニポート ドライバー WDK ネットワークの種類
- NDIS ミニポート ドライバー WDK、種類
- WDM 低い edge WDK ネットワーク
- 下端の NDIS ミニポート ドライバー WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a13005151e58c4be3a52799a01752caf35d8b3ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527279"
---
# <a name="ndis-miniport-drivers-with-a-wdm-lower-edge"></a>NDIS ミニポート ドライバー WDM がエッジを削減します。





バス上のデバイスを制御する NDIS ミニポート ドライバーを記述する — たとえば、ユニバーサル シリアル バス (USB) または IEEE 1394 (firewire) バス。 ミニポートのドライバーは、上端にある標準の NDIS ミニポート ドライバー インターフェイスを公開し、クラス インターフェイスの下の端に特定のバスを使用する必要があります。 ミニポート ドライバーは、I/O 要求パケット (Irp) を Microsoft Windows Driver Model (WDM) 下位インターフェイスを介してバスに送信することによって、バスに接続されているデバイスと通信します。

WDM 下端のミニポート ドライバーを逆シリアル化する必要があります。 逆シリアル化されたドライバーの詳細については、[NDIS ミニポート ドライバーの逆シリアル化](deserialized-ndis-miniport-drivers.md)を参照してください。

WDM の下端とミニポート ドライバーの詳細については、[ミニポート ドライバー WDM 下位インターフェイスが](miniport-drivers-with-a-wdm-lower-interface.md)を参照してください。

 

 





