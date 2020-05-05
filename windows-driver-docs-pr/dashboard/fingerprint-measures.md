---
title: 指紋の測定
description: 指紋の測定では、指紋デバイスを使用するユーザー エクスペリエンスの成功を検証します
ms.topic: article
ms.date: 03/30/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7ab3017b067332260583b3d87f8d8c48431b17ce
ms.sourcegitcommit: 774d42aa3392ae88f4890d901dbd3e8945cb2658
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82139496"
---
# <a name="fingerprint-measures"></a>指紋の測定

## <a name="description"></a>説明

[Windows 生体認証フレームワーク (WBF)](https://docs.microsoft.com/windows/win32/secbiomet/biometric-service-api-portal) は、生体認証センサーに Windows 10 と統合するためのプラグ可能なモデルを提供します。 WBF に接続する指紋センサーは、Windows Hello の一部としてユーザーに提供されます。 指紋センサーは、[Windows 生体認証ドライバー インターフェイス (WBDI)](https://docs.microsoft.com/windows-hardware/drivers/biometric/) と連携するユーザー モード ドライバーを実装することにより、フレームワークに登録できます。 WBF はドライバーに含まれるアダプターを使用してセンサーを呼び出し、サンプルのキャプチャ、照合操作、テンプレート管理操作などの生体認証の操作を調整します。 