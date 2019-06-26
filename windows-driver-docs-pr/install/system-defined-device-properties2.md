---
title: システム定義のデバイス プロパティ
description: システム定義のデバイス プロパティ
ms.assetid: 9d823a9f-0802-4e92-bf94-abb5b0e7b9ee
keywords:
- システム定義のデバイス プロパティ、WDK のデバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfa4ae50e99c87c9bbffc4b79125d88f8de92b28
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385863"
---
# <a name="system-defined-device-properties"></a>システム定義のデバイス プロパティ


Windows Vista および Windows での以降のバージョンで、[統一されたデバイス プロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)構成またはデバイスのインスタンスの操作の特性を示すシステム定義のプロパティをサポートしている[デバイス セットアップ クラス](device-setup-classes.md)、[デバイス インターフェイス クラス](device-interface-classes.md)、およびデバイスのインターフェイス。 によって表される各プロパティを[プロパティのキー](property-keys.md)、これはプロパティのカテゴリおよびプロパティの識別子を識別する GUID 値です。 システム定義のプロパティ、主要なカテゴリは、システム専用として予約されています。

次のシステム定義のデバイス プロパティのキーが定義されている*Devpkey.h*:

-   コンポーネントの名前を表す DEVPKEY_NAME プロパティのキー。 DEVPKEY_NAME プロパティの値を使用して、エンドユーザーにコンポーネントを識別します。 Windows の DEVPKEY_NAME プロパティをサポートする[**デバイス インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-name--device-instance-)、 [**デバイス セットアップ クラス**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-name--device-setup-class-)、および[ **デバイス インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-name--device-interface-)します。

-   プロパティのキーを表す、 [SPDRP_Xxx 識別子に対応するデバイス インスタンス プロパティ](https://docs.microsoft.com/previous-versions/ff541334(v=vs.85))します。 (、SPDRP_*Xxx*で識別子が定義されている*Setupapi.h*)。

-   デバイスを表すプロパティのキーのインスタンスのプロパティを対応する SPDRP_ を持たない*Xxx*識別子。 これには、次のデータが含まれます。

    [デバイスの状態および問題のプロパティ](https://docs.microsoft.com/previous-versions/ff542254(v=vs.85))

    [デバイスのリレーション プロパティ](https://docs.microsoft.com/previous-versions/ff541498(v=vs.85))親デバイス、デバイスの子、兄弟デバイスなど、

    [デバイス ドライバーのプロパティ](https://docs.microsoft.com/previous-versions/ff541205(v=vs.85))

    [デバイス ドライバ パッケージのプロパティ](https://docs.microsoft.com/previous-versions/ff541200(v=vs.85))

    [その他の他のデバイスのプロパティ](https://docs.microsoft.com/previous-versions/ff549289(v=vs.85))

-   プロパティのキーを表す[デバイス セットアップ クラスのプロパティ](https://docs.microsoft.com/previous-versions/ff542239(v=vs.85))SPCRP_Xxx 識別子に対応しています。 (で SPCRP_Xxx 識別子が定義されている*Setupapi.h*)。

-   対応する SPCRP_Xxx 識別子がないデバイス セットアップ クラスのプロパティを表すプロパティのキー。

-   プロパティのキーを表す[デバイス インターフェイスのクラス プロパティ](https://docs.microsoft.com/previous-versions/ff541406(v=vs.85))します。

-   プロパティのキーを表す[デバイス インターフェイスのプロパティ](https://docs.microsoft.com/previous-versions/ff541409(v=vs.85))します。

カスタムのデバイスのプロパティを作成する方法については、次を参照してください。[カスタム デバイス プロパティの作成](creating-custom-device-properties.md)です。

 

 





