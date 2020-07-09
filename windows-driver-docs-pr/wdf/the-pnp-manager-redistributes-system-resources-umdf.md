---
title: PnP マネージャーによるシステムリソースの再配布 (UMDF 1)
description: PnP マネージャーがシステム リソースを再配布する
ms.assetid: c8e6277b-b1e5-449f-b5a0-f5a46b46e56e
keywords:
- 電源管理のシナリオ WDK UMDF、PnP マネージャーによるシステムリソースの再配布
- システムリソースの再配布のシナリオ WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b97df9ba28892a51fce9c5c5b53528bd6d3a6e1a
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141340"
---
# <a name="the-pnp-manager-redistributes-system-resources-umdf-1"></a>PnP マネージャーによるシステムリソースの再配布 (UMDF 1)


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

ユーザーがデバイスをシステムに追加し、PnP マネージャーが既に別のデバイスに割り当てているシステムリソースがデバイスに必要な場合は、PnP マネージャーがリソースの再割り当てを試行します。

このプロセスの間、PnP マネージャーはデバイスを停止し、動作 (D0) 状態から除外します。 その後、新しいリソースリストがデバイスに配信され、新しいリソースを使用して再起動できるようになります。

リソースを再配布するときに、デバイスの UMDF ベースのドライバーのいずれかで[**IPnpCallback:: OnQueryStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-onquerystop)コールバック関数が提供され、コールバック関数が再割り当てを拒否した場合、PnP マネージャーはデバイスのリソース割り当てを変更しません。

<a href="" id="power-down-sequence"></a>**電源ダウンシーケンス**  
各 UMDF ベースの関数とフィルタードライバーが停止しているデバイスをサポートしている場合、フレームワークは、ドライバースタックの最上位にあるドライバーから、一度に1つのドライバーを順番に実行します。

1.  ドライバーが自己管理型 i/o を使用している場合、フレームワークは、ドライバーの[**IPnpCallbackSelfManagedIo:: OnSelfManagedIoSuspend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackselfmanagedio-onselfmanagediosuspend)コールバック関数を呼び出します。

2.  フレームワークは、デバイスのすべての電源管理 i/o キューを停止します。

3.  フレームワークは、ドライバーの[**IPnpCallback:: OnD0Exit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0exit) callback 関数 (存在する場合) を呼び出します。

4.  このフレームワークは、PnP マネージャーによってデバイスに割り当てられたハードウェアリソースのリストを渡して、ドライバーの[**IPnpCallbackHardware:: OnReleaseHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onreleasehardware)コールバック関数 (存在する場合) を呼び出します。

これらの手順を示す図を表示するには、[ユーザーがデバイスを Unplugs](a-user-unplugs-a-device.md)していることを確認してください。

<a href="" id="power-up-sequence-------"></a>**電源投入シーケンス**   
デバイスをサポートする各 UMDF ベースの関数とフィルタードライバーについて、フレームワークは次の処理を一度に1つずつ実行します。ドライバーはドライバースタックの一番下のドライバーから始まります。

1.  このフレームワークは、ドライバーの[**IPnpCallbackHardware:: On ハードウェア**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)コールバック関数 (存在する場合) を呼び出し、PnP マネージャーがデバイスに割り当てたハードウェアリソースのリストを渡します。

2.  フレームワークは、ドライバーの[**IPnpCallback:: OnD0Entry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0entry) callback 関数 (存在する場合) を呼び出します。

3.  フレームワークは、デバイスのすべての電源管理 i/o キューを再起動します。

4.  ドライバーが自己管理型 i/o を使用している場合、フレームワークはドライバーの[**IPnpCallbackSelfManagedIo:: OnSelfManagedIoRestart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackselfmanagedio-onselfmanagediorestart) callback 関数を呼び出します。

これらの手順を示す図については、「[デバイスにユーザーが](a-user-plugs-in-a-device.md)接続している」を参照してください。

 

 





