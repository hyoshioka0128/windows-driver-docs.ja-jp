---
title: WLAN ユニバーサル Windows ドライバー モデル
description: WDI (WLAN デバイスドライバーインターフェイス) は、Windows 10 用の新しいユニバーサル Windows ドライバーモデルです。
ms.assetid: 6EF92E34-7BC9-465E-B05D-2BCB29165A18
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5532b9cdceb43e17b602d2610c46900d89a788b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844395"
---
# <a name="wlan-universal-windows-driver-model"></a>WLAN ユニバーサル Windows ドライバー モデル


WDI (WLAN デバイスドライバーインターフェイス) は、Windows 10 用の新しいユニバーサル Windows ドライバーモデルです。 WLAN デバイスの製造元は、単一の WDI ミニポート ドライバーを作成して、すべてのデバイス プラットフォームで実行することができます。これに必要なコードは、前のネイティブ WLAN ドライバー モデルよりも少なくなります。 Windows 10 で導入されるすべての新しい WLAN 機能には WDI ベースのドライバーが必要です。

ベンダーから提供されるネイティブ WLAN ドライバーは Windows 10 で引き続き動作しますが、開発時に対象とした Windows バージョンの機能に限定されます。

WDI ヘッダーファイル wditypes と dot11wdi は、WDK に含まれています。

## <a name="how-to-write-a-universal-wlan-driver"></a>ユニバーサル WLAN ドライバーを作成する方法


ユニバーサル WLAN ドライバーを作成するには、「[ユニバーサル windows ドライバー](https://docs.microsoft.com/windows-hardware/drivers)を使用したはじめに」を参照し、「カーネルモードドライバー (kmdf) テンプレートを使用してユニバーサルドライバーを構築するための*ユニバーサル Windows ドライバーの構築*」に記載されている手順に従います。

次に、実装のガイダンスについては、WDI の設計とリファレンスのセクションを参照してください。

-   [WDI ミニポートドライバーの設計ガイド](wdi-miniport-driver-design-guide.md)
-   [WDI ミニポートドライバーリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

## <a name="related-topics"></a>関連トピック


[ユニバーサル Windows ドライバーの概要](https://docs.microsoft.com/windows-hardware/drivers)

 

 






