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
ms.openlocfilehash: 5b0eb09c81628c1e9072f1e062dc1dfb30f882af
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552121"
---
# <a name="introduction-to-registry-keys-for-drivers"></a>ドライバーのレジストリ キーの概要


通常、ドライバーは、保存または特定のドライバーまたはデバイスに固有の情報にアクセスする、一連のシステム定義のレジストリ キーを使用します。 ドライバーは、次のレジストリ キーにアクセス可能性があります。

-   **パラメーター**キー

    ドライバーの**パラメーター**キーは、ドライバーの構成情報を含めることができます。 カーネル モード ドライバー フレームワーク (KMDF) ドライバーは、このキーにある、 [ **HKLM\\システム\\CurrentControlSet\\サービス**](https://msdn.microsoft.com/library/windows/hardware/ff546188)ドライバーの下のツリーサービスの名前。 ユーザー モード ドライバー フレームワーク (UMDF) ドライバーは、このキーにある、 **HKLM\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\サービス**ドライバーのサービス名の下のツリーです。 ドライバーのサブキーは、ドライバーのバイナリ ファイルのファイル名は、サービス名と異なる場合でも常に、ドライバーのサービスの名前を使用します。

    システムのドライバーの呼び出すと[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff540807) 、日常的なドライバーのパスに渡す、ドライバーの**サービス**ツリー。 ドライバーはこのパスを渡す必要があります[ **WdfDriverCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547175)します。 ドライバーが呼び出すことで、パスを取得するその後、 [ **WdfDriverGetRegistryPath**](https://msdn.microsoft.com/library/windows/hardware/ff547187)、ドライバーを開くことがその**パラメーター**呼び出してキー [ **WdfDriverOpenParametersRegistryKey**](https://msdn.microsoft.com/library/windows/hardware/ff547202)します。

    詳細については、**パラメーター**キーを参照してください[、HKLM\\システム\\CurrentControlSet\\サービス ツリー](https://msdn.microsoft.com/library/windows/hardware/ff546188)します。

-   ソフトウェア キー

    ドライバーのソフトウェア キーとも呼ばれますが、*ドライバー キー*レジストリには、各ドライバー ソフトウェア キーが含まれています。 レジストリにデバイスのクラスのすべての一覧が含まれていますされ、そのデバイス クラスのエントリの下に各ドライバーのソフトウェアのキーが存在します。 システムでは、そのソフトウェア キーの下には、各ドライバーに関する情報を格納します。

    ドライバーを呼び出すことができます[ **WdfFdoInitOpenRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff547249)と[ **WdfDeviceOpenRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff546804)そのソフトウェア キーを開けません。

    ソフトウェア キーの詳細については、[、HKLM\\システム\\CurrentControlSet\\コントロール ツリー](https://msdn.microsoft.com/library/windows/hardware/ff546165)を参照してください。

-   ハードウェア キー

    ドライバー スタックは、プラグ アンド プレイ (PnP) マネージャーを通知し、デバイスがシステムに接続されていること、PnP マネージャーは、デバイスのハードウェア キーを作成します。 このキーとも呼ばれますが、*デバイス キー*します。 PnP マネージャーでは、デバイスのハードウェア キーの下の各デバイスの一意な識別情報を格納します。

    ドライバーを呼び出すことができます[ **WdfFdoInitOpenRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff547249)と[ **WdfDeviceOpenRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff546804)デバイスのハードウェア キーを開けません。

    ハードウェア キーの詳細については、[、HKLM\\システム\\CurrentControlSet\\列挙ツリー](https://msdn.microsoft.com/library/windows/hardware/ff546173)を参照してください。

ドライバーの INF ファイルに含めることができます[ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)レジストリ値を設定します。 INF ファイルを使用して、通常[ **INF DDInstall.HW セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547330)デバイスのハードウェア キーの下の情報を設定します。

ドライバーの種類によって、特定のレジストリ キーの下の情報を格納することが必要かどうかを確認するのには、このドキュメントの目次を使用して、ドライバーのデバイスの種類を説明するセクションを参照してください。

ドライバーのレジストリ キーの詳細についてを参照してください。

-   [レジストリ ツリーとキーの概要](https://msdn.microsoft.com/library/windows/hardware/ff549538)

-   [ドライバーでは、レジストリを使用します。](https://msdn.microsoft.com/library/windows/hardware/ff565537)

 

 





