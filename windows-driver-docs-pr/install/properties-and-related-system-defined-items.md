---
title: プロパティと関連するシステム定義の項目
description: プロパティと関連するシステム定義の項目
ms.assetid: 87787a84-6403-4246-abf5-49747b883202
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b6b8c410ea9731037ef256e2dd8e450f56adc56
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380466"
---
# <a name="properties-and-related-system-defined-items"></a>プロパティと関連するシステム定義の項目


Windows Vista および Windows の以降のバージョンでは、統一されたデバイス プロパティのモデルは、システム定義のインストールに関連する次の項目とデバイスの管理の対応を管理します。

-   [システム定義プロパティ](system-defined-device-properties2.md)し、対応する[プロパティ キー](property-keys.md)、[プロパティのデータ型](property-data-type-identifiers.md)、およびプロパティの値。

-   SPDRP_*Xxx*デバイス インスタンス プロパティの識別子と、SPCRP_*Xxx*で定義されているデバイスのデバイス セットアップ クラス プロパティ id *Setupapi.h します。* CM_DRP_*Xxx*デバイス インスタンス プロパティの識別子と、CM_CRP_*Xxx*[デバイス セットアップ クラス](device-setup-classes.md)識別子で定義されている*Cfgmgr32.h*.

-   REGSTR_VAL_*Xxx*デバイスのインストールと管理に関連するレジストリ エントリ値の識別子。 これらの識別子が定義されている*Regstr.h*します。

-   デバイスのプロパティに対応するレジストリ エントリの値。

-   デバイスのプロパティを変更する INF のファイル エントリ値。

デバイスのプロパティに関連付けられているシステム定義の項目間の通信については、次のトピックを参照してください。

[デバイス インスタンスのプロパティ](https://docs.microsoft.com/previous-versions/ff541334(v=vs.85))

[デバイス セットアップ クラスのプロパティ](https://docs.microsoft.com/previous-versions/ff542239(v=vs.85))

[デバイスのインターフェイス クラスのプロパティ](https://docs.microsoft.com/previous-versions/ff541406(v=vs.85))

[デバイス インターフェイスのプロパティ](https://docs.microsoft.com/previous-versions/ff541409(v=vs.85))

 

 





