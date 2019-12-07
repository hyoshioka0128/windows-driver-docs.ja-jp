---
title: DIFx のガイドライン
description: DIFx のガイドライン
ms.assetid: de34f810-0e90-4626-b84d-160ac61541ad
ms.date: 05/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: 265ef1ed226aeeb4ab0727a16676e8740b5f4e51
ms.sourcegitcommit: a97a623d64ddf573c760664be17778606e156cf5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2019
ms.locfileid: "74907118"
---
# <a name="difx-guidelines"></a>DIFx のガイドライン

Windows 10 バージョン 1607 (Redstone 1) 以降、Driver Install Framework (DIFx) ツール (`Difxapi.dll`、`Difxapp.dll`、`Difxappa.dll`、および `DPInst.exe`) は非推奨となり、WDK に含まれなくなりました。

代わりに、インストーラーを必要としないスタンドアロンドライバーパッケージとして[ドライバーパッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)を提供することをお勧めします。  これは、システム状態を変更するインストーラーに依存するのではなく、独自の設定または構成を追加する自己完結型パッケージです。  すべてのドライバーパッケージシナリオを堅牢にサポートするためには、スタンドアロンドライバーパッケージが必要です。  スタンドアロンのドライバーパッケージを公開するには、Windows Update を使用することをお勧めします。  これを行うには、まず、ドライバーパッケージを[Windows ハードウェアデベロッパーセンター](https://partner.microsoft.com/dashboard)に送信します。

DIFx の使用を選択した場合は、古い WDK を使用して適切なツールを取得する必要があります。 次の注意事項が適用されます。

* ドライバーパッケージで Windows 8.1 以降の**TargetOSVersion**値のみが指定されている場合、Windows 8.1 で開始された API である[**GetVersionEx**](https://docs.microsoft.com/windows/desktop/api/sysinfoapi/nf-sysinfoapi-getversionexa)に対して difxapp の依存関係があるため、difxapp MSI カスタムアクションを使用することはできません。  **TargetOSVersion**は、[ [INF Manufacturer] セクション](inf-manufacturer-section.md)で指定します。 DIFxApp は、MsiProcessDrivers、Msiprocessdrivers、MsiUninstallDrivers などの MSI カスタムアクションを公開します。  ドライバーパッケージで Windows 8.1 以降の**TargetOSVersion**値が指定されている場合、これらのカスタム動作を MSI で使用することはできません。
* Windows 8.1 以降、`Difxapi.dll` にリンクするアプリケーションには、アプリケーションを実行する対象の OS バージョンを対象とするアプリマニフェストが含まれている必要があります。  これは、Windows 8.1 から変更された API である、 [**GetVersionEx**](https://docs.microsoft.com/windows/desktop/api/sysinfoapi/nf-sysinfoapi-getversionexa)に対する difxapi の依存関係が原因です。  Windows 8.1 での**GetVersionEx**の変更の詳細については、「 [Windows 用のアプリケーションを対象](https://docs.microsoft.com/windows/desktop/SysInfo/targeting-your-application-at-windows-8-1)にする」を参照してください。
* ドライバーパッケージで**TargetOSVersion**の製品版 (Windows 10 バージョン 1607 (ビルド14310以降) で導入 ***) が使用***されている場合は、そのドライバーパッケージで difx ツールを使用することはできません。  DIFx ツールは、対象化をサポートしていません。
* Windows 7 WDK で Windows 10 バージョン 1511 WDK を通じて使用できる DIFx バージョン2.1 を使用します。  2\.1 の DIFx バージョンは、以前のバージョンの WDK では使用できましたが、windows 7 以降のバージョンの Windows と互換性がありませんでした。

現在は更新されていませんが、 [Difxapi. h](https://docs.microsoft.com/previous-versions/windows/hardware/difxapi/)の api リファレンスドキュメントを参照できます。

ドライバーパッケージをインストールするためのカスタムインストーラーが必要な場合は、 [PnPUtil](https://docs.microsoft.com/windows-hardware/drivers/devtest/pnputil)コマンドラインツールまたは[ドライバーのインストール機能](functions-that-simplify-driver-installation.md)を呼び出すカスタムインストーラーのいずれかを使用します。

同様に、カスタムインストーラーを使用してドライバーパッケージをアンインストールする必要がある場合は、 [PnPUtil](https://docs.microsoft.com/windows-hardware/drivers/devtest/pnputil)を使用するか、 [**Diuninstalldriver**](https://docs.microsoft.com/windows/win32/api/newdev/nf-newdev-diuninstalldriverw)または[**setupuninsteminf**](https://docs.microsoft.com/windows/win32/api/setupapi/nf-setupapi-setupuninstalloeminfw)を呼び出すカスタムインストーラーを使用します。
