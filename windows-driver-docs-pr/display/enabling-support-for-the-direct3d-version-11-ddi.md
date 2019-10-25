---
title: Direct3D バージョン 11 DDI のサポートを有効にする
description: Direct3D バージョン 11 DDI のサポートを有効にする
ms.assetid: 997d6b06-110b-403d-bcf5-350a26ecffbd
keywords:
- Direct3D バージョン 11 WDK Windows 7 ディスプレイ、DDI サポートの有効化
- Direct3D バージョン 11 WDK Windows Server 2008 R2 ディスプレイ、DDI サポートの有効化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 701483d830241f68703f499286ed5b880a17083a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838953"
---
# <a name="enabling-support-for-the-direct3d-version-11-ddi"></a>Direct3D バージョン 11 DDI のサポートを有効にする


このセクションは、windows 7 以降、および windows Server 2008 R2 以降のバージョンの Windows オペレーティングシステムにのみ適用されます。

ユーザーモードの表示ドライバー DLL のバージョン 11 DDI のサポートを有効にするには、グラフィックスデバイスのディスプレイドライバーをインストールする INF ファイルで、direct3d version 11 DDI が[direct3d バージョン 9 D と同じ dll に存在するかどうかに関係なく、dll の名前を一覧表示する必要があります。DI](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/index)および[Direct3D バージョン 10 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)または別の DLL。

「[ミニポートを表示する」および「ユーザーモードの表示ドライバーのインストール要件](installing-display-miniport-and-user-mode-display-drivers.md)」セクションでは、Windows Vista の表示ドライバーモデルに従って、ユーザーモードの表示ドライバーをインストールして使用する方法について説明します。 また、Direct3D バージョン 11 DDI のサポートを有効にするには、バージョン 11 ddi がバージョン9および 10 DDIs と同じ DLL に存在する場合でも、バージョン 11 DDI を含む DLL の名前を3番目のエントリとして指定する必要があります。

複数の場所で同じユーザーモードの表示ドライバーの DLL 名を使用して、ドライバーの実装を統合することができます。 実際、direct3d version 10 および version 11 DDIs の設計では、Direct3D バージョン10および Direct3D version 11 ドライバーの共有実装が厳密にサポートされています。

次の例では、バージョン 11 ddi が*Umd11*に含まれている場合、バージョン 11 ddi のサポートが有効になっていることを示しています (つまり、バージョン9と 10 DDIs の別の dll)。

```inf
 [Xxx_SoftwareDeviceSettings]
...
 HKR,, UserModeDriverName,    %REG_MULTI_SZ%, umd9.dll, umd10.dll,  umd11.dll
 HKR,, InstalledDisplayDrivers,    %REG_MULTI_SZ%, umd9, umd10, umd11 
```

次の例では、バージョン 11 ddi が*Umd*.dll に含まれている場合、バージョン 11 ddi のサポートが有効になっていることを示しています。これは、Direct3D バージョン9、10、および11ドライバーの共有の実装です。

```inf
[Xxx_SoftwareDeviceSettings]
...
 HKR,, UserModeDriverName,    %REG_MULTI_SZ%, umd.dll, umd.dll, umd.dll
 HKR,, InstalledDisplayDrivers,    %REG_MULTI_SZ%, umd, umd, umd 
```

 

 





