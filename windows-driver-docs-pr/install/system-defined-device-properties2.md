---
title: システム定義のデバイス プロパティ
description: システム定義のデバイス プロパティ
ms.assetid: 9d823a9f-0802-4e92-bf94-abb5b0e7b9ee
keywords:
- システム定義のデバイス プロパティ、WDK のデバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3303baf46621e4037768ff56a658b85b842aedac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578804"
---
# <a name="system-defined-device-properties"></a>システム定義のデバイス プロパティ


Windows Vista および Windows での以降のバージョンで、[統一されたデバイス プロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)構成またはデバイスのインスタンスの操作の特性を示すシステム定義のプロパティをサポートしている[デバイス セットアップ クラス](device-setup-classes.md)、[デバイス インターフェイス クラス](device-interface-classes.md)、およびデバイスのインターフェイス。 によって表される各プロパティを[プロパティのキー](property-keys.md)、これはプロパティのカテゴリおよびプロパティの識別子を識別する GUID 値です。 システム定義のプロパティ、主要なカテゴリは、システム専用として予約されています。

次のシステム定義のデバイス プロパティのキーが定義されている*Devpkey.h*:

-   コンポーネントの名前を表す DEVPKEY_NAME プロパティのキー。 DEVPKEY_NAME プロパティの値を使用して、エンドユーザーにコンポーネントを識別します。 Windows の DEVPKEY_NAME プロパティをサポートする[**デバイス インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff543530)、 [**デバイス セットアップ クラス**](https://msdn.microsoft.com/library/windows/hardware/ff543534)、および[ **デバイス インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff543533)します。

-   プロパティのキーを表す、 [SPDRP_Xxx 識別子に対応するデバイス インスタンス プロパティ](https://msdn.microsoft.com/library/windows/hardware/ff541334)します。 (、SPDRP_*Xxx*で識別子が定義されている*Setupapi.h*)。

-   デバイスを表すプロパティのキーのインスタンスのプロパティを対応する SPDRP_ を持たない*Xxx*識別子。 これには、次のデータが含まれます。

    [デバイスの状態および問題のプロパティ](https://msdn.microsoft.com/library/windows/hardware/ff542254)

    [デバイスのリレーション プロパティ](https://msdn.microsoft.com/library/windows/hardware/ff541498)親デバイス、デバイスの子、兄弟デバイスなど、

    [デバイス ドライバーのプロパティ](https://msdn.microsoft.com/library/windows/hardware/ff541205)

    [デバイス ドライバ パッケージのプロパティ](https://msdn.microsoft.com/library/windows/hardware/ff541200)

    [その他の他のデバイスのプロパティ](https://msdn.microsoft.com/library/windows/hardware/ff549289)

-   プロパティのキーを表す[デバイス セットアップ クラスのプロパティ](https://msdn.microsoft.com/library/windows/hardware/ff542239)SPCRP_Xxx 識別子に対応しています。 (で SPCRP_Xxx 識別子が定義されている*Setupapi.h*)。

-   対応する SPCRP_Xxx 識別子がないデバイス セットアップ クラスのプロパティを表すプロパティのキー。

-   プロパティのキーを表す[デバイス インターフェイスのクラス プロパティ](https://msdn.microsoft.com/library/windows/hardware/ff541406)します。

-   プロパティのキーを表す[デバイス インターフェイスのプロパティ](https://msdn.microsoft.com/library/windows/hardware/ff541409)します。

カスタムのデバイスのプロパティを作成する方法については、[カスタム デバイス プロパティの作成](creating-custom-device-properties.md)を参照してください。

 

 





