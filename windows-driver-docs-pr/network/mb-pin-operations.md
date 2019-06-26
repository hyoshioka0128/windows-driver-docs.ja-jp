---
title: MB PIN 操作
description: MB PIN 操作
ms.assetid: ca9e1537-29e8-4849-a634-5c2177886321
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d3ce5cc457e997450b662b30e1b6a3b6072e486
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374046"
---
# <a name="mb-pin-operations"></a>MB PIN 操作


このトピックでは、MB デバイスのメモリまたは Subscriber Identity Module (SIM カード) に格納されているサブスクリプション情報のアクセス制御に関連する操作について説明します。

## <a name="mb-pin-operations-for-device-hibernation"></a>デバイスの休止状態の MB のピン留め操作

ごと、 [3 gpp](https://www.3gpp.org/about-3gpp)標準、別の種類があります SIM Pin。  このページの情報は、SIM PIN1、特定の SIM カードのユニバーサル ピン留めとも呼ばれますにのみ適用されます。  

携帯電話のモデムが、低電力状態から再開するたびに標準の 3 gpp は、SIM 資格情報が移動体通信ネットワークに接続する前に更新することが必要です。  

ため、PC と Windows ベースのタブレット デバイスの電源を切りますシステムが休止状態に入ったときにすべての周辺機器、SIM 認証が必要です、システムの電源投入時にします。  

シャーシの内部的なモデムの場合は、Windows SIM の暗証番号 (pin) をキャッシュし、自動的にロックを解除 SIM 暗証番号 (pin)、システムが起動するとき、モデムのロックが解除されて、システムが休止状態を入力するときに限り。

Windows ではこれを基になるモデム デバイス D3 コールド電源の状態の終了時に検出する方法します。  D3 コールドは、電源がオフに相当するデバイスの電源状態です。  

携帯電話モデム デバイスが D3 コールドをサポートしていない場合 Windows は自動的にロックを解除、モデムの SIM 暗証番号 (pin)。  代わりに、ユーザーがモバイル ブロード バンド接続を復元して PIN を手動で入力する必要があります。

USB モデム デバイスでコールド D3 を有効にする方法については、参照してください。

* [USB デバイスの D3Cold をサポートしている](https://techcommunity.microsoft.com/t5/Microsoft-USB-Blog/bg-p/MicrosoftUSBBlog)します。
* [ドライバーで D3cold のサポート](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-d3cold-in-a-driver)

ピン留め操作の詳細については、次を参照してください。 [OID\_WWAN\_PIN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin)します。
