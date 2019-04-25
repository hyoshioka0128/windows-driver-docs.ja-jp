---
title: 3D プリンター ドライバー設計ガイド
description: このセクションでは、Windows 10 の 3D プリンター ドライバーについて説明します。
ms.assetid: 3271C160-4253-48B5-A089-E026C6BAD3AF
ms.date: 09/20/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 0a22e90a6a9131a637d03354f5825443c02de466
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325945"
---
# <a name="3d-printer-driver-design-guide"></a>3D プリンター ドライバー設計ガイド

このセクションでは、Windows 10 の 3D プリンター ドライバーについて説明します。

Windows 10 の 3D 印刷には、次の機能があります。

-   3D 製造機器のドライバー モデル

-   3D デバイスの UWP アプリと拡張機能のサポート

-   ジョブのスプールとキューのサポート

-   機器の機能をモデル化するためのキーワード

-   3D 製造ジョブを 3D プリンターに送信するアプリ用 API

Windows 10 での 3D 印刷の最新情報については、以下のリソースを参照してください。

-   [Windows 上の 3D 印刷](https://go.microsoft.com/fwlink/p/?LinkId=627554)
-   [3D ハードウェア パートナー](https://go.microsoft.com/fwlink/p/?LinkId=627548)
-   [3D Builder リソース](https://go.microsoft.com/fwlink/p/?LinkId=627556)
-   [3D Builder ユーザー ガイド](https://go.microsoft.com/fwlink/p/?LinkId=627557)
-   [Channel 9 の 3D 印刷のブログ](https://go.microsoft.com/fwlink/p/?LinkId=624519)

[Windows 3D 印刷 SDK](https://go.microsoft.com/fwlink/p/?LinkId=394375) をダウンロードして、3D プリンターでの印刷用ドライバーの開発を始めます。

## <a name="in-this-section"></a>このセクションの内容

-   [3D 印刷パートナー オンボーディング ガイド](3d-partner-onboarding-guide.md)
-   [3D プリンター用の Microsoft 標準ドライバー](microsoft-standard-driver-for-3d-printers-.md)
-   [MS3DPrint 標準 G コード ドライバー](ms3dprint-standard-g-code-driver.md)
-   [3D プリンターのカスタム USB インターフェイスのサポート](3d-printer-custom-usb-interface.md)
-   [3D 印刷のサンプル WSD アプリ](3d-printing-sample-wsd-app.md)
-   [デバイスで WSPrint 2.0 を有効にする](enabling-wsprint-on-a-device.md)
-   [3D 製造用の印刷スキーマのキーワード](print-schema-keywords-for-3d-manufacturing.md)
-   [3D ハードウェア パートナー](3d-printing-partners.md)

## <a name="related-sections"></a>関連セクション

-   [印刷 DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_print)
