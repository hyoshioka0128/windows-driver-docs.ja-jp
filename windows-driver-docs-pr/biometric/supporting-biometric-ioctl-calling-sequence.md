---
title: 生体認証 IOCTL 呼び出しシーケンスのサポート
description: 生体認証 IOCTL 呼び出しシーケンスのサポート
ms.assetid: e6555895-8936-4f5d-8f2b-05b5283edbee
keywords:
- 生体認証ドライバー WDK、Ioctl をサポートしています。
- Ioctl WDK 生体認証をサポートしています。
- Ioctl WDK 生体認証
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91d6ac6f024310295e152932c3ed497e2efe2ed2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364678"
---
# <a name="supporting-biometric-ioctl-calling-sequence"></a>生体認証 IOCTL 呼び出しシーケンスのサポート


WBDI は、Windows の標準 IOCTL ベースのインターフェイスです。 WBDI ドライバーを記述するときに、必須の Ioctl のセットをサポートする必要があります。 さらに、省略可能な Ioctl をサポートできます。 必須およびオプションの Ioctl での完全な一覧を検索する[生体認証の Ioctl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

Windows 生体認証サービス (WBS) から次の順序で IOCTL 要求を受信するには、ベンダーから提供された WBDI ドライバーを準備する必要があります。 ハンドラーの例を確認するにはこれらの Ioctl で Device.cpp での[WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)します。

1.  Windows 生体認証サービスまたはセンサー アダプター、生体認証デバイスを初期化し、使用準備ができたことを確認します。 サービスまたはアダプターの送信、 [ **IOCTL\_生体認証の\_取得\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_get_attributes)要求。

    ドライバーへのポインターを受け取る、 [ **WINBIO\_センサー\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winbio_ioctl/ns-winbio_ioctl-_winbio_sensor_attributes)構造体。 この IOCTL のハンドラーで、ドライバーする必要がありますこの構造体の関連するメンバーを入力し、呼び出すことによって、要求を完了[ **IWDFIoRequest::Complete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-complete)します。

2.  ドライバーを次に、受信[ **IOCTL\_生体認証の\_取得\_センサー\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_get_sensor_status)します。 ドライバーの関連するメンバーを入力する必要があります、 [ **WINBIO\_診断**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winbio_ioctl/ns-winbio_ioctl-_winbio_diagnostics)構造体し、要求を完了します。

3.  場合は、ドライバーは、調整が必要であることを示します、 **SensorStatus**のメンバー、 [ **WINBIO\_診断**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winbio_ioctl/ns-winbio_ioctl-_winbio_diagnostics)から返された構造体IOCTL\_生体認証の\_取得\_センサー\_状態の要求、ドライバーを次に受信、 [ **IOCTL\_生体認証の\_調整** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_calibrate)要求。 ドライバーは、この IOCTL のハンドラーを用意する必要があります。 デバイスを調整するには、後に、コールバックが返す必要があります、 [ **WINBIO\_調整\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winbio_ioctl/ns-winbio_ioctl-_winbio_calibration_info)構造体。

4.  受信するドライバーが期待できるようになりました[ **IOCTL\_生体認証の\_キャプチャ\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_capture_data)要求。 1 つだけのキャプチャが保留されているため、いつでもこの要求のハンドラーをする必要がありますまず確認要求が保留中ないこと。 要求が保留中の場合は、完了 WINBIO で要求を\_E\_データ\_コレクション\_IN\_進行状況。

    WinBio サービスまたはアプリケーションなど、Win32 キャンセル ルーチンを呼び出すことによって、いつでも、未処理のキャプチャ要求のキャンセルを要求できます[ **CancelIo**](https://docs.microsoft.com/windows/desktop/FileIO/cancelio)、 [ **CancelIoEx**](https://docs.microsoft.com/windows/desktop/FileIO/cancelioex-func)、または[ **CancelSynchronousIo**](https://docs.microsoft.com/windows/desktop/FileIO/cancelsynchronousio-func)します。 そのため、WBDI ドライバーは、キャンセルもサポートする必要があります。

    ドライバーは、呼び出すことでキャンセルを処理[ **IWDFIoRequest::MarkCancelable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-markcancelable)を登録する、 [IRequestCallbackCancel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-irequestcallbackcancel)インターフェイス。

    ハンドラーは、キャプチャ モードのデバイスをプログラムし、コールバックを返します。 要求が保留状態のまま取り消されるまで、またはドライバーがキャプチャが完了したことを検出しました。 この I/O 要求を完了すると、デバイスがアイドル状態を取得できます。 クライアントは、IOCTL の最初の呼び出しを行う可能性があります\_生体認証の\_キャプチャ\_データを実際のキャプチャの適切なバッファー サイズを決定します。

5.  ハンドラーは[ **IOCTL\_生体認証の\_リセット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_reset)既知のまたはアイドル状態にデバイスを物理的にリセットする必要があります。 この要求のハンドラーのデータ収集の I/O の保留中の取り消しし、記入する必要がありますも、 [ **WINBIO\_空白\_ペイロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winbio_ioctl/ns-winbio_ioctl-_winbio_blank_payload)構造体。 ハンドラーは、要求を完了します。 クライアントは、IOCTL 呼び出しの間でリセットを呼び出す必要はありません\_生体認証の\_キャプチャ\_データ。

 

 





