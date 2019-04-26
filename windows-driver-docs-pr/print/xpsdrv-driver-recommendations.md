---
title: XPSDrv ドライバー推奨事項
description: XPSDrv ドライバー推奨事項
ms.assetid: 6700afd2-8526-4464-92b8-a9c1a37f8402
keywords:
- バージョン 3 XPS ドライバー WDK XPSDrv、推奨事項
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cae981451f5fc77b5e42f2e50ae7c8f58a1f0b70
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358232"
---
# <a name="xpsdrv-driver-recommendations"></a>XPSDrv ドライバー推奨事項


加え、 [XPSDrv ドライバー要件](xpsdrv-driver-requirements.md)、次のベスト プラクティスを検討する必要があります。

-   **モジュールの GPD または PPD ファイルを使用します。** Unidrv ベースまたは PScript5 ベースの構成モジュールは、印刷ドライバーは、各フィルターの別 GPD または PPD ファイルを指定する必要があります。 次に、1 つの「親」印刷ドライバー GPD または PPD ファイルではすべてのフィルターあたり GPD または PPD ファイルを参照する必要があります。 フィルターによって、モジュール方式で GPD と PPD ファイルを整理すると、モジュール性と、フィルター パイプライン内のフィルターを再利用を維持できます。

-   **印刷スキーマ キーワードをパブリックにマップします。** 可能であれば、する必要がありますを割り当てるすべての印刷ドライバーの設定と印刷ドライバー機能を策定、public 印刷スキーマに相当するキーワード。 印刷ドライバーの設定をパブリック印刷スキーマ キーワードにマッピングすると、新しい機能を採用するアプリケーションを簡単にできます。 このマッピングには、印刷ドライバーおよびアプリケーションとシステム間のプリンターの設定を同期させるも用意されています。

 

 




