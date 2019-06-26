---
title: WLAN ユニバーサル Windows ドライバー モデル
description: WDI (WLAN デバイス ドライバー インターフェイス) は、Windows 10 用の新しいユニバーサル Windows ドライバー モデルです。
ms.assetid: 6EF92E34-7BC9-465E-B05D-2BCB29165A18
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 156c4761e5b8d9b4db92640e176759bfef3c6e41
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370559"
---
# <a name="wlan-universal-windows-driver-model"></a>WLAN ユニバーサル Windows ドライバー モデル


WDI (WLAN デバイス ドライバー インターフェイス) は、Windows 10 用の新しいユニバーサル Windows ドライバー モデルです。 WLAN デバイスの製造元は、単一の WDI ミニポート ドライバーを作成して、すべてのデバイス プラットフォームで実行することができます。これに必要なコードは、前のネイティブ WLAN ドライバー モデルよりも少なくなります。 Windows 10 で導入されるすべての新しい WLAN 機能には WDI ベースのドライバーが必要です。

ベンダーから提供されるネイティブ WLAN ドライバーは Windows 10 で引き続き動作しますが、開発時に対象とした Windows バージョンの機能に限定されます。

Wditypes.hpp と dot11wdi.h、WDI ヘッダー ファイルは、WDK に含まれます。

## <a name="how-to-write-a-universal-wlan-driver"></a>ユニバーサル WLAN ドライバーを記述する方法


ユニバーサル WLAN ドライバーを作成するを参照してください[ユニバーサル Windows ドライバーの概要](https://docs.microsoft.com/windows-hardware/drivers)、」の手順に従います*ユニバーサル Windows ドライバーをビルド*を使用して、ユニバーサル ドライバーをビルドするには。カーネル モード ドライバー (KMDF) のテンプレートです。

次に、実装のガイダンスについては、WDI デザインおよび参照セクションを参照してください。

-   [WDI ミニポート ドライバーの設計ガイド](wdi-miniport-driver-design-guide.md)
-   [WDI ミニポート ドライバー リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

## <a name="related-topics"></a>関連トピック


[ユニバーサル Windows ドライバーの概要](https://docs.microsoft.com/windows-hardware/drivers)

 

 






