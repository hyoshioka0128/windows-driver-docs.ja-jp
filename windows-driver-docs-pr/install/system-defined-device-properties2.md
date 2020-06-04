---
title: システム定義のデバイス プロパティ
description: システム定義のデバイス プロパティ
ms.assetid: 9d823a9f-0802-4e92-bf94-abb5b0e7b9ee
keywords:
- デバイスのプロパティ WDK デバイスのインストール、システム定義
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca583ca5242add42be6d73c56321d1d2622396b4
ms.sourcegitcommit: a386cf5ac5a157dfe1041e7c23b6e70a33ca2704
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/03/2020
ms.locfileid: "84330060"
---
# <a name="system-defined-device-properties"></a>システム定義のデバイス プロパティ


Windows Vista 以降のバージョンの Windows では、デバイスインスタンス、[デバイスセットアップクラス](device-setup-classes.md)、[デバイスインターフェイスクラス](device-interface-classes.md)、デバイスインターフェイスの構成や操作を特徴とするシステム定義のプロパティが[統合デバイスプロパティモデル](unified-device-property-model--windows-vista-and-later-.md)によってサポートされています。 各プロパティはプロパティ[キー](property-keys.md)によって表されます。これは、プロパティのカテゴリとプロパティ識別子を識別する GUID 値です。 システム定義のプロパティのキーカテゴリは、システムでのみ使用するために予約されています。

次のシステム定義のデバイスプロパティキーは、 *Devpkey*で定義されています。

-   コンポーネントの名前を表す DEVPKEY_NAME プロパティキーです。 コンポーネントをエンドユーザーに識別には、DEVPKEY_NAME プロパティの値を使用します。 Windows では、[**デバイスインスタンス**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-name--device-instance-)、[**デバイスセットアップクラス**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-name--device-setup-class-)、[**デバイスインターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-name--device-interface-)の DEVPKEY_NAME プロパティがサポートされています。

-   [SPDRP_Xxx の識別子に対応するデバイスインスタンスのプロパティ](https://docs.microsoft.com/previous-versions/ff541334(v=vs.85))を表すプロパティキー。 (SPDRP_*Xxx*識別子は、 *setupapi.log*で定義されています)。

-   対応する SPDRP_*Xxx*識別子を持たないデバイスインスタンスプロパティを表すプロパティキー。 これには、次の内容が含まれます。

    [デバイスの状態と問題のプロパティ](https://docs.microsoft.com/windows-hardware/drivers/install/retrieving-the-status-and-problem-code-for-a-device-instance)

    [デバイスの関係のプロパティ](https://docs.microsoft.com/previous-versions/ff541498(v=vs.85))(親デバイス、子デバイス、兄弟デバイスなど)

    [デバイスドライバーのプロパティ](https://docs.microsoft.com/previous-versions/ff541205(v=vs.85))

    [デバイスドライバーパッケージのプロパティ](https://docs.microsoft.com/previous-versions/ff541200(v=vs.85))

    [その他のデバイスのプロパティ](https://docs.microsoft.com/previous-versions/ff549289(v=vs.85))

-   SPCRP_Xxx の識別子に対応する[デバイスセットアップクラスのプロパティ](https://docs.microsoft.com/previous-versions/ff542239(v=vs.85))を表すプロパティキー。 (SPCRP_Xxx 識別子は、 *setupapi.log*で定義されています)。

-   対応する SPCRP_Xxx 識別子を持たないデバイスセットアップクラスのプロパティを表すプロパティキー。

-   [デバイスインターフェイスクラスのプロパティ](https://docs.microsoft.com/previous-versions/ff541406(v=vs.85))を表すプロパティキー。

-   [デバイスインターフェイスのプロパティ](https://docs.microsoft.com/previous-versions/ff541409(v=vs.85))を表すプロパティキー。

カスタムデバイスプロパティを作成する方法の詳細については、「[カスタムデバイスプロパティの作成](creating-custom-device-properties.md)」を参照してください。

 

 





