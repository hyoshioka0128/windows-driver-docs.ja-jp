---
title: バージョン 3 XPSDrv 印刷ドライバー コンポーネント
description: バージョン 3 XPSDrv 印刷ドライバー コンポーネント
ms.assetid: 7eced017-a6a6-4fa5-8965-ff6655f86b8c
keywords:
- XPSDrv プリンター ドライバー WDK、モジュールの構成
- 構成モジュール WDK XPSDrv、バージョン 3 の XPS ドライバー
- バージョン 3 XPS ドライバー WDK XPSDrv
- レンダリングの WDK XPSDrv 変換モジュール
- バージョン 3 の XPS ドライバーに関する XPS ドライバー WDK XPSDrv、バージョン 3
- XPSDrv プリンター ドライバー WDK、バージョン 3 の XPS ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcfab6011e6a34f20ba27ddb4e105b7ef612f231
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538830"
---
# <a name="version-3-xpsdrv-print-driver-components"></a>バージョン 3 XPSDrv 印刷ドライバー コンポーネント


XPSDrv プリンター ドライバーのバージョン 3 のコンポーネントは構成モジュールを含み、aconversion モジュールを表示します。

印刷ドライバーが以前のバージョン 3 と同じアーキテクチャに基づいて、XPSDrv の構成のモジュールは、ドライバーを印刷します。 (Windows Vista は、ユニバーサル プリンター ドライバー (Unidrv) もサポートしています。 および PostScript (PScript5) は、一般的なプリンターの定義 (GPD) ファイルと PostScript プリンターの定義 (PPD) ファイルにそれぞれ基づいてドライバーを印刷します。 Windows Vista もサポートしています Unidrv または PScript5 印刷ドライバー構成プラグインとモノリシック印刷ドライバーの構成モジュール。)

既存の GDI を使用して XPSDrv プリンター ドライバーには、印刷の Microsoft Win32 アプリケーションでは、API のサポートを印刷します。 Microsoft が指定した変換のレンダリング モジュールは、GDI が出力するドライバー インターフェイス (DDI) 呼び出し、受信デバイスから XPS スプール ファイルを作成します。

次のトピックでは、XPSDrv 構成の問題を説明します。

[XPDDrv ドライバーのオプション](xpsdrv-driver-options.md)

[XPSDrv ドライバーの要件](xpsdrv-driver-requirements.md)

[XPSDrv ドライバーに関する推奨事項](xpsdrv-driver-recommendations.md)

[XPSDrv ドライバーの実装](xpsdrv-driver-implementation.md)

[Unidrv ベースまたは PScript5 ベース XPSDrv ドライバーの変更](unidrv-based-or-pscript5-based-xpsdrv-driver-changes.md)

 

 




