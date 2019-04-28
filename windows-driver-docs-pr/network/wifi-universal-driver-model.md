---
title: WLAN ユニバーサル Windows ドライバー モデル
description: WDI (WLAN デバイス ドライバー インターフェイス) は、Windows 10 用の新しいユニバーサル Windows ドライバー モデルです。
ms.assetid: 6EF92E34-7BC9-465E-B05D-2BCB29165A18
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2c8b90af05caab82984ea70c062f5d3e682ab3b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378961"
---
# <a name="wlan-universal-windows-driver-model"></a>WLAN ユニバーサル Windows ドライバー モデル


WDI (WLAN デバイス ドライバー インターフェイス) は、Windows 10 用の新しいユニバーサル Windows ドライバー モデルです。 WLAN デバイスの製造元は、単一の WDI ミニポート ドライバーを作成して、すべてのデバイス プラットフォームで実行することができます。これに必要なコードは、前のネイティブ WLAN ドライバー モデルよりも少なくなります。 Windows 10 で導入されるすべての新しい WLAN 機能には WDI ベースのドライバーが必要です。

ベンダーから提供されるネイティブ WLAN ドライバーは Windows 10 で引き続き動作しますが、開発時に対象とした Windows バージョンの機能に限定されます。

Wditypes.hpp と dot11wdi.h、WDI ヘッダー ファイルは、WDK に含まれます。

## <a name="how-to-write-a-universal-wlan-driver"></a>ユニバーサル WLAN ドライバーを記述する方法


ユニバーサル WLAN ドライバーを作成するを参照してください[ユニバーサル Windows ドライバーの概要](https://msdn.microsoft.com/windows-drivers/develop/getting_started_with_universal_drivers)、」の手順に従います*ユニバーサル Windows ドライバーをビルド*を使用して、ユニバーサル ドライバーをビルドするには。カーネル モード ドライバー (KMDF) のテンプレートです。

次に、実装のガイダンスについては、WDI デザインおよび参照セクションを参照してください。

-   [WDI ミニポート ドライバーの設計ガイド](wdi-miniport-driver-design-guide.md)
-   [WDI ミニポート ドライバー リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn926075)

## <a name="related-topics"></a>関連トピック


[ユニバーサル Windows ドライバーの概要](https://msdn.microsoft.com/windows-drivers/develop/getting_started_with_universal_drivers)

 

 






