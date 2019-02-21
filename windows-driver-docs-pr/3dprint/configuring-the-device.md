---
title: デバイスを構成します。
description: デバイスを構成するには、デバイスとプリンターのコントロール パネルでの 3D プリンター デバイスが必要し、G-Microsoft スライサーを使用して、コードを印刷できます。
ms.assetid: 897081C3-47A4-46A0-9A45-A49E4569216D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39f4fc78da8cb0a8d4e282f2bf1b261d35e84d8f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530605"
---
# <a name="configuring-the-device"></a>デバイスを構成します。


デバイスを構成するを 3D プリンター デバイスを含めるか、**デバイスとプリンター**コントロール パネルと G-Microsoft スライサーを使用して、コードを印刷できます。

次に、スライサーを変更する必要があり、詳細構成ファイルで設定します。

プリンターのプロパティとスライサーの設定を制御する 2 つの構成ファイルがあります。

ハードウェア デバイスに印刷する場合。 

- **C:\\Windows\\System32\\MS3DPrint\\StandardGCode\*します。XML** – これは StandardGCode.DLL によって使用されで定義されているレジストリのマッピングに応じて、デバイスを変更することができます、 **ConfigurationXML**下キー。

    - プリンター キュー: ごとHKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Enum\\3DPRINTER\\{PrinterName}\\{node}

    - ハードウェア ID:HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\Enum\\USB\\{VID & PID}\\{DeviceSerial}\\デバイスパラメーター\\

ファイル (USB ドライバーしません存在) で印刷する場合。

- **C:\\Windows\\System32\\スプール\\ドライバー\\x64\\3\\MS3DPrinterDeviceConfig.xml** – これは、グローバル、スライサーで使用します。

わかりやすくするため、編集、 **MS3DPrinterDeviceConfig.xml**ファイルとして、**管理者**を使用する場合、**ファイルへ出力**物理デバイスなしで関数を (G コード ファイル)接続されているし、編集**StandardGCode.XML**物理デバイスに印刷する場合。

これで整いました 3d 印刷 Windows、またはストアでは、3 D のビルダー app などのアプリケーションまたは Windows のネイティブ 3D 印刷を実装するデスクトップ アプリケーションから。

 

 




