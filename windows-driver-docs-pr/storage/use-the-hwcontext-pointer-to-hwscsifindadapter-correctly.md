---
title: HwScsiFindAdapter に対する HwContext ポインターの正しい使用
description: HwScsiFindAdapter に対する HwContext ポインターの正しい使用
ms.assetid: 9f287989-423b-4084-bf18-8df8676f7123
keywords:
- SCSI ミニポートドライバー WDK 記憶域、PnP
- PnP WDK SCSI
- WDK SCSI のプラグアンドプレイ
- SCSI ミニポートドライバーの変換
- HwContext ポインター
- HwScsiFindAdapter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 213c4150ce5f5ebce61e56993711891781804ed9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840327"
---
# <a name="use-the-hwcontext-pointer-to-hwscsifindadapter-correctly"></a>HwScsiFindAdapter に対する HwContext ポインターの正しい使用


## <span id="ddk_use_the_hwcontext_pointer_to_hwscsifindadapter_correctly_kg"></span><span id="DDK_USE_THE_HWCONTEXT_POINTER_TO_HWSCSIFINDADAPTER_CORRECTLY_KG"></span>


ミニポートドライバーの[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))がポートドライバーから0以外のアクセス範囲値を受け取った場合、 *HwContext*ポインターを使用することはできません。 この制限はバージョン4.0 ミニポートドライバーにも適用されていますが、このようなミニポートドライバーがこのポインターを使用することはできませんでした。

ミニポートドライバーを Microsoft Windows 2000 以降のプラグアンドプレイドライバーとして初期化できる場合、SCSI ポートドライバーが*HwContext*引数として**NULL**ポインターを渡すため、 *HwContext*ポインターを使用してはなりません。

既存のミニポートドライバーを変更する方法は、現在*HwContext*をどのように使用しているかによって異なります。 たとえば、ミニポートドライバーで*HwContext*を使用して hba の数を管理している場合 (たとえば、 **debugprint**ステートメントでを使用する場合)、代わりに*HwDeviceExtension*ポインターを使用する方法があります。 *HwDeviceExtension*は、 **debugprint**メッセージを発信した特定の HBA に関連する一意の番号を提供します。 (HBA 数を格納するためにグローバル変数を使用するのは不適切な方法です。ミニポートドライバーでは、グローバル変数を使用して状態情報を維持する必要がないためです)。

もう1つの例として、4.0 バージョンのミニポートドライバーで*HwContext*を使用して、初期化されるデバイスの種類に関する情報 (PCI HBA の特定のモデルでサポートされている機能に関する情報など) を通信する場合、5.0 バージョンのミニポートドライバーでは、 [**ScsiPortGetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetbusdata)を使用して HBA の識別子を取得し、その識別子を使用して、正しい情報を見つけるために、このようなパラメーターブロックの一覧を検索します。

もう1つの可能性のあるミニポートドライバーの変更は、 *argumentstring*パラメーターで渡されるレジストリ文字列にこの情報を提供することです。 検出されたカードのモデルに関連する情報への初期化中に、ミニポートドライバーの INF ファイルによってレジストリ文字列を設定できます。 これにより、ミニポートドライバーでパラメーターをハードコーディングするよりも柔軟性が向上します。このようなミニポートドライバーでは、ミニポートドライバーを再コンパイルしなくても、更新された INF ファイルを使用して新しいカードのモデルを処理する可能性があるためです。

 

 




