---
title: MB PIN 操作
description: MB PIN 操作
ms.assetid: ca9e1537-29e8-4849-a634-5c2177886321
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc6e164116a4c427b4da5395d9b865811bf506f0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343291"
---
# <a name="mb-pin-operations"></a>MB PIN 操作


このトピックでは、MB デバイスのメモリまたは Subscriber Identity Module (SIM カード) に格納されているサブスクリプション情報のアクセス制御に関連する操作について説明します。

## <a name="mb-pin-operations-for-device-hibernation"></a>デバイスの休止状態の MB のピン留め操作

ごと、 [3 gpp](http://www.3gpp.org/about-3gpp)標準、別の種類があります SIM Pin。  このページの情報は、SIM PIN1、特定の SIM カードのユニバーサル ピン留めとも呼ばれますにのみ適用されます。  

携帯電話のモデムが、低電力状態から再開するたびに標準の 3 gpp は、SIM 資格情報が移動体通信ネットワークに接続する前に更新することが必要です。  

ため、PC と Windows ベースのタブレット デバイスの電源を切りますシステムが休止状態に入ったときにすべての周辺機器、SIM 認証が必要です、システムの電源投入時にします。  

シャーシの内部的なモデムの場合は、Windows SIM の暗証番号 (pin) をキャッシュし、自動的にロックを解除 SIM 暗証番号 (pin)、システムが起動するとき、モデムのロックが解除されて、システムが休止状態を入力するときに限り。

Windows ではこれを基になるモデム デバイス D3 コールド電源の状態の終了時に検出する方法します。  D3 コールドは、電源がオフに相当するデバイスの電源状態です。  

携帯電話モデム デバイスが D3 コールドをサポートしていない場合 Windows は自動的にロックを解除、モデムの SIM 暗証番号 (pin)。  代わりに、ユーザーがモバイル ブロード バンド接続を復元して PIN を手動で入力する必要があります。

USB モデム デバイスでコールド D3 を有効にする方法については、参照してください。

* [USB デバイスの D3Cold をサポートしている](https://blogs.msdn.microsoft.com/usbcoreblog/2013/02/18/supporting-d3cold-for-usb-devices)します。
* [ドライバーで D3cold のサポート](https://msdn.microsoft.com/library/windows/hardware/hh967717)

ピン留め操作の詳細については、次を参照してください。 [OID\_WWAN\_PIN](https://msdn.microsoft.com/library/windows/hardware/ff569828)します。
