---
title: ドライバーのレジストリ キーの概要
description: ドライバーのレジストリ キーの概要
ms.assetid: ec1a21db-1a31-4041-941d-31156884ffae
keywords:
- レジストリ WDK KMDF
- レジストリ キー オブジェクト WDK KMDF
- フレームワーク ベースのドライバー WDK KMDF、レジストリ
- カーネル モード ドライバー WDK KMDF、レジストリ
- KMDF WDK、レジストリ
- カーネル モード ドライバー フレームワーク WDK、レジストリ
- パラメーターは、WDK KMDF をキーします。
- ソフトウェア キー WDK KMDF
- ドライバーは、WDK KMDF をキーします。
- ハードウェア キー WDK KMDF
- WDK KMDF キー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a073a037054dbff3642f8105c54a3a3112b75599
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371112"
---
# <a name="introduction-to-registry-keys-for-drivers"></a>ドライバーのレジストリ キーの概要


通常、ドライバーは、保存または特定のドライバーまたはデバイスに固有の情報にアクセスする、一連のシステム定義のレジストリ キーを使用します。 ドライバーは、次のレジストリ キーにアクセス可能性があります。

-   **パラメーター**キー

    ドライバーの**パラメーター**キーは、ドライバーの構成情報を含めることができます。 カーネル モード ドライバー フレームワーク (KMDF) ドライバーは、このキーにある、 [ **HKLM\\システム\\CurrentControlSet\\サービス**](https://docs.microsoft.com/windows-hardware/drivers/install/hklm-system-currentcontrolset-services-registry-tree)ドライバーの下のツリーサービスの名前。 ユーザー モード ドライバー フレームワーク (UMDF) ドライバーは、このキーにある、 **HKLM\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\サービス**ドライバーのサービス名の下のツリーです。 ドライバーのサブキーは、ドライバーのバイナリ ファイルのファイル名は、サービス名と異なる場合でも常に、ドライバーのサービスの名前を使用します。

    システムのドライバーの呼び出すと[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers) 、日常的なドライバーのパスに渡す、ドライバーの**サービス**ツリー。 ドライバーはこのパスを渡す必要があります[ **WdfDriverCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdrivercreate)します。 ドライバーが呼び出すことで、パスを取得するその後、 [ **WdfDriverGetRegistryPath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdrivergetregistrypath)、ドライバーを開くことがその**パラメーター**呼び出してキー [ **WdfDriverOpenParametersRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdriveropenparametersregistrykey)します。

    詳細については、**パラメーター**キーを参照してください[、HKLM\\システム\\CurrentControlSet\\サービス ツリー](https://docs.microsoft.com/windows-hardware/drivers/install/hklm-system-currentcontrolset-services-registry-tree)します。

-   ソフトウェア キー

    ドライバーのソフトウェア キーとも呼ばれますが、*ドライバー キー*レジストリには、各ドライバー ソフトウェア キーが含まれています。 レジストリにデバイスのクラスのすべての一覧が含まれていますされ、そのデバイス クラスのエントリの下に各ドライバーのソフトウェアのキーが存在します。 システムでは、そのソフトウェア キーの下には、各ドライバーに関する情報を格納します。

    ドライバーを呼び出すことができます[ **WdfFdoInitOpenRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitopenregistrykey)と[ **WdfDeviceOpenRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceopenregistrykey)そのソフトウェア キーを開けません。

    ソフトウェア キーの詳細については、次を参照してください。 [、HKLM\\システム\\CurrentControlSet\\コントロール ツリー](https://docs.microsoft.com/windows-hardware/drivers/install/hklm-system-currentcontrolset-control-registry-tree)します。

-   ハードウェア キー

    ドライバー スタックは、プラグ アンド プレイ (PnP) マネージャーを通知し、デバイスがシステムに接続されていること、PnP マネージャーは、デバイスのハードウェア キーを作成します。 このキーとも呼ばれますが、*デバイス キー*します。 PnP マネージャーでは、デバイスのハードウェア キーの下の各デバイスの一意な識別情報を格納します。

    ドライバーを呼び出すことができます[ **WdfFdoInitOpenRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitopenregistrykey)と[ **WdfDeviceOpenRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceopenregistrykey)デバイスのハードウェア キーを開けません。

    ハードウェア キーの詳細については、次を参照してください。 [、HKLM\\システム\\CurrentControlSet\\列挙ツリー](https://docs.microsoft.com/windows-hardware/drivers/install/hklm-system-currentcontrolset-enum-registry-tree)します。

ドライバーの INF ファイルに含めることができます[ **INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)レジストリ値を設定します。 INF ファイルを使用して、通常[ **INF DDInstall.HW セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)デバイスのハードウェア キーの下の情報を設定します。

ドライバーの種類によって、特定のレジストリ キーの下の情報を格納することが必要かどうかを確認するのには、このドキュメントの目次を使用して、ドライバーのデバイスの種類を説明するセクションを参照してください。

ドライバーのレジストリ キーの詳細についてを参照してください。

-   [レジストリ ツリーとキーの概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-registry-trees-and-keys)

-   [ドライバーでは、レジストリを使用します。](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-the-registry-in-a-driver)

 

 





