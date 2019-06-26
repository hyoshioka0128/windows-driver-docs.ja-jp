---
title: HwScsiFindAdapter に対する HwContext ポインターの正しい使用
description: HwScsiFindAdapter に対する HwContext ポインターの正しい使用
ms.assetid: 9f287989-423b-4084-bf18-8df8676f7123
keywords:
- SCSI ミニポート ドライバー WDK 記憶域、PnP
- PnP WDK SCSI
- プラグ アンド プレイ WDK SCSI
- SCSI ミニポート ドライバーに変換します。
- HwContext ポインター
- HwScsiFindAdapter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14d508b1e9b6ab2e9e8c948dfca33fd1ad7b3c3a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386801"
---
# <a name="use-the-hwcontext-pointer-to-hwscsifindadapter-correctly"></a>HwScsiFindAdapter に対する HwContext ポインターの正しい使用


## <span id="ddk_use_the_hwcontext_pointer_to_hwscsifindadapter_correctly_kg"></span><span id="DDK_USE_THE_HWCONTEXT_POINTER_TO_HWSCSIFINDADAPTER_CORRECTLY_KG"></span>


ミニポート ドライバーの場合[ *HwScsiFindAdapter* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))が 0 以外のアクセスの範囲の値を受信ポート、ドライバーからそれを使用しないでください、 *HwContext*ポインター。 この制限は、バージョン 4.0 のミニポート ドライバーにも適用されて、このポインターを使用してからのミニポート ドライバーがこのような何もできません。

使用する必要がありますいない場合は、ミニポート ドライバーは、Microsoft Windows 2000 以降のプラグ アンド プレイ ドライバーとして初期化できますが、 *HwContext*ポインターで渡されるから、SCSI ポート ドライバー、 **NULL**ポインターとして、*HwContext*引数。

既存のミニポート ドライバーをどのように変更する必要が現在使用してどのように異なります*HwContext*します。 たとえば、ミニポート ドライバーを使用して*HwContext* Hba のカウントを保持する (例で使用する**DebugPrint**ステートメント) を使用する別の方法があります、 *HwDeviceExtension*ポインター代わりにします。 *HwDeviceExtension*特定の HBA に関連付けられている一意の番号を提供します。 送信元、 **DebugPrint**メッセージ。 (グローバル変数を使用して、HBA の数を格納するが不適切な手法では、ミニポート ドライバーには、状態情報を維持するためにグローバル変数は使用しないでください。)

4\.0、ミニポート ドライバーのバージョンで使用する場合、別の例として*HwContext* (PCI HBA の特定のモデルでサポートされている機能についての情報などの初期化中のデバイスの種類に関する情報をやり取り)、バージョン 5.0、ミニポート ドライバーの使用[ **ScsiPortGetBusData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetbusdata)に HBA の識別子を取得するを適切な場合は、このようなパラメーター ブロックの一覧を検索し、その識別子を使用情報。

もう 1 つの考えられるミニポート ドライバーの変更が渡されるレジストリの文字列でこの情報を提供することがあります、*引き*パラメーター。 レジストリの文字列は、検出されたカードのモデルに関連する情報を初期化中に、ミニポート ドライバーの INF ファイルで設定できます。 ユーザーがこのようなミニポート ドライバーが再コンパイルするミニポート ドライバーを必要とするのではなく、更新された INF ファイルを使用してカードの新しいモデルを処理できるため、ミニポート ドライバーでは、パラメーターをハードコーディングするよりも柔軟この提供します。

 

 




