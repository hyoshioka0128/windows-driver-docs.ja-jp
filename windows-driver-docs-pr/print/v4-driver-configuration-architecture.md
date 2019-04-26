---
title: V4 プリンター ドライバー構成アーキテクチャ
description: V4 プリンター ドライバー モデルは、大幅に簡略化された構成のレイヤーをサポートします。
ms.assetid: E797CB4A-C28E-4442-89E6-97B589900BD6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73f581861a41a02141560b8aed3221d2941d5500
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358712"
---
# <a name="v4-printer-driver-configuration-architecture"></a>V4 プリンター ドライバー構成アーキテクチャ


V4 プリンター ドライバー モデルは、大幅に簡略化された構成のレイヤーをサポートします。

場所 UI には、ドライバーの構成が厳密に結合されて、v3 プリンター ドライバーの場合とは異なり v4 プリンター ドライバーは PrintTicket、PrintCapabilities、および制約の機能を提供することに注目します。 PrintConfig.dll、共通の構成モジュールには、UnidrvUI と PS5UI コア ドライバーで使用可能だった機能がカプセル化します。

V4 プリンター ドライバー モデル GPD または PPD ファイルでデバイス構成のほとんどを表現する必要がありますので構成プラグインを必要としません。 さらに、v4 プリンター ドライバーは PrintCapabilities をサポートする PrintTicket と制約処理の高度なことは、JavaScript ファイルを提供することがあります。

**構成ファイルの形式**

一般的なプリンターの説明 (GPD) と PostScript プリンターの説明 (PPD) ファイル形式は、v4 プリンター ドライバーで変更されていません。 既存の GPD と PPD ファイルは、互換性のある、ただし、v4 プリンター ドライバーをすべて必要がありますさらを指定、次のディレクティブ、GPD または PPD ファイルで。 これらのディレクティブは、XPSDrv、n-up などでネイティブにサポートされていない機能の式を防止します。

| ファイルの種類 | 必要なディレクティブ | 必要な値 |
|-----------|--------------------|----------------|
| GPD       | \*含まれます          | msxpsinc.gpd   |
| PPD       | \*MSIsXPSDriver    | True           |

 

**注**  PPD ベースのドライバーを指定する必要があります、 \*Include: この msxpsinc.ppd ディレクティブは、一部のアプリケーションとの互換性の問題が発生する既知の。

 

**PrintSchema へのマッピング**

マッピングの機能とオプション PrintSchema の名前空間には、多くの場合必要があります。 マッピングは、標準の印刷 UI とアプリケーションとより互換性がある、ドライバーによって生成された PrintCapabilities ドキュメントをによりします。

一部の機能とオプションは、標準であると見なされます、PrintSchema の名前空間に自動的にマップされます。 これらの機能とオプションは固有でありを使用する必要がありますリマップいない\*PrintSchemaKeywordMap します。 ドライバーを使用する必要があります一覧にない場合、 \*GPD ベースのドライバーに関する PrintSchemaKeywordMap ディレクティブまたは\*PPD ベースのドライバーで MSPrintSchemaKeywordMap ディレクティブ。

 

 




