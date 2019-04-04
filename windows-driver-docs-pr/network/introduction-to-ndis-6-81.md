---
title: NDIS 6.81 の概要
description: このセクションでは、NDIS 6.81 を紹介し、NDIS 6.80 からの変更について説明します。 Windows 10、バージョン 1803 で NDIS 6.81 が含まれます。
ms.assetid: 5B41C6D6-96FE-4B3D-94ED-46DF164FB202
ms.date: 05/14/2018
ms.localizationpriority: medium
ms.openlocfilehash: a0ee434442739e401b862ee96a876650ee4186b3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553914"
---
# <a name="introduction-to-ndis-681"></a>NDIS 6.81 の概要

このトピックでは、Network Driver Interface Specification (NDIS) 6.81 を示し、その主要な設計の追加機能を説明します。 NDIS 6.81 は、Windows 10、バージョン 1803 および Windows Server 2016 に含まれる以降です。

NDIS 6.81 は、NDIS 6.80 にマイナー バージョン更新です。 NDIS 6.81 する NDIS 6.x ドライバーの移植の詳細については、[NDIS 6.81 に移植する NDIS 6.x ドライバー](porting-ndis-6-x-drivers-to-ndis-6-81.md)を参照してください。

## <a name="feature-updates"></a>機能更新プログラム

NDIS 6.81 NDIS 6.80 を増分更新は、主要な新機能が含まれていません。

## <a name="implementing-an-ndis-681-driver"></a>NDIS 6.81、ドライバーを実装します。

NDIS 6.81、ドライバーがで定義されている要件に従う必要があります[、NDIS 6.30 ドライバーを実装する](implementing-an-ndis-6-30-driver.md)します。

さらに、NDIS 6.81 ドライバーは、次の要件に準拠する必要があります。

- NDIS 6.81 ドライバーは、NDIS に登録する際に、正しい NDIS バージョンを報告する必要があります。
   
   必要があります、メジャーおよびマイナー NDIS バージョン番号を更新 NDIS_Xxx_DRIVER_CHARACTERISTICS 構造で NDIS 6.81 をサポートするためにします。 MajorNdisVersion メンバーは、6 を含める必要があり、MinorNdisVersion メンバーは 81 を含める必要があります。 この要件は、ミニポート、プロトコル、およびフィルター ドライバーに適用されます。 コンパイラのバージョン情報を更新することも必要があります (を参照してください[コンパイル、NDIS 6.81 ドライバー](#compiling-an-ndis-681-driver))。

- Windows 10、バージョン 1803 および Windows Server 2016 以降の NDIS 6.81 ミニポート ドライバーでは、データ構造の NDIS 6.81 バージョンを使用する必要があります。

## <a name="compiling-an-ndis-681-driver"></a>コンパイル、NDIS 6.81 ドライバー

Windows 10 の WDK バージョン 1803 では、ヘッダー バージョン管理をサポートします。 ヘッダー バージョン管理は、NDIS 6.81 ドライバーがコンパイル時に適切な NDIS 6.81 データ構造を使用することを確認します。

ドライバーの Visual Studio プロジェクトには、次のコンパイラ設定を追加します。

- ミニポート ドライバーでは、追加`NDIS681_MINIPORT=1`します。
- フィルターまたはプロトコルのドライバーを追加`NDIS681=1`します。

Windows 10、バージョン 1803 リリース、WDK のドライバーを構築する方法についてを参照してください。[ドライバーをビルド](../develop/building-a-driver.md)します。
