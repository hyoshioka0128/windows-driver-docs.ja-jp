---
title: フレームワーク ライブラリのバージョン
description: このトピックでは、カーネルモードドライバーフレームワーク (KMDF) ライブラリとユーザーモードドライバーフレームワーク (UMDF) ライブラリのファイル名の名前付け規則について説明します。
ms.assetid: 51db6f3c-45cb-46a7-9dd4-2bab67893fea
keywords:
- カーネルモードドライバー WDK KMDF、ライブラリバージョン
- KMDF WDK、ライブラリバージョン
- カーネルモードドライバーフレームワーク WDK、ライブラリバージョン
- ライブラリ WDK KMDF
- バージョン番号 WDK KMDF
- メジャーバージョン番号 WDK KMDF
- マイナーバージョン番号 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f67147e2201e9364928be3b1c27ad1c9ac8b85eb
ms.sourcegitcommit: 73a693bf52f07169f38e6a2a68bccaa8db8faf2a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68341187"
---
# <a name="framework-library-versioning"></a>フレームワーク ライブラリのバージョン


このトピックでは、カーネルモードドライバーフレームワーク (KMDF) ライブラリとユーザーモードドライバーフレームワーク (UMDF) ライブラリのファイル名の名前付け規則について説明します。

## <a name="kmdf"></a>KMDF


メジャーバージョン番号とマイナーバージョン番号は、KMDF ライブラリの各バージョンに割り当てられます。 ライブラリのファイル名にメジャーバージョン番号が含まれています。 ファイル名の形式は次のとおりです。

**Wdf**&lt;MajorVersionNumber000&gt; **. sys**

メジャーバージョン番号は2文字を使用します。 たとえば、ライブラリのバージョン1.0 のファイル名は*Wdf01000*です。 バージョン1.9、1.11 なども*Wdf01000*という名前で、新しいマイナーバージョンのライブラリファイルは、以前のバージョンのファイルを上書きします。

システム上のバージョンより新しいバージョンの KMDF ライブラリを使用してドライバーをビルドした場合は、後者を更新する必要があります。 フレームワークライブラリの更新の詳細については、「[再頒布可能フレームワークコンポーネント](installation-components-for-kmdf-drivers.md)」を参照してください。

(フレームワークの共同インストーラーのファイル名には、メジャーバージョン番号とマイナーバージョン番号の両方が含まれていることに注意してください。 共同インストーラーファイル名の詳細については、「 [KMDF 共同インストーラーの使用](installing-the-framework-s-co-installer.md)」を参照してください。

ドライバーをビルドすると、MSBuild ユーティリティは、MSBuild ユーティリティが使用したライブラリのバージョン番号を含むスタブファイルにドライバーをリンクします。 オペレーティングシステムによってドライバーが読み込まれると、フレームワークのローダーは、ドライバーのスタブ内のバージョン情報をチェックして、ドライバーがシステム上のフレームワークライブラリのバージョンで実行されるかどうかを判断します。

ドライバーが実行されているライブラリのバージョンを確認するには、ドライバーは[**Wdfdriverisversionavailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdriverisversionavailable)または[**WdfDriverRetrieveVersionString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdriverretrieveversionstring)を呼び出すことができます。

WDF を使用すると、ドライバーが実行されるのとは異なるバージョンの Windows を使用してドライバーをビルドできます。  詳細については、「[複数のバージョンの Windows 用の WDF ドライバーのビルド](https://docs.microsoft.com/windows-hardware/drivers/wdf/building-a-wdf-driver-for-multiple-versions-of-windows)」を参照してください。

KMDF ライブラリのリリース履歴の詳細については、「 [Kmdf のバージョン履歴](kmdf-version-history.md)」を参照してください。

## <a name="umdf"></a>UMDF


KMDF と同様に、UMDF ライブラリのメジャーバージョン番号は2文字を使用します。 ただし、メジャーバージョン番号は、umdf バージョン2.0 以降の UMDF ライブラリファイル名にのみ表示されます。

UMDF version 2.0 では、UMDF ライブラリのファイル名は*Wudfx02000*です。

UMDF バージョン1の場合。*x*の場合、UMDF ライブラリのファイル名は*wudfx .dll*です。

KMDF ライブラリのリリース履歴の詳細については、「 [UMDF Version history](umdf-version-history.md)」を参照してください。


