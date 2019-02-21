---
title: DIFx ガイドライン
description: DIFx ガイドライン
ms.assetid: de34f810-0e90-4626-b84d-160ac61541ad
ms.date: 05/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: ecc9e613e9207794263a89b1a4c677fd8bda05ad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536293"
---
# <a name="difx-guidelines"></a>DIFx ガイドライン

以降では、Windows 10 バージョン 1607 (Redstone 1) は、WDK で Driver Install Frameworks (DIFx) ツールは含まれなくします。  代わりに、Windows Update を通じて理想的には、インストーラーを必要としないスタンドアロン パッケージとして、ドライバーを提供することをお勧めします。  Windows Update には、ドライバーを追加するには、まずをドライバー パッケージを提出、 [Windows ハードウェア デベロッパー センター](https://developer.microsoft.com/windows/hardware/dashboard-sign-in)します。

とにかく DIFx を使用する場合は、ツールを含む古い WDK を使用する必要があり、いくつか注意すべき点に注意する必要があります。

* ドライバー パッケージはのみに指定されている場合**TargetOSVersion** Windows 8.1 またはそれ以降の値では使用できません DIFxApp DIFxApp の依存関係のため[ **GetVersionEx**](https://msdn.microsoft.com/library/windows/desktop/ms724451)、APIWindows 8.1 以降を変更します。  **TargetOSVersion**で指定された、 [INF 製造元セクション](inf-manufacturer-section.md)します。 DIFxApp は、MSI MsiProcessDrivers、MsiInstallDrivers、MsiUninstallDrivers などのカスタム操作を公開します。  ドライバー パッケージが指定されている場合**TargetOSVersion**値または後で、Windows 8.1 の MSI でこれらのカスタム動作を使用することはできません。
* Windows 8.1、リンクするアプリケーションで起動`Difxapi.dll`アプリケーションが実行しようとする OS バージョンを対象とするアプリケーション マニフェストを含める必要があります。  DIFxAPI の依存関係のためにこれは、 [ **GetVersionEx**](https://msdn.microsoft.com/library/windows/desktop/ms724451)API を Windows 8.1 以降に変更します。  詳細の変更を**GetVersionEx**で Windows 8.1 では、次を参照してください。 [Windows 用のアプリケーションを対象とする](https://msdn.microsoft.com/library/windows/desktop/dn481241)します。
* ドライバー パッケージで使用する場合、 ***BuildNumber***一部分**TargetOSVersion** (Windows 10 version 1607 で導入された (ビルド 14310 およびそれ以降))、ドライバー パッケージに DIFx ツールを使用することはできません。  DIFx ツールでは、ビルド番号を対象とするが理解できません。
* Windows 10 Version 1511 WDK から Windows 7 の WDK で提供されている DIFx は、バージョン 2.1 を使用します。  以前のバージョンの WDK で DIFx バージョン 2.1 の使用できた、Windows 7 以降のバージョンの Windows 互換性適切でした。

DIFx での API リファレンス ドキュメントを見つけることができますが、不要になった更新中は、 [Difxapi.h](https://docs.microsoft.com/previous-versions/windows/hardware/difxapi/)します。

インストーラーを必要としないスタンドアロン パッケージとしてドライバーを提供することがない場合、オプションし、コマンド ライン ツール[PnPUtil](https://docs.microsoft.com/windows-hardware/drivers/devtest/pnputil)またはを使用するカスタム インストーラー[ドライバーのインストール機能](setupapi-functions-that-simplify-driver-installation.md)できますインストールのストーリーの一部として使用します。
