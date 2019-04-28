---
title: WIA スキャナー ドライバーの開発
description: WIA スキャナー ドライバーの開発
ms.assetid: befe7e36-cb42-48da-88b4-d8983876266f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 624fb0ee5f3755e4dcb115b5995fc92717c381eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364578"
---
# <a name="developing-a-wia-scanner-driver"></a>WIA スキャナー ドライバーの開発





WIA スキャナー ドライバー開発者向けには、WIA microdriver または WIA ミニドライバーを作成できます。

### <a name="microdriver"></a>Microdriver

Microdriver は、単純なフラット ベッド スキャナーをサポートする小規模なドライバーです。 このドライバーの種類は、ミニドライバーより迅速に開発できますが、次の制限があります。

-   Microdrivers は、フラット ベッド スキャナーの場合のみに制限されます。

-   Microdrivers 最小限ドキュメント フィーダー サポート (双方向の操作なし) のみを提供します。

-   Microdrivers では、限定された数のドット/インチ (dpi) で解決策を提供します。75、100、150、200、300 および 600。

-   Microdrivers WiaImgFmt のみをサポートする\_BMP と WiaImgFmt\_MEMORYBMP イメージ形式。 これらのイメージ形式の詳細については、Microsoft Windows SDK を参照してください。

-   Microdrivers は、3 回のスキャン (色のフィルターを使用してカラー イメージをキャプチャするは、古い色スキャナーで使用) をサポートしていません。

Microdrivers の開発に関する詳細については、次を参照してください。[作成 WIA Microdriver](creating-a-wia-microdriver.md)します。

### <a name="minidriver"></a>ミニドライバー

ミニドライバーは、完全な WIA ミニドライバーです。 参照してください[WIA ミニドライバーを作成する](creating-a-wia-minidriver.md)詳細についてはします。

このセクションには、次のトピックに関する追加情報が含まれています。

[WIA スキャナー項目ツリーのレイアウト](wia-scanner-item-tree-layout.md)

[ドキュメント フィーダーのサポートを追加します。](adding-document-feeder-support.md)

[ページ サイズと向き](page-size-and-orientation.md)

[TWAIN 互換性](twain-compatibility.md)

 

 




