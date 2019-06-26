---
title: プロパティの表示と変更
description: プロパティの表示と変更
ms.assetid: 657b687d-b0c0-46e0-a948-242509590a4b
keywords:
- ネットワー キング WDK オブジェクト、プロパティ ページに通知します。
- ネットワークがオブジェクトにプロパティ ページに通知します。
- プロパティ ページの WDK ネットワーク
- WDK ネットワークのプロパティ
- ネットワーク構成のプロパティを表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b426660d3724633dc94cb6041d8f677311698b19
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386561"
---
# <a name="displaying-and-changing-properties"></a>プロパティの表示と変更





ネットワーク構成のサブシステムでは、ネットワーク コンポーネントのプロパティ ページを表示し、コンポーネントのパラメーターを変更します。

コンポーネントのプロパティを表示し、コントロール パネルから変更できます。 クリックすると、**ネットワーク**アイコン、通知オブジェクトのインスタンスを作成し、オブジェクトの呼び出しが、ネットワーク構成サブシステムを起動する[ **INetCfgComponentControl::Initialize**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547729(v=vs.85))メソッド。 このメソッドは、オブジェクトを初期化し、コンポーネントとネットワークの構成のすべての側面へのアクセスを提供します。

アプリケーションによってコンポーネントの[ **INetCfgComponent::RaisePropertyUi** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547895(v=vs.85))コンポーネントのプロパティを表示するメソッド。 **RaisePropertyUi**メソッドを呼び出して次の通知オブジェクトのメソッド。

-   [**INetCfgComponentPropertyUi::QueryPropertyUi** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547749(v=vs.85))メソッドは、特定のコンテキストが、コンポーネントのプロパティを表示する適切なかどうかを判断します。

-   [**INetCfgComponentPropertyUi::SetContext** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547752(v=vs.85))メソッドを直接、コンポーネントの指定したコンテキストで、コンポーネントのプロパティを表示するオブジェクトに通知します。

-   [**INetCfgComponentPropertyUi::MergePropPages** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547746(v=vs.85))メソッドを作成およびカスタム コンポーネントのプロパティ シート ページを既定のセットにマージします。

ユーザーがカスタムのページの 1 つのコンポーネントのパラメーターのいずれかを変更した場合**RaisePropertyUi**通知オブジェクトの呼び出し[ **INetCfgComponentPropertyUi::ApplyProperties** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547741(v=vs.85))メモリで変更を格納する方法。

変更を適用するには、ネットワーク構成のサブシステムは、通知オブジェクトを呼び出します[ **INetCfgComponentControl::ApplyRegistryChanges** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547727(v=vs.85))のネットワーク コンポーネントに関する情報を変更する方法。レジストリ。 コンポーネントのドライバーを変更した情報で構成するは、ネットワーク構成のサブシステムは、通知オブジェクトを呼び出します[ **INetCfgComponentControl::ApplyPnpChanges** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547726(v=vs.85))メソッドを呼び出し。[ **INetCfgPnpReconfigCallback** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547935(v=vs.85))インターフェイス。

 

 





