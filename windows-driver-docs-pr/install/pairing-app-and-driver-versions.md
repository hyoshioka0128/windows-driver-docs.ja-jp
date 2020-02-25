---
title: ドライバーとユニバーサル Windows プラットフォーム (UWP) アプリとのペアリング
description: このトピックでは、特定のドライバーが存在する場合にのみ、ユニバーサル Windows プラットフォーム (UWP) アプリを読み込むように指定する方法について説明します。
ms.assetid: 50f981bb-e17b-4454-88f9-46b09eb05509
ms.date: 08/24/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8b9d79f2fa11b2d607352f0ae005e3b7196ed1f
ms.sourcegitcommit: c9e5aa086b72ae9c1a31bf952d0711383cfd4bbd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/25/2020
ms.locfileid: "77575206"
---
# <a name="pairing-a-driver-with-a-universal-windows-platform-uwp-app"></a>ドライバーとユニバーサル Windows プラットフォーム (UWP) アプリとのペアリング

Windows 10 バージョン1709以降では、特定のドライバーが存在する場合にのみ、ユニバーサル Windows プラットフォーム (UWP) アプリを読み込むように指定できます。 このオプションを使用すると、Microsoft Store は、ユーザーのコンピューターにインストールされているバージョンのドライバーで動作するアプリの最新バージョンを各ユーザーに提供します。

アプリは、特定のドライバーのバージョンまたは日付への読み込みをさらに制限することができます。  このトピックでは、このような要件を作成するために、アプリとドライバーの両方で必要な手順について説明します。

## <a name="steps-in-the-app"></a>アプリのステップ

特定のドライバーが存在するときに UWP アプリが読み込まれるようにするには、アプリのマニフェスト XML (.appx) ファイルに2つの XML 要素を追加します。

* [uap5: DriverDependency](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap5-driverdependency)
* [uap5: DriverConstraint](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap5-driverconstraint)

特に、これらの要素を使用して、少なくとも1つのドライバーの制約を含むドライバーの依存関係を少なくとも1つ指定します。  これらの要素の使用方法の詳細については、上記のリンク先の参照ページを参照してください。  後者のページには例が含まれています。

## <a name="steps-in-the-driver"></a>ドライバーのステップ

次に、ドライバーの INF ファイルで次の操作を行います。

1. [INF AddSoftware ディレクティブ](inf-addsoftware-directive.md)を指定します。
2. **ソフトウェアの種類**のエントリを2に設定します。
3. **[ソフトウェア id]** エントリにパッケージファミリ名 (PFN) を指定します。

最新のアプリとドライバーのバージョンを照合するだけでなく、システムは以前のアプリとドライバーのバージョンを照合しようとします。  たとえば、アプリバージョン2で最小ドライバーバージョン2が指定され、アプリバージョン1で最小ドライバーバージョン1が指定されている場合、ドライバーバージョン1のシステムでは、アプリバージョン1が正常に読み込まれます。

## <a name="see-also"></a>参照

* [uap5: DriverDependency](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap5-driverdependency)
* [uap5: DriverConstraint](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap5-driverconstraint)
* [INF AddSoftware ディレクティブ](inf-addsoftware-directive.md)
* [ハードウェアサポートアプリ (HSA): ドライバー開発者向けの手順](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)
* [ハードウェアサポートアプリ (HSA): アプリ開発者向けの手順](../devapps/hardware-support-app--hsa--steps-for-app-developers.md)
