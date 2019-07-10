---
title: ベンダー拡張プロパティ
description: ベンダー拡張プロパティ
ms.assetid: bcc89272-c14d-4d46-a2ca-7da0fb188111
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1279041b5a64aacdc02117432c8a06a84a4993a
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716904"
---
# <a name="vendor-extended-properties"></a>ベンダー拡張プロパティ





A **PropCode**内のエントリ、 **DeviceData** INF ファイルのセクション (例を参照してください[Vendor-Extended 機能](vendor-extended-features.md)) で区切られた、、すべてのプロパティのベンダー拡張コードの一覧。コンマです。 各プロパティのコード、フォームのエントリの**PropCode**_XXXX_ XXXX が大文字の 16 進数コード値が存在する必要があります。 エントリには、WIA プロパティのコードが一覧表示し、引用符で囲まれたテキストの説明 (をローカライズする必要はありません)。

WIA プロパティのコードは、0x9802 ~ 0x11802、WIA デバイスのベンダ定義のプロパティに対して定義されている範囲でなければなりません。 プロパティを通じてアクセスできる、 **IWiaPropertyStorage::GetPropertyStream**と**IWiaPropertyStorage::SetPropertyStream**メソッドは、Microsoft Windows SDK で説明されています。ドキュメントです。

 

 




