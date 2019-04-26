---
title: ベンダー拡張プロパティ
description: ベンダー拡張プロパティ
ms.assetid: bcc89272-c14d-4d46-a2ca-7da0fb188111
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15937fdd0040d87217fc01ff00a73741951d5976
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356144"
---
# <a name="vendor-extended-properties"></a>ベンダー拡張プロパティ





A **PropCode**内のエントリ、 **DeviceData** INF ファイルのセクション (例を参照してください[Vendor-Extended 機能](vendor-extended-features.md)) で区切られた、、すべてのプロパティのベンダー拡張コードの一覧。コンマです。 各プロパティのコード、フォームのエントリの **PropCode * * * XXXX* XXXX が大文字の 16 進数コード値が存在する必要があります。 エントリには、WIA プロパティのコードが一覧表示し、引用符で囲まれたテキストの説明 (をローカライズする必要はありません)。

WIA プロパティのコードは、0x9802 ~ 0x11802、WIA デバイスのベンダ定義のプロパティに対して定義されている範囲でなければなりません。 プロパティを通じてアクセスできる、 **IWiaPropertyStorage::GetPropertyStream**と**IWiaPropertyStorage::SetPropertyStream**メソッドは、Microsoft Windows SDK で説明されています。ドキュメントです。

 

 




