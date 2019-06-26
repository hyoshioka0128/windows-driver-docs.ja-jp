---
title: フレームワークでサポートされていない IRP の処理
description: フレームワークでサポートされていない IRP の処理
ms.assetid: 0481f335-f63b-4f93-8eb4-523a70082302
keywords:
- サポートされていない WDM Irp の WDK KMDF
- Irp WDK KMDF、サポートされていません
- WDM Irp の WDK KMDF、サポートされていません
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2808940a38a5300eb50fbd7ba4b44ff61077917a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382863"
---
# <a name="handling-an-irp-that-the-framework-does-not-support"></a>フレームワークでサポートされていない IRP の処理


\[KMDF にのみ適用されます。\]

フレームワークは、次の主要な IRP のコードの I/O 要求をサポートしません。

-   IRP\_MJ\_作成\_"メール スロット"
-   IRP\_MJ\_作成\_名前付き\_パイプ
-   IRP\_MJ\_デバイス\_変更
-   [**IRP\_MJ\_ディレクトリ\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-directory-control)
-   [**IRP\_MJ\_ファイル\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-file-system-control)
-   [**IRP\_MJ\_フラッシュ\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)
-   [**IRP\_MJ\_ロック\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-lock-control)
-   [**IRP\_MJ\_クエリ\_EA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-ea)
-   [**IRP\_MJ\_クエリ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-information)
-   [**IRP\_MJ\_クエリ\_クォータ**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-quota)
-   [**IRP\_MJ\_QUERY\_SECURITY**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-security)
-   [**IRP\_MJ\_クエリ\_ボリューム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-volume-information)
-   [**IRP\_MJ\_SET\_EA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-ea)
-   [**IRP\_MJ\_SET\_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-set-information)
-   [**IRP\_MJ\_SET\_QUOTA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-quota)
-   [**IRP\_MJ\_SET\_SECURITY**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-security)
-   [**IRP\_MJ\_設定\_ボリューム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-volume-information)

フレームワークは、これらの I/O 関数コードのいずれかを含む IRP を受信する場合、フレームワークは IRP を処理しません。 ドライバーが、フィルター ドライバーの場合は、フレームワークは、次の下位ドライバーはドライバー スタックに IRP を渡します。 ドライバーでない場合、フィルター ドライバー、フレームワーク[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)状態のステータス値を持つ IRP の完了に\_無効な\_デバイス\_要求します。

ドライバーを呼び出す必要があります、ドライバーでは、これらの I/O 関数コードのいずれかが含まれている Irp を処理する必要がある場合[ **WdfDeviceInitAssignWdmIrpPreprocessCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback)を登録する、 [ *EvtDeviceWdmIrpPreprocess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess) I/O 関数のコードのイベントのコールバック関数。

ドライバーがドライバーに登録されている I/O 関数コードを含む IRP を受信すると、 [ *EvtDeviceWdmIrpPreprocess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)コールバックに framework パス IRP のコールバック関数関数。 コールバック関数に従って IRP を処理する必要がありますし、 [WDM Irp の取り扱いルール](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)します。 ドライバーを呼び出す必要があります[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)完了、IRP も呼び出す必要があります[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) IRP を次の下位に渡すドライバー。

例については、 [ *EvtDeviceWdmIrpPreprocess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)フレームワークがサポートされていない IRP を処理するコールバック関数を参照してください、[シリアル](sample-kmdf-drivers.md)サンプル ドライバー。

 

 





