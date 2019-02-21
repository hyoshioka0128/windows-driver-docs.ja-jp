---
title: 表示して、プロパティを変更します。
description: 表示して、プロパティを変更します。
ms.assetid: 657b687d-b0c0-46e0-a948-242509590a4b
keywords:
- ネットワー キング WDK オブジェクト、プロパティ ページに通知します。
- ネットワークがオブジェクトにプロパティ ページに通知します。
- プロパティ ページの WDK ネットワーク
- WDK ネットワークのプロパティ
- ネットワーク構成のプロパティを表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f23c47240e50ac78268d69fa11bd29fbe410cbf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529893"
---
# <a name="displaying-and-changing-properties"></a>表示して、プロパティを変更します。





ネットワーク構成のサブシステムでは、ネットワーク コンポーネントのプロパティ ページを表示し、コンポーネントのパラメーターを変更します。

コンポーネントのプロパティを表示し、コントロール パネルから変更できます。 クリックすると、**ネットワーク**アイコン、通知オブジェクトのインスタンスを作成し、オブジェクトの呼び出しが、ネットワーク構成サブシステムを起動する[ **INetCfgComponentControl::Initialize**](https://msdn.microsoft.com/library/windows/hardware/ff547729)メソッド。 このメソッドは、オブジェクトを初期化し、コンポーネントとネットワークの構成のすべての側面へのアクセスを提供します。

アプリケーションによってコンポーネントの[ **INetCfgComponent::RaisePropertyUi** ](https://msdn.microsoft.com/library/windows/hardware/ff547895)コンポーネントのプロパティを表示するメソッド。 **RaisePropertyUi**メソッドを呼び出して次の通知オブジェクトのメソッド。

-   [**INetCfgComponentPropertyUi::QueryPropertyUi** ](https://msdn.microsoft.com/library/windows/hardware/ff547749)メソッドは、特定のコンテキストが、コンポーネントのプロパティを表示する適切なかどうかを判断します。

-   [**INetCfgComponentPropertyUi::SetContext** ](https://msdn.microsoft.com/library/windows/hardware/ff547752)メソッドを直接、コンポーネントの指定したコンテキストで、コンポーネントのプロパティを表示するオブジェクトに通知します。

-   [**INetCfgComponentPropertyUi::MergePropPages** ](https://msdn.microsoft.com/library/windows/hardware/ff547746)メソッドを作成およびカスタム コンポーネントのプロパティ シート ページを既定のセットにマージします。

ユーザーがカスタムのページの 1 つのコンポーネントのパラメーターのいずれかを変更した場合**RaisePropertyUi**通知オブジェクトの呼び出し[ **INetCfgComponentPropertyUi::ApplyProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff547741)メモリで変更を格納する方法。

変更を適用するには、ネットワーク構成のサブシステムは、通知オブジェクトを呼び出します[ **INetCfgComponentControl::ApplyRegistryChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff547727)のネットワーク コンポーネントに関する情報を変更する方法。レジストリ。 コンポーネントのドライバーを変更した情報で構成するは、ネットワーク構成のサブシステムは、通知オブジェクトを呼び出します[ **INetCfgComponentControl::ApplyPnpChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff547726)メソッドを呼び出し。[ **INetCfgPnpReconfigCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff547935)インターフェイス。

 

 





