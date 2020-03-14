---
title: 非 PnP ドライバーのインストール
description: 非 PnP ドライバーのインストール
ms.assetid: 99676d85-feb2-482c-a91b-cfc48be5904c
keywords:
- カーネルモードドライバーフレームワーク WDK、ドライバーのインストール
- フレームワークベースのドライバー WDK KMDF, インストール
- INF ファイル WDK KMDF、PnP 以外のドライバー
- 非 PnP ドライバー WDK KMDF
ms.date: 03/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: a6b59f70626d08aac48ba3af61e36782b229f9fa
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79216614"
---
# <a name="installing-a-non-pnp-driver"></a>非 PnP ドライバーのインストール


KMDF ドライバーが Windows 10 で非プラグアンドプレイ (PnP) デバイスをサポートしている場合は、 [Pnp 以外のドライバーのサンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/ioctl/kmdf)に記載されているものと同じ方法を使用しますが、INF ファイルと共同インストーラーへの参照は削除します。 たとえば、次のものは必要ありません。

```
#define NONPNP_INF_FILENAME  L"\\nonpnp.inf"
#define WDF_SECTION_NAME L"nonpnp.NT.Wdf"
 
LoadWdfCoInstaller
UnloadWdfCoInstaller
 
PFN_WDFPREDEVICEINSTALLEX pfnWdfPreDeviceInstallEx;
PFN_WDFPOSTDEVICEINSTALL   pfnWdfPostDeviceInstall;
PFN_WDFPREDEVICEREMOVE     pfnWdfPreDeviceRemove;
PFN_WDFPOSTDEVICEREMOVE   pfnWdfPostDeviceRemove;
```

PnP 以外の KMDF ドライバーの場合は、SCM API を呼び出してサービスを作成するだけです。 詳細については、「[サービスのインストール](https://docs.microsoft.com/windows/win32/services/installing-a-service)」を参照してください。



