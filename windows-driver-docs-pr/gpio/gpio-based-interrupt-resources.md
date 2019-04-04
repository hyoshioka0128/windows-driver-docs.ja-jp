---
title: 割り込みの GPIO ベースのリソース
description: 割り込みを汎用入出力 (GPIO) ピンとして抽象 Windows GPIO 割り込みを取得する送信周辺機器のデバイス用のドライバーでは、リソースを中断します。
ms.assetid: 65031C43-917D-4665-BD7F-97D3DDA0A918
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4faac9f588b4980abb7094d4c13895603f342b9e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535315"
---
# <a name="gpio-based-interrupt-resources"></a>割り込みの GPIO ベースのリソース


割り込みを汎用入出力 (GPIO) ピンとして抽象 Windows GPIO 割り込みを取得する送信周辺機器のデバイス用のドライバーでは、リソースを中断します。 [カーネル モード ドライバー フレームワーク](https://msdn.microsoft.com/library/windows/hardware/ff544296)(KMDF) ドライバーと[ユーザー モード ドライバー フレームワーク](../wdf/overview-of-the-umdf.md)(UMDF) ドライバーを通じてこれらのリソースが表示される、 [ *EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)イベント コールバック関数。

割り込みの GPIO ベースのリソースを使用して、周辺機器のデバイス ドライバーは、割り込みコント ローラーまたはプロセッサ チップの割り込みの pin に GPIO pin の代わりにで割り込みが生成されるかどうかなどの低レベルの実装の詳細を無視できます。

GPIO ベース割り込み型のリソースは、 **CmResourceTypeInterrupt**します。 この割り込みの構成パラメーターに含まれる、 **u.Interrupt**のメンバー、 [ **CM\_部分\_リソース\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff541977)割り込みリソースを記述する構造体。 割り込み割り込みサービス ルーチン (ISR) に接続するには、UMDF または KMDF ドライバーを指定両方、[生、翻訳した](https://msdn.microsoft.com/library/windows/hardware/ff544561)割り込み作成メソッドへの割り込みのリソースの説明。

KMDF または UMDF ドライバーの周辺機器を呼び出し、 [ **WdfInterruptCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate) ISR をデバイスからの割り込みに接続するメソッド。 ポインターは、このメソッドへの入力パラメーターのいずれかを[ **WDF\_割り込み\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)割り込みの構成情報を含む構造体。 詳細については、[ハードウェアの割り込み処理](../wdf/handling-hardware-interrupts.md)を参照してください。

これらのリソースへの入力パラメーターとして提供されている生、翻訳したリソースの一覧に表示される順序に注意してくださいこのドライバーがある必要があります、周辺機器のデバイス ドライバーは、GPIO 割り込みの 1 つ以上のリソースを使用している場合、  *。EvtDevicePrepareHardware*関数または**OnPrepareHardware**メソッド。 ドライバーで想定される順序と同じプラットフォーム ファームウェアで説明した順序でこれらのリスト内のリソースが表示されます。

 

 




