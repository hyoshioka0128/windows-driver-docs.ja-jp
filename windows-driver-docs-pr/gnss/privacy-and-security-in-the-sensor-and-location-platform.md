---
title: センサーおよび位置情報プラットフォームのプライバシーとセキュリティ
description: センサーおよび位置情報プラットフォームのプライバシーとセキュリティ
ms.assetid: 9defb163-4de6-46cc-b817-d3e6291137be
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 240648fb548181304853fb8520158750cebbfaf6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825059"
---
# <a name="privacy-and-security-in-the-sensor-and-location-platform"></a>センサーおよび位置情報プラットフォームのプライバシーとセキュリティ

場所データは、特に情報が特定のユーザーを識別する場合に、ユーザーのプライバシーに違反することがあります。 市区町村、つまり、それを決定する緯度と経度の座標は、個人を特定できる情報と見なされます。 ユーザーは、この種の情報をセキュリティで保護するためにコンピューターソフトウェアを想定しています。 ソフトウェア開発者にとっての課題は、プライバシーに違反することなく、ユーザーが必要とする機能をユーザーに提供する方法を見つけることです。

## <a name="privacy-and-security-controls"></a>プライバシーとセキュリティの制御

Windows のセンサーと場所のプラットフォームには、場所データをプライベートに保つために、次の機能が用意されています。

- Windows 8 には、場所を有効にするための3種類の設定があります。 すべてのユーザー、場所を有効または無効にするユーザーごとの設定、UWP アプリの場所を無効にできる管理者向けの設定があります。 既定では、ユーザーごとの場所の設定は、ユーザーがコントロールパネルを使用してデータにアクセスするための明示的な同意を得るまではオフになっています。 Windows 8 での場所の設定の詳細については、「[場所の認識](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation)」を参照してください。

- Windows は、ユーザーに開示メッセージを提供します。 これらのメッセージは、ユーザーが場所データを使用して個人を特定できる情報を公開する方法を理解するのに役立ちます。

- Location API を使用するデスクトップアプリでは、 [**Requestpermissions**](https://docs.microsoft.com/windows/desktop/api/locationapi/nf-locationapi-ilocation-requestpermissions)メソッドを呼び出して、ユーザーに場所を有効にするように求めるシステムダイアログボックスを開くことができます。

- 場所ドライバーはセンサークラス拡張を使用します。 クラス拡張は、すべての i/o 要求を処理し、ユーザーのアクセス許可を持つプログラムのみが位置情報にアクセスできるようにします。

## <a name="keeping-user-data-private"></a>ユーザーデータをプライベートに保つ

センサードライバーを作成する場合は、ユーザーのプライバシーを考慮する必要があります。 センサークラスの拡張機能によって適用されるプライバシーコントロールをバイパスしないようにする必要があります。 ユーザーがアクセス許可を付与する前に特定のプロパティを取得できるため、これらのプロパティを使用して、個人を特定できる情報をドライバーが明らかにしないようにする必要があります。 ユーザーがアクセス許可を付与する前に使用可能なプロパティの一覧については、「 [**ISensorDriver:: OnGetProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties)」を参照してください。

## <a name="additional-resources"></a>その他の情報

ユーザーのプライバシーを保護するソフトウェアを開発する際には、次のリソースを参照してください。

[ソフトウェア製品とサービスの開発に関するプライバシーガイドライン](https://go.microsoft.com/fwlink/p/?linkid=2085300)

[TechNet セキュリティデベロッパーセンター](https://go.microsoft.com/fwlink/p/?linkid=237150)

## <a name="related-topics"></a>関連トピック

[アーキテクチャの概要](https://docs.microsoft.com/windows-hardware/drivers/sensors/architecture-overview)  

[センサークラス拡張について](https://docs.microsoft.com/windows-hardware/drivers/sensors/about-the-sensor-class-extension)  

[場所の認識](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation)  
