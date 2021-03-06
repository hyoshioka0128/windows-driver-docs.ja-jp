---
title: センサーおよび位置情報プラットフォームのプライバシーとセキュリティ
description: センサーおよび位置情報プラットフォームのプライバシーとセキュリティ
ms.assetid: 9defb163-4de6-46cc-b817-d3e6291137be
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9b5733c443846a4990b112bcc7e50d9bf11be6f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363643"
---
# <a name="privacy-and-security-in-the-sensor-and-location-platform"></a>センサーおよび位置情報プラットフォームのプライバシーとセキュリティ

場所データは、情報は、特定のユーザーを識別する場合に特ににユーザーのプライバシーに関するに違反することができます。 ストリート アドレス、またはそれを決定する緯度と経度の座標は、個人を特定できる情報と見なされます。 ユーザーは、この種の情報を保護するコンピューター ソフトウェアを期待します。 ソフトウェア開発者の課題は、し、お客様のプライバシーを侵害せずに必要な機能をユーザーに提供する方法です。

## <a name="privacy-and-security-controls"></a>プライバシーとセキュリティ制御

Windows で sensor and location プラットフォームは、場所データがプライベートであることを確認する次の機能を提供します。

- Windows 8 では場所を有効にするための設定の 3 つの種類があります。 すべてのユーザー、ユーザーごとの設定を有効または場所を無効にする場所を無効にできる管理者用の設定は、UWP アプリの場合は、ユーザーがアプリごとの場所の設定を適用できます。 既定では、ユーザーごとの場所の設定はユーザーがコントロール パネルからデータにアクセスする明示的な同意を提供するまでになります。 Windows 8 での場所の設定の詳細については、次を参照してください。 [Location awareness](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation)します。

- Windows では、ユーザーに漏えいメッセージが提供されます。 これらのメッセージでは、ユーザーがどの場所データを使用してにより、個人を特定できる情報の漏えいを理解するのに役立ちます。

- Location API を使用してデスクトップ アプリを呼び出すことができます、 [ **RequestPermissions** ](https://docs.microsoft.com/windows/desktop/api/locationapi/nf-locationapi-ilocation-requestpermissions)メソッドの場所を有効にするユーザーの入力を求めるシステム ダイアログ ボックスを開きます。

- ドライバーの場所は、センサー クラスの拡張機能を使用します。 クラスの拡張機能はすべての I/O 要求を処理、ユーザーのアクセス許可があるプログラムだけが場所データにアクセスできることを確認します。

## <a name="keeping-user-data-private"></a>ユーザー データ プライベートのままの状態

センサー ドライバーを記述するときに、ユーザーのプライバシーを考慮する必要があります。 センサー クラスの拡張機能によって適用されるプライバシー制御をバイパスするには、しないことを確認しておく必要があります。 ユーザーがアクセス許可を付与する前に、特定のプロパティを取得できるため、ドライバーは、これらのプロパティは、個人情報は表示されませんか確認する必要があります。 ユーザーがアクセス許可を付与する前に使用できるプロパティの一覧は、次を参照してください。 [ **ISensorDriver::OnGetProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties)します。

## <a name="additional-resources"></a>その他のリソース

ユーザー プライバシーを保護するソフトウェアの開発に役立つ、次のリソースを確認します。

[ソフトウェアの製品やサービスを開発するための公開プライバシー ガイドライン](https://go.microsoft.com/fwlink/p/?linkid=2085300)

[TechNet セキュリティ デベロッパー センター](https://go.microsoft.com/fwlink/p/?linkid=237150)

## <a name="related-topics"></a>関連トピック

[アーキテクチャの概要](https://docs.microsoft.com/windows-hardware/drivers/sensors/architecture-overview)  

[センサー クラスの拡張機能について](https://docs.microsoft.com/windows-hardware/drivers/sensors/about-the-sensor-class-extension)  

[位置認識](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation)  
