---
title: WBDI ドライバーでのセキュリティで保護されたチャネルのサポート
description: WBDI ドライバーでのセキュリティで保護されたチャネルのサポート
ms.assetid: 1b4532f4-18ee-4c65-9373-2ca635d2f40d
keywords:
- 生体認証ドライバー WDK、セキュリティで保護されたチャネル
- セキュリティで保護されたチャネル WDK 生体認証
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86d094897584be04bf2efe022930ed743b94b0e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558827"
---
# <a name="supporting-secure-channels-in-wbdi-drivers"></a>WBDI ドライバーでのセキュリティで保護されたチャネルのサポート


WBDI ドライバーでは、ホストとデバイス間のセキュリティで保護されたチャネルをサポートするために、ドライバーでのセキュリティ関連の機能をカプセル化する必要があります。 ドライバーは、セキュリティで保護されたチャネルを管理します。 ドライバーは、Windows 生体認証サービス (WBS) にサンプル データを渡す、データを暗号化されたあります。 WBS でプラグイン ベンダーから提供されたエンジンは、必要に応じて、web サービスをセキュリティで保護されたチャネルを設定できます。

セキュリティに関する考慮事項は、WBF アプリケーションにとって透過的な必要があります。

 

 





