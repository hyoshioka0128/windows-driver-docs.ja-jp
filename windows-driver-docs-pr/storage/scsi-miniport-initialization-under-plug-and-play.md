---
title: プラグ アンド プレイでの SCSI ミニポートの初期化
description: プラグ アンド プレイでの SCSI ミニポートの初期化
ms.assetid: bf2f9809-8271-4f0f-a2c4-25127fe9c4aa
keywords:
- SCSI ミニポート ドライバー WDK 記憶域、PnP
- PnP WDK SCSI
- プラグ アンド プレイ WDK SCSI
- SCSI ミニポート ドライバーの初期化
- SCSI ミニポート ドライバー WDK のストレージの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92c3eac06cffafee1101168a74eb86a21c053e02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580724"
---
# <a name="scsi-miniport-initialization-under-plug-and-play"></a>プラグ アンド プレイでの SCSI ミニポートの初期化


## <span id="ddk_scsi_miniport_initialization_under_plug_and_play_kg"></span><span id="DDK_SCSI_MINIPORT_INITIALIZATION_UNDER_PLUG_AND_PLAY_KG"></span>


Windows 2000 以降では、従来のミニポート ドライバーが Microsoft Windows NT 4.0 の場合とまったく同じ方法で初期化されます。 従来のミニポート ドライバーを呼び出すと[ **ScsiPortInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff564645)、ポート ドライバー呼び出しミニポート ドライバーを見つけてその HBA を初期化します。 これは、各 hba (、HBA が列挙可能なバス上にある場合) が見つかるまたは繰り返しミニポート ドライバーは、他のデバイスが見つからないことを報告するまでに実行されます。 ミニポート ドライバーの返しますの制御[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff552654)ミニポート ドライバーを呼び出すことができます、ルーチン**ScsiPortInitialize**別の種類 (の HBA の用にもう一度別のインターフェイスまたはなど、さまざまなベンダーと製品 ID)。 ミニポート ドライバーのコンテキストで行われるすべての初期化呼び出し**DriverEntry**ルーチンとは、順序で作成する**ScsiPortInitialize**が呼び出されました。 従来のドライバーの初期化には、システムの起動時とその他のことはありませんが発生します。

プラグ アンド プレイでは、初期化の順序を保持することはできません。 プラグ アンド プレイの呼び出しが有効になっているミニポート ドライバーと**ScsiPortInitialize**、ポート ドライバーは、今後の参考として初期化データを保存し、ステータスを返します\_成功します。 ミニポート ドライバーの記載されているインターフェイスの種類ごとにこれは、 **PnPInterface** --すべてのインターフェイスのレジストリ キー*いない*そのキーに示されてはすぐに初期化もします。

後で、プラグ アンド プレイ マネージャーは、ミニポート ドライバーの HBA を検出すると、ポートのドライバーを通知します。 ポート ドライバー (メモリ、ミニポート ドライバーのデバイスの拡張機能用) などのために必要なシステム リソースの割り当てし、HBA を検索するミニポート ドライバーを呼び出すし、それを初期化します。 これは通常、システムの起動時に行いますが、ドッキング操作またはなど、CardBus HBA がシステムにホット接続の場合、システムを検出したときにも発生可能性があります。

デバイスに、プラグ アンド プレイ manager デバイスを報告するまでに、(など、I/O ポート、メモリ アドレス、および割り込み) バス リソースに割り当てられますが既にその*とそのデバイスを単独で*します。 これらのリソースは、これらのリソースを使用して、またはデバイスが見つからなかったことを報告する必要がありますミニポート ドライバーに提供されます。 具体的には、ミニポート ドライバーは、ポートやデバイスを検索するためのもの以外のメモリの場所にアクセスする必要がありますしません。

プラグ アンド プレイ ドライバーが nonenumerable バス上にあるデバイスを検出するために求められる場合が、開始されたミニポート ドライバー。 これには、ミニポート ドライバーの問題の HBA を検索するバスにコマンドを必要とするバス ISA などが含まれます。 このような検出中にあるデバイスはレジストリに記録し、次回システムを起動するときにプラグ アンド プレイ デバイスとして初期化します。

プラグ アンド プレイの詳細については、次を参照してください。[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)します。

 

 




