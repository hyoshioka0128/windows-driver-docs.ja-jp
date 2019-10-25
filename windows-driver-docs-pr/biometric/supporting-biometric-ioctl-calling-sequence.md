---
title: 生体認証 IOCTL 呼び出しシーケンスのサポート
description: 生体認証 IOCTL 呼び出しシーケンスのサポート
ms.assetid: e6555895-8936-4f5d-8f2b-05b5283edbee
keywords:
- 生体認証ドライバー WDK、Ioctl のサポート
- Ioctl WDK 生体認証のサポート
- Ioctl WDK 生体認証
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49719c03fd32e24fab86c46d0fa8ced51bf327d3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832213"
---
# <a name="supporting-biometric-ioctl-calling-sequence"></a>生体認証 IOCTL 呼び出しシーケンスのサポート


WBDI は、Windows の標準の IOCTL ベースのインターフェイスです。 WBDI ドライバーを作成する場合は、一連の必須 Ioctl をサポートする必要があります。 また、オプションの Ioctl をサポートするように選択することもできます。 必須の Ioctl と省略可能な Ioctl の完全な一覧については、「[生体認証 ioctl](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

ベンダーから提供された WBDI ドライバーは、Windows 生体認証サービス (WBS) から次の順序で IOCTL 要求を受け取るように準備する必要があります。 これらの Ioctl のハンドラーの例は、 [WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)のデバイス .cpp で確認できます。

1.  Windows 生体認証サービスまたはセンサーアダプターは、生体認証デバイスを初期化し、使用できる状態であることを確認します。 サービスまたはアダプターは、 [**IOCTL\_生体認証\_GET\_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_get_attributes)要求を送信します。

    ドライバーは、 [**Winbio\_センサー\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winbio_ioctl/ns-winbio_ioctl-_winbio_sensor_attributes)構造へのポインターを受け取ります。 この IOCTL のハンドラーでは、ドライバーはこの構造体の関連するメンバーを入力し、 [**IWDFIoRequest:: complete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete)を呼び出すことによって要求を完了する必要があります。

2.  次に、ドライバーは[**IOCTL\_生体認証\_受信し\_センサー\_の状態を取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_get_sensor_status)します。 ドライバーは、 [**Winbio\_診断**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winbio_ioctl/ns-winbio_ioctl-_winbio_diagnostics)構造の関連するメンバーに入力し、要求を完了する必要があります。

3.  ドライバーが、IOCTL\_生体認証によって返された[**Winbio\_診断**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winbio_ioctl/ns-winbio_ioctl-_winbio_diagnostics)構造の**sensorstatus**メンバーで調整が必要であることが示された場合、\_\_センサー\_状態要求を取得します。次に、ドライバーは[**IOCTL\_生体認証\_調整**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_calibrate)要求を受信します。 ドライバーは、この IOCTL のハンドラーを提供する必要があります。 デバイスを調整した後、コールバックは[**Winbio\_調整\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winbio_ioctl/ns-winbio_ioctl-_winbio_calibration_info)構造体を返す必要があります。

4.  ドライバーは、\_データ要求を[**キャプチャ\_IOCTL\_生体認証**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_capture_data)を受け取ることが予想されるようになりました。 いつでも1つのキャプチャしか保留できないため、この要求のハンドラーは、要求が保留中でないことを最初に確認する必要があります。 要求が保留中の場合は、\_の進行状況で\_データ\_コレクション\_の WINBIO\_E の要求を完了します。

    WinBio サービスまたはアプリケーションは、 [**CancelIo**](https://docs.microsoft.com/windows/desktop/FileIO/cancelio)、 [**cancelioex**](https://docs.microsoft.com/windows/desktop/FileIO/cancelioex-func)、 [**CancelSynchronousIo**](https://docs.microsoft.com/windows/desktop/FileIO/cancelsynchronousio-func)などの Win32 キャンセルルーチンを呼び出すことによって、未処理のキャプチャ要求の取り消しをいつでも要求できます。 そのため、WBDI ドライバーはキャンセルもサポートする必要があります。

    ドライバーは[**IWDFIoRequest:: Markcancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-markcancelable)を呼び出して、 [irequest cancel](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-irequestcallbackcancel)インターフェイスを登録することで、取り消し処理を行います。

    次に、ハンドラーはデバイスでキャプチャモードをプログラムし、コールバックから制御を戻します。 要求は取り消されるか、またはドライバーによってキャプチャが完了したことが検出されるまで保留のままになります。 この i/o 要求が完了すると、デバイスはアイドル状態に戻ることができます。 クライアントは、IOCTL\_生体認証\_最初の呼び出しを行って\_データをキャプチャし、実際のキャプチャの正しいバッファーサイズを決定することができます。

5.  [**IOCTL\_生体認証\_リセット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_reset)のハンドラーは、デバイスを物理的に既知またはアイドル状態にリセットする必要があります。 また、この要求のハンドラーは、保留中のデータコレクション i/o をキャンセルし、 [**Winbio\_空白\_ペイロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winbio_ioctl/ns-winbio_ioctl-_winbio_blank_payload)構造を入力する必要があります。 次に、ハンドラーが要求を完了します。 クライアントは、IOCTL\_生体認証\_の呼び出しの間で reset を呼び出す必要はありません\_データをキャプチャします。

 

 





