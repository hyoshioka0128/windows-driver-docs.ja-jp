---
title: Windows Display Driver Model (WDDM) の設計ガイド
description: Windows Display Driver Model (WDDM) は Windows Vista 以降で使用でき、windows 8 以降で必要です。 このセクションでは、WDDM ドライバーの要件、仕様、および動作について説明します。
ms.assetid: d9dc0d48-aea4-4614-a23b-e2449800469f
keywords:
- WDDM 設計ガイド WDK
- ドライバーモデルの表示 WDK Windows Vista
- Windows Vista display driver model WDK
- デバイスの WDK を表示する
- ディスプレイドライバー WDK、Windows Vista
- ディスプレイドライバーモデル WDK Windows Vista、ディスプレイドライバーモデルについて
- Windows Vista display driver model WDK、display driver model の概要
- ミニポート ドライバー WDK ディスプレイ
- ミニポートドライバーの表示 WDK 「ミニポートドライバーの WDK ディスプレイ」を参照してください。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72c22419a18eca7ab8af5e8c70131e7102df1aff
ms.sourcegitcommit: 0d89fc46058efb2ebc6ed9bd8f638c3f8cc1a678
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2020
ms.locfileid: "86459234"
---
# <a name="windows-display-driver-model-wddm-design-guide"></a>Windows Display Driver Model (WDDM) の設計ガイド

Windows Display Driver Model (WDDM) は、Windows 8 以降で必要になります。 このガイドでは、wddm ドライバーの WDDM 要件、仕様、および動作について説明します。

> [!NOTE]
>
> [Windows 2000 Display Driver Model (XDDM)](windows-2000-display-driver-model-design-guide.md)および VGA ドライバーは、windows 8 以降のバージョンではコンパイルされません。 WDDM 1.2 以降のサポートを認定されたドライバーのない Windows 8 コンピューターにディスプレイ ハードウェアが接続されている場合、システムは既定で Microsoft Basic Display Driver を実行します。
>
> WDDM ドライバーでは、Windows グラフィックスデバイスインターフェイス (GDI) エンジンのサービスは直接使用されません。そのため、[ [GDI](gdi.md) ] セクションは、WDDM ドライバーモデルのディスプレイドライバーの記述には関係ありません。
