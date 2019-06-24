---
title: プリミティブ ドライバーの作成
description: プリミティブ ドライバーは、INF ベースのインストールを使用するが特定のハードウェア デバイスに関連付けられているとは限らないソフトウェアを処理および管理するために使用します。
ms.date: 04/16/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: e1588c5d17710faa91f4c13890988944cec860b5
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63382422"
---
# <a name="creating-a-new-primitive-driver"></a>新しいプリミティブ ドライバーの作成

プリミティブ ドライバーは、INF ベースのインストールを使用するが特定のハードウェア デバイスに関連付けられているとは限らないソフトウェアを処理および管理するために使用します。

## <a name="background-and-benefits-of-primitive-drivers"></a>プリミティブのドライバーの背景と利点

Windows 10 バージョン 1903 以前は、INF ベースのインストールを使用するが特定のハードウェア デバイスに関連付けられているとは限らない特定の種類のソフトウェアは、OS で完全にサポートされていませんでした。 これらの種類のソフトウェアではインストールのマニフェストとして INF ファイルが使用されますが、このシナリオは OS では直接認識されず、これをネイティブに処理するためのサポートがありませんでした。

これらの種類のソフトウェアは、ハードウェア デバイスに関連付けられていないため、ハードウェアを問わずシステム全体にインストールされていました。 その結果、OS のアップグレード時にこれらの種類のソフトウェアが適切にインストール、アンインストール、または処理される保証がありませんでした。

プラグ アンド プレイ プラットフォーム (Windows 10 バージョン 1903 以降) では、これらの種類のソフトウェアの信頼性を向上させて適切な動作を保証するために、特に OS のアップグレードとリセットのシナリオにおいて、この種類のソフトウェア パッケージが最上位レベルのエンティティとして処理および管理されるようになりました。

この新しいプラットフォームのサポートを利用するソフトウェアの種類を、**プリミティブ ドライバー**といいます。 プリミティブ ドライバーでは引き続き INF ベースのインストールが使用され、基になるプラットフォームでは[ドライバー ストア](https://docs.microsoft.com/windows-hardware/drivers/install/driver-store)を利用して関連するすべてのファイルが記録されます。

基になるプラグ アンド プレイ プラットフォームでは、OS のアップグレード時にドライバーの状態が適切にインストール、アンインストール、および維持されます。

概念的には、これらの INF は異なる方法で管理されます。 以前は、\[DefaultInstall\] (多くの場合、\[DefaultUninstall\] も) は、[SetupAPI](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi) によってスクリプトのように処理されていました。つまり、INF がマニフェストとして使用され、呼び出し元の代わりに [SetupAPI](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi) によって関連するセクションの手順が実行されていました。

(アンインストールを実行するために) 変更を元に戻すには、インストール セクションとは逆の一連の手順を実行する INF セクションを指定する必要がありました。 しかし、INF を利用するプリミティブ ドライバーでは、アンインストール セクションは必要ありません。

プリミティブ ドライバーでは、デバイス ドライバーと同じインストール API とアンインストール API が使用されます。アンインストール API ではインストール操作とは逆の一連の操作が実行され、ドライバー パッケージのインストールまたはアンインストールによってそれらのセクションが処理されます。

## <a name="inf-requirements-to-access-primitive-driver-functionality"></a>プリミティブ ドライバーの機能にアクセスするための INF の要件

* PnP ドライバーと同様に、**Version** セクションに入力する必要があります。

  * **Provider** ディレクティブを入力する必要があります。

  * **Class** ディレクティブを入力する必要があります。

  * **ClassGuid** ディレクティブを入力する必要があります。

* ドライバーが[ユニバーサル](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)要件に準拠している必要があります。

* \[Manufacturer\] セクションがない場合もあります。

* \[DefaultInstall\] セクションはアーキテクチャで修飾されている必要があり、装飾されていないバージョンがない場合もあります。

  * **正しい例:** \[DefaultInstall.amd64\]

  * **誤った例:** \[DefaultInstall\]

* \[DefaultUninstall\] は INF にない場合もあります (例外については「[レガシ互換性](#legacy-compatibility)」をご覧ください)。

## <a name="primitive-drivers-targeting-only-windows-10-version-1903-and-later"></a>Windows 10 バージョン 1903 以降のみを対象とするプリミティブ ドライバー

Windows 10 バージョン 1903 のみを対象とするプリミティブ ドライバーでソフトウェアを適切にドライバー ストアにインストール/ドライバー ストアからアンインストールするには、[DiInstallDriver](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldriverw) と [DiUninstallDriver](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diuninstalldriverw) を使用する必要があります。

また、インストール先のドライバー ストアを適切に指定するために、Dirid 13 も使用する必要があります。 Dirids の詳細については、「[Dirids の使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-dirids)」をご覧ください。

## <a name="legacy-compatibility"></a>レガシ互換性

プリミティブ ドライバーでは \[DefaultUninstall\] が禁止されていますが、OS の下位互換性のために、例外が設けられています。 Windows に導入された INF ディレクティブは、プリミティブ ドライバーをサポートする OS バージョンで \[DefaultUninstall\] セクションが無視される原因となります。 ドライバー パッケージで OS の下位バージョンをサポートする必要がある場合は、そのようなケースが適切にプラットフォームで処理されるように、次の構文を含めます。

```INF
[DefaultUninstall.NTamd64]
LegacyUninstall=1
```

\[DefaultInstall\] および \[DefaultUninstall\] セクションは、**引き続きアーキテクチャで装飾されている必要があります**。ただし、`LegacyUninstall=1` を含めることで、Windows で \[DefaultUninstall\] セクションが無視されます (Windows 10 バージョン 1903 以降)。 これを行うことにより、INF にそのセクションを含めることができ、これを従来のアプリケーションのインストール/アンインストールで使用して、プリミティブ ドライバー パッケージをアンインストールすることができます。

Windows 10 バージョン 1903 以降は、アーキテクチャで装飾された \[DefaultInstall\] または \[DefaultUninstall\] セクションを setupapi.dll で [InstallHInfSection](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-installhinfsectionw) API に渡す場合、ドライバー パッケージがプリミティブ ドライバーの機能をサポートしているかどうかがチェックされます。 プリミティブ ドライバーの機能をサポートしている場合は、指定されたセクションを従来の方法で処理するのではなく、[DiInstallDriver](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldrivera) または [DiUninstallDriver](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diuninstalldriverw) の適切な方に INF が渡されます。 これにより、1 つのインストーラーで、互換性のある OS バージョンではプリミティブ ドライバーを使用し、以前の OS バージョンのサポートも維持することができます。
