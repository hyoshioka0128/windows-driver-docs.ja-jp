---
title: SPB 接続周辺機器の接続 ID
description: ドライバーは、単純な周辺機器バス (SPB) 上の周辺機器に i/o 要求を送信する前に、デバイスへの論理接続を開く必要があります。
ms.assetid: 234B5858-5930-40AD-BE4C-4A774A809D10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b69c56f4ecd1ee5c7561e4b0830e6257037516c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842756"
---
# <a name="connection-ids-for-spb-connected-peripheral-devices"></a>SPB 接続周辺機器の接続 ID


ドライバーは、[単純な周辺機器バス](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))(SPB) 上の周辺機器に i/o 要求を送信する前に、デバイスへの論理接続を開く必要があります。 この接続を使用して、ドライバーは、デバイスとの間でデータを転送するための読み取り要求と書き込み要求を送信できます。 さらに、ドライバーは、デバイスに i/o 制御 (IOCTL) 要求を送信して、SPB 固有の操作を実行できます。




システムの起動時に、プラグアンドプレイ (PnP) マネージャーは、PnP デバイスと非 PnP デバイスの両方を列挙します。 SP 1 に固定接続されている PnP 以外の周辺機器の場合、PnP マネージャーは、ハードウェアプラットフォームの ACPI ファームウェアに問い合わせて、デバイスへのアクセス方法を説明する一連の接続パラメーターを取得します。 これらの接続パラメーターは、デバイスが接続されているバスの SPB コントローラーを識別し、コントローラーがデバイスとの通信に必要とする他の情報 (バスアドレスやバスクロック周波数など) を含めます。

PnP マネージャーは、*接続 ID*と呼ばれる識別子を、SPB に接続されている周辺機器の接続パラメーターに割り当てます。 PnP マネージャーは、この ID と接続パラメーターを、*リソースハブ*と呼ばれるシステムデータストアに格納します。 (リソースハブは、SPB に接続されている周辺機器に関する構成情報を PnP マネージャーが格納する内部データストアです)。接続 ID は、ドライバーが明示的に指定する必要がないように、これらのパラメーターをカプセル化します。

SPB に接続されている周辺機器のドライバーは、ドライバーに割り当てられたハードウェアリソースの一部として、デバイスの接続 ID を受け取ります。 周辺機器のドライバーがシステム関数を呼び出してデバイスへの接続を開くと、ドライバーは接続 ID を提供します。この ID は、関数がリソースハブからデバイスの接続パラメーターを取得するために使用します。

ドライバー開発者は、[ユーザーモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf)(UMDF) または[カーネルモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)(kmdf) のいずれかを使用して、SPB に接続された周辺機器用のドライバーを構築できます。 フレームワークがドライバーの[**IPnpCallbackHardware2:: On hardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)メソッドを呼び出すと、UMDF ドライバーはそのリソース (接続 ID を含む) を受け取ります。 KMDF ドライバーは、 [*Evtdevicepreparehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック中にハードウェアリソースを受け取ります。

UMDF 周辺機器ドライバーがリソースリスト内の接続 Id を受信できるようにするには、ドライバーをインストールする INF ファイルで、WDF 固有の**Ddinstall**セクションに次のディレクティブを含める必要があります。

**UmdfDirectHardwareAccess = AllowDirectHardwareAccess**このディレクティブの詳細については、「 [INF ファイルでの WDF ディレクティブの指定](https://docs.microsoft.com/windows-hardware/drivers/wdf/specifying-wdf-directives-in-inf-files)」を参照してください。 このディレクティブを使用する INX ファイル (対応する INF ファイルのビルドに使用) の例については、 [SpbAccelerometer](https://go.microsoft.com/fwlink/p/?LinkId=618052) driver サンプルを参照してください。

ドライバーがリソースとして受信する接続 ID は64ビットの整数ですが、ドライバーは、リソースハブから接続パラメーターを取得するために使用できるデバイスパス名にこの ID を組み込む必要があります。 デバイスパス名を作成するために、ドライバーは**リソース\_ハブを呼び出し\_\_ID 関数から\_パス\_を作成**します。これは、Reshub ヘッダーファイルで宣言されています。

SPB 接続周辺機器への論理接続を開くには、UMDF ドライバーは[**Iwdfremotetarget:: OpenFileByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-openfilebyname)メソッドを呼び出し、kmdf ドライバーは[**WdfIoTargetOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)メソッドを呼び出します。 どちらの方法でも、デバイスパス名を入力パラメーターとして指定する必要があります。

接続 Id を使用して SPB 接続周辺機器への論理接続を開く、UMDF と KMDF のコード例については、次のトピックを参照してください。

[ユーザーモードの周辺機器ドライバーのハードウェアリソース](https://docs.microsoft.com/windows-hardware/drivers/spb/hardware-resources-for-user-mode-spb-peripheral-drivers)[カーネルモード spb 周辺機器のドライバー](https://docs.microsoft.com/windows-hardware/drivers/spb/hardware-resources-for-kernel-mode-spb-peripheral-drivers)
ユーザーモードアプリケーションが、SPB に接続されている周辺機器への論理接続を開くことができません。 i/o を送信することはできません。これらのデバイスに直接要求します。

1つのドライバーのみが、SPB に接続されている周辺機器への開いている論理接続を保持できます。 別のドライバーによる同じデバイスへの2番目の接続を開こうとして失敗します。

 

 




