---
title: ドライバーとユニバーサル Windows プラットフォーム (UWP) アプリとのペアリング
description: このトピックでは、特定のドライバーが存在する場合に、ユニバーサル Windows プラットフォーム (UWP) アプリがのみ読み込むことを指定する方法について説明します。
ms.assetid: 50f981bb-e17b-4454-88f9-46b09eb05509
ms.date: 08/24/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f31245dd44ee9597907614accdb956592fa84b1
ms.sourcegitcommit: c4dc4a78ea33537bd47fc7fb666cfd0718d302e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2019
ms.locfileid: "58349251"
---
# <a name="pairing-a-driver-with-a-universal-windows-platform-uwp-app"></a>ドライバーとユニバーサル Windows プラットフォーム (UWP) アプリとのペアリング

Windows 10 バージョン 1709 以降、特定のドライバーが存在する場合に、ユニバーサル Windows プラットフォーム (UWP) アプリがのみ読み込むことを指定できます。 このオプションを使用すると、Microsoft Store は、そのユーザーのコンピューターにインストールされているバージョンのドライバーで動作するアプリの最新バージョンを各ユーザーに提供します。

さらにアプリが、特定のドライバーのバージョンや日付への読み込みを制限します。  このトピックでは、このような要求を作成するアプリとドライバーの両方で必要な手順について説明します。

## <a name="steps-in-the-app"></a>アプリでの手順

UWP アプリを特定のドライバーが存在する場合にのみを読み込むには、2 つの XML 要素をアプリのマニフェスト XML (.appx) ファイルに追加します。

* [uap5:DriverDependency](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap5-driverdependency)
* [uap5:DriverConstraint](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap5-driverconstraint)

具体的には、これらの要素を使用して、少なくとも 1 つのドライバーの制約を含む少なくとも 1 つのドライバーの依存関係を指定します。  上記にリンクされているリファレンス ページのこれらの要素の使用方法の詳細な情報を参照してください。  後者のページには、例が含まれています。

## <a name="steps-in-the-driver"></a>ドライバーでの手順

次に、ドライバーの INF ファイルでは、次の操作を行います。

1. 指定、 [INF AddSoftware ディレクティブ](inf-addsoftware-directive.md)します。
2. 設定、 **SoftwareType** 2 を入力します。
3. パッケージ ファミリ名 (PFN) の提供、 **SoftwareID**エントリ。

最新のアプリとドライバーのバージョンに一致する、だけでなく、システムもアプリとドライバーの以前のバージョンの一致を試みます。  たとえば、アプリのバージョン 2 では、最小ドライバー バージョン 2、およびアプリのバージョン 1 = 最小のドライバーのバージョン 1 を指定します、ドライバーのバージョン 1 を搭載したシステムにアプリのバージョン 1 が読み込ま正常にれます。

## <a name="see-also"></a>関連項目

* [uap5:DriverDependency](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap5-driverdependency)
* [uap5:DriverConstraint](https://review.docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap5-driverconstraint?branch=lahugh-rs3)
* [INF AddSoftware ディレクティブ](inf-addsoftware-directive.md)
* [ハードウェア サポート アプリ (HSA):ドライバー開発者向け手順](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)
* [ハードウェア サポート アプリ (HSA):アプリ開発者向け手順](../devapps/hardware-support-app--hsa--steps-for-app-developers.md)
