---
title: ストレージ ミニポート ドライバーの WMI される Srb の処理
description: ストレージ ミニポート ドライバーの WMI される Srb の処理
ms.assetid: 92b78611-7e6f-4d77-9133-635df96584f0
keywords:
- ストレージ ミニポート ドライバー WDK、WMI される Srb
- WMI される Srb のミニポート ドライバー WDK ストレージ
- WMI される Srb についての WMI される Srb WDK ストレージ
- WMI される Srb WDK ストレージ
- SRB の WMI のサポートを WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fde44f7cd85051cd993054daa3bb3629508af880
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550275"
---
# <a name="handling-wmi-srbs-in-storage-miniport-drivers"></a>ストレージ ミニポート ドライバーの WMI される Srb の処理


## <span id="ddk_handling_wmi_srbs_in_storage_miniport_drivers_kg"></span><span id="DDK_HANDLING_WMI_SRBS_IN_STORAGE_MINIPORT_DRIVERS_KG"></span>


WMI は、ホスト バス アダプター (HBA) に関する情報を報告するをインターフェイスまたは HBA の記憶域ミニポート ドライバーとの対話、通常は WMI プロバイダとして機能するミニポート ドライバーを必要とする WMI クライアントを使用できます。 ストレージ ミニポート ドライバーは、WMI プロバイダーとして登録して後の SCSI 要求ブロック (SRB) の Windows Management Instrumentation (WMI) の SCSI 要求のブロックと呼ばれる特殊なを処理する準備する必要があります ([**SCSI\_WMI\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff565397))。

WMI される Srb を処理するために、記憶域ミニポート ドライバーを準備するには、次の手順を完了します。

1.  デザインし、システム提供の MOF ファイルで定義されていない WMI スキーマの部分を説明する管理オブジェクト フォーマット (MOF) ファイルをコンパイルします。

    MOF 構文については、[WMI データとイベント ブロックの MOF 構文](https://msdn.microsoft.com/library/windows/hardware/ff556400)を参照してください。

2.  ミニポート ドライバー コールバック ルーチンを実装します。

    SCSI ポート WMI ライブラリには、WMI される Srb のミニポート ドライバーの処理が簡略化します。 SCSI ポート WMI ライブラリを使用して、実装、 *HwScsiWmiXxx*で説明されているコールバック ルーチン[SCSI ミニポート ドライバー ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff565312)します。

3.  ミニポート ドライバーに必要なコードを追加[ **SCSI ミニポート ドライバーの DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff552654)ルーチン。

4.  ミニポート ドライバーに必要なコードを追加[ *HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300)ルーチン。

5.  ミニポート ドライバーに必要なコードを追加[ **HwScsiStartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557323)ルーチン。

前の手順を実装する方法の詳細については、このセクションで、次のトピックを参照してください。

[ポートのドライバーが WMI 要求を処理する方法](how-the-port-driver-processes-wmi-requests.md)

[SCSI ポート WMI ライブラリの使用](using-the-scsi-port-wmi-library.md)

[設計の WMI のミニポート ドライバー コールバック ルーチン](designing-wmi-miniport-driver-callback-routines.md)

[WMI される Srb をサポートする記憶域ミニポート ドライバー、ルーチンの変更](modifying-storage-miniport-driver-routines-to-support-wmi-srbs.md)

 

 




