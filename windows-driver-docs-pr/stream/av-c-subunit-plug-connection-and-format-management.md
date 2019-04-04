---
title: AV/C サブユニット プラグ接続と形式管理
description: AV/C サブユニット プラグ接続と形式管理
ms.assetid: c80641d5-3108-4dbc-91b9-7ed295434b97
keywords:
- WDK AV/C 接続を接続します。
- サブユニット サポート WDK AV/C
- AV/C WDK、プラグ接続
- ピアのサブユニット ドライバー WDK AV/C をスタックします。
- KS 接続 WDK AV/C をピン留め
- 接続 WDK AV/C をピン留め
- WDK AV/C を書式設定します。
- pin が WDK AV/C を書式設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0fe524c888c92de7457044f484bd68f570ca6fe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572049"
---
# <a name="avc-subunit-plug-connection-and-format-management"></a>AV/C サブユニット プラグ接続と形式管理





AV/C ピアのサブユニット ドライバー スタックは、IEEE 1394 と AV/C サブユニットの関数のプラグイン接続と形式の管理を提供します。 カーネルのストリーミング (KS) pin 形式のネゴシエーションと pin 接続メカニズムはプラグイン経由の接続に変換されます*Avc.sys*します。 このアーキテクチャの重要な側面は次のとおりです。

-   IEEE 1394 および AV/C のサブユニット プラグ接続は、DirectShow フィルター グラフで KS 暗証番号 (pin) の接続として表されます。

-   内部のサブユニットがない場合にのみ、KS ピンのプラグイン接続の機能と、IEEE 1394 シリアル バス プラグ (入力と出力プラグ) が直接表されます。 この場合、IEEE 1394 シリアル バス プラグインあたり 1 つの pin があります。

-   中規模のグローバル一意識別子 (GUID) は、IEEE 1394 シリアル バス接続を表します。 中規模の Guid の詳細については、[メディアとカテゴリ](mediums-and-categories.md)を参照してください。

-   中規模の Guid の永続的なの内部 AV/C の単体テストとサブユニット接続では、デバイス一意識別子ら合成されましたが、アドレスを接続します。

-   AV/C 接続で使用する新しい KSDATARANGE と KSDATAFORMAT 拡張機能があります。

メディアと一緒の形式かを調べるかどうか KS 暗証番号 (pin) の接続データと、コンピューターの間、IEEE 1394 シリアル バス経由でデバイスの内部に役立ちます。

 

 




