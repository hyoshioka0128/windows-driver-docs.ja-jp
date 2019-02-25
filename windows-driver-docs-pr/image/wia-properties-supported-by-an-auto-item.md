---
title: 自動アイテムでサポートされる WIA プロパティ
description: 自動アイテムでサポートされる WIA プロパティ
ms.assetid: 71b3a9ea-e402-4be8-9c62-9463e2a10f27
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 995920193026fc1f5702cb4fe42ba27da6c2697b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560072"
---
# <a name="wia-properties-supported-by-an-auto-item"></a>自動アイテムでサポートされる WIA プロパティ


[自動項目](auto-item.md)を表す、[スキャンの自動構成](auto-configured-scanning.md)WIA デバイス WIA アプリケーションでスキャン ジョブの介入なしにその設定のほとんどは自動的に構成での関数。 自動アイテムの詳細については、WIA の説明を参照してください。\_カテゴリ\_] の [自動] [WIA 項目カテゴリ](wia-item-categories.md)します。

WIA サービスは、自動項目では、次の WIA プロパティを管理します。

[**WIA\_IPA\_項目\_名**](https://msdn.microsoft.com/library/windows/hardware/ff551590)

[**WIA\_IPA\_完全\_項目\_名**](https://msdn.microsoft.com/library/windows/hardware/ff551561)

[**WIA\_IPA\_項目\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/ff551585)

[**WIA\_IPA\_アクセス\_権限**](https://msdn.microsoft.com/library/windows/hardware/ff551518)

[**WIA\_IPA\_色\_プロファイル**](https://msdn.microsoft.com/library/windows/hardware/ff551536)

WIA サービスが初期化、WIA\_IPA\_項目\_ミニドライバーによって送信された項目の名前に、プロパティ値を設定してミニドライバーの代わりに NAME プロパティです。 同様に、WIA サービスが、WIA を初期化します\_IPA\_項目\_ミニドライバーによって送信されたフラグ値にプロパティを設定してミニドライバーに代わって FLAGS プロパティ。

WIA ミニドライバーは、自動項目で、次のプロパティを実装できます。

[**WIA\_IPA\_項目\_カテゴリ**](https://msdn.microsoft.com/library/windows/hardware/ff551581)

[**WIA\_IPA\_圧縮**](https://msdn.microsoft.com/library/windows/hardware/ff551540)

[**WIA\_IPA\_FILENAME\_拡張機能**](https://msdn.microsoft.com/library/windows/hardware/ff551549)

[**WIA\_IPA\_形式**](https://msdn.microsoft.com/library/windows/hardware/ff551553)

[**WIA\_IPA\_優先\_形式**](https://msdn.microsoft.com/library/windows/hardware/ff551623)

[**WIA\_IPA\_TYMED**](https://msdn.microsoft.com/library/windows/hardware/ff551656)

自動項目、WIA アーキテクチャが必要です WIA を除く、上記のすべてのプロパティをサポートするミニドライバー\_IPA\_FILENAME\_拡張機能。 サポート、WIA\_IPA\_FILENAME\_拡張機能プロパティは省略可、ただし推奨します。

ミニドライバーは、WIA を設定する必要があります\_IPA\_項目\_WIA 値に自動アイテムのプロパティをカテゴリ\_カテゴリ\_自動。 上記のリストの最後の 5 つのプロパティは、自動構成済みのスキャン中にデバイスを取得するイメージ データを転送するために使用するファイル形式をネゴシエートする WIA アプリケーションを有効にします。 アプリケーションでは、その内部の要件に基づくファイル形式を選択する必要があります。 一部のアプリケーションには、アプリケーションとドライバーの両方でサポートされている形式の一覧から、ファイル形式を選択するユーザーが有効にする場合があります。

 

 




