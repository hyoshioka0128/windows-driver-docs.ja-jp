---
title: IWiaItem CreateChildItem を使用して選択範囲を作成するには
description: IWiaItem CreateChildItem を使用して選択範囲を作成するには
ms.assetid: c430d15b-51e9-4419-9cdb-904a0f5ef09b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1abebae6edb22e25d618641d21735ef035ba8079
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537741"
---
# <a name="using-iwiaitemcreatechilditem-to-create-selection-areas"></a>IWiaItem::CreateChildItem を使用して選択範囲を作成するには





WIA アプリケーションをお読みください、 [ **WIA\_IP\_サポート\_子\_項目\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff552653)プロパティを確認するかどうかフィルムの項目をスキャンでは、子項目の作成をサポートします。 フィルム スキャナーの項目に含めることができます、項目の子項目 (つまり、フレーム) ツリーを*できません*削除します。 アプリケーションでマークされている WIA 項目を削除する、 [ **WIA\_IPA\_アクセス\_RIGHTS** ](https://msdn.microsoft.com/library/windows/hardware/ff551518)の設定 (WIA\_PROP\_読み取り |WIA\_項目\_書き込み |WIA\_項目\_できます\_BE\_削除済み)。

### <a name="creating-dynamic-film-items"></a>動的なフィルムの項目の作成

WIA アプリケーションを呼び出す**IWiaItem::CreateChildItem** (Microsoft Windows SDK のドキュメントで説明)、新しい項目の WIA アプリケーション (またはフレーム) を作成するフィルム スキャナーの項目の下にあります。 WIA ドライバーは、WIA に必要なプロパティを初期化する必要があります、WIA アプリケーションは、新しいフレームを構成するには、エクステントの設定とその他のプロパティを設定する必要があります。 必要な WIA プロパティの詳細については、[フィルム スキャナーの必須の WIA 項目プロパティ](required-wia-item-properties-for-film-scanners.md)を参照してください。

**注**   WIA フィルムの項目は、WIA 子項目の 1 つだけのレベルをいる必要があります。 フィルム項目は、フォルダー、フォルダーのアイテムに設定できます*できません*フィルム スキャナーの項目の下に作成します。

 

 

 




