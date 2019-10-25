---
title: フレームワークでサポートされていない IRP の処理
description: フレームワークでサポートされていない IRP の処理
ms.assetid: 0481f335-f63b-4f93-8eb4-523a70082302
keywords:
- サポートされていない WDM Irp WDK KMDF
- Irp WDK KMDF、サポートされていません
- WDM Irp WDK KMDF、サポートされていません
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 520878652f5e5fad65476c6ea266b0e816292b61
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844429"
---
# <a name="handling-an-irp-that-the-framework-does-not-support"></a>フレームワークでサポートされていない IRP の処理


\[は KMDF にのみ適用され\]

フレームワークでは、次の主要な IRP コードを含む i/o 要求はサポートされていません。

-   \_メールスロットを作成\_IRP\_MJ
-   IRP\_MJ\_\_パイプ\_名前を作成します
-   IRP\_MJ\_デバイス\_変更
-   [**IRP\_MJ\_DIRECTORY\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-directory-control)
-   [**IRP\_MJ\_ファイル\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-file-system-control)
-   [**IRP\_MJ\_フラッシュ\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)
-   [**IRP\_MJ\_ロック\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-lock-control)
-   [**IRP\_MJ\_クエリ\_EA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-ea)
-   [**IRP\_MJ\_クエリ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-information)
-   [**IRP\_MJ\_クエリ\_クォータ**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-quota)
-   [**IRP\_MJ\_クエリ\_セキュリティ**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-security)
-   [**IRP\_MJ\_クエリ\_ボリューム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-volume-information)
-   [**IRP\_MJ\_設定\_EA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-ea)
-   [**IRP\_MJ\_設定\_情報**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-set-information)
-   [**IRP\_MJ\_設定\_クォータ**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-quota)
-   [**IRP\_MJ\_設定\_セキュリティ**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-security)
-   [**IRP\_MJ\_\_ボリューム\_情報の設定**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-volume-information)

これらの i/o 関数コードのいずれかを含む IRP がフレームワークによって受信された場合、フレームワークは IRP を処理しません。 ドライバーがフィルタードライバーである場合、フレームワークは IRP をドライバースタック内の次の下位のドライバーに渡します。 ドライバーがフィルタードライバーでない場合、フレームワークは[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出して、状態の値\_無効\_デバイス\_要求で IRP を完了します。

ドライバーが、これらの i/o 関数コードを含む Irp を処理する必要がある場合、ドライバーは[**Wdfdeviceinit割り当て Wdmirpq Preprocesscallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback)を呼び出して、i/o 関数コードの[*Evtdevicewdmiの*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)イベントコールバック関数を登録する必要があります。

ドライバーが、に対して[*Evtdevicewdmirppreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)関数を登録したことを示す i/o 関数コードを含む irp を受信すると、フレームワークはその irp をコールバック関数に渡します。 次に、 [irp を処理する WDM ルール](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)に従って、このコールバック関数が irp を処理する必要があります。 ドライバーは、IRP を完了するために[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出す必要があります。または、irp を次の下位のドライバーに渡すには、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出す必要があります。

フレームワークがサポートしていない IRP を処理する[*Evtdevicewdmi、前処理*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)コールバック関数の例については、[シリアル](sample-kmdf-drivers.md)サンプルドライバーを参照してください。

 

 





