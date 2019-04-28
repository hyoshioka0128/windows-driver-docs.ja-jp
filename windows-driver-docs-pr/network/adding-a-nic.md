---
title: NIC の追加
description: NIC の追加
ms.assetid: 3da89acc-5504-4362-b148-e8228795721f
keywords:
- WDK の Nic を追加するネットワークを
- ネットワーク インターフェイス カードの WDK ネットワーク、追加します。
- プラグ アンド プレイ WDK NDIS ミニポート、NIC を追加します。
- Nic の WDK ネットワークを追加します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d17cb4f22b8329a45bc722a486ef851e246f46e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367780"
---
# <a name="adding-a-nic"></a>NIC の追加





次の説明では、ミニポート ドライバーの読み込みで開始し、NIC を追加する方法について説明します。 手順 1 ~ 11 の PnP マネージャーは、実行中のシステムに追加されると、NIC を実行する初期処理を参照してください[PnP デバイスを追加するシステムを実行して](https://msdn.microsoft.com/library/windows/hardware/ff540535)します。

1.  PnP マネージャーがドライバーを読み込むし、呼び出してミニポート ドライバーの NIC のミニポート ドライバーが既に読み込まれていない場合[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff548818)関数。 ドライバーは既に読み込まれている場合は、手順 4 で処理が続行されます。

2.  その**DriverEntry**関数、ミニポート ドライバーは、ミニポート ドライバーとして登録し、その他のドライバーの初期化を実行します。 ミニポート ドライバーとして登録の詳細については、次を参照してください。[ミニポート ドライバーの初期化](initializing-a-miniport-driver.md)します。

3.  NDIS は、ミニポート ドライバーのドライバー オブジェクトに次のエントリを入力します。
    -   エントリ ポイント、 *AddDevice*ルーチン。
    -   *DispatchXxx* Irp を処理するためのエントリ ポイント。
    -   エントリ ポイント、*アンロード*ルーチン。

4.  PnP マネージャーには、NDIS の*AddDevice*ルーチン。 NDIS の*AddDevice*ルーチンは、新しく追加した NIC の機能のデバイス オブジェクト (FDO) を作成し、nic デバイス スタックにこの FDO をアタッチします。

5.  NDIS は、NIC の構成情報を取得するレジストリから情報を読み取ります この情報には、バインド情報、および NIC のハードウェア属性が含まれます。

6.  PnP マネージャーでは、必要な場合に、NIC にリソースを割り当てます。

 

 





