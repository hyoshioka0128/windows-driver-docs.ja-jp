---
title: カメラの測定値
description: カメラの測定値では、Bluetooth ドライバーのフライティング時に、良性の初期化エラーがフィルターで除外されます
ms.topic: article
ms.date: 05/20/2019
ms.author: paslote
author: parkeratmicrosoft
ms.localizationpriority: medium
ms.openlocfilehash: 2acb116ac751bf4bc132c327273b3fa37feb834a
ms.sourcegitcommit: 04da1962e34908adeca54fcf5bbfbaa456efca5f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2019
ms.locfileid: "70224034"
---
# <a name="camera-measures"></a>カメラの測定値

## <a name="description"></a>説明

Windows 10 で、Microsoft は[汎用カメラ ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/stream/windows-10-technical-preview-camera-drivers-design-guide)を提供しています。これは、カメラ ドライバー インターフェイスがすべてのカメラ関連デバイスをどのようにサポートしているかを説明したものです。 このモデルには、デジタル ビデオ手ブレ補正、可変フレーム レート、顔検出などの新しい DDI や、多くのその他の機能が含まれています。 汎用カメラ ドライバーは Windows Driver Model で構築された AVStream ミニドライバーです。AVStream は、ビデオのみのストリーミングとビデオおよびオーディオの統合ストリーミングをサポートする、Microsoft 提供のマルチメディア クラス ドライバーです。 AVStream の詳細については、[AVStream ミニドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-minidrivers-design-guide)をご覧ください。