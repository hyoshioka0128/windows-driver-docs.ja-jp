---
title: フレームワーク ライブラリのバージョン
description: このトピックでは、カーネル モード ドライバー フレームワーク (KMDF) ライブラリとユーザー モード ドライバー フレームワーク (UMDF) ライブラリのファイル名の名前付け規則について学習します。
ms.assetid: 51db6f3c-45cb-46a7-9dd4-2bab67893fea
keywords:
- カーネル モード ドライバー WDK KMDF、ライブラリのバージョン
- KMDF WDK、ライブラリのバージョン
- カーネル モード ドライバー フレームワーク WDK、ライブラリのバージョン
- WDK KMDF ライブラリ
- バージョン番号を WDK KMDF
- メジャー バージョン番号を WDK KMDF
- マイナー バージョン番号を WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2544f6c59809aecaaa8fb54870ff80b6aa55ea74
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528427"
---
# <a name="framework-library-versioning"></a>フレームワーク ライブラリのバージョン


このトピックでは、カーネル モード ドライバー フレームワーク (KMDF) ライブラリとユーザー モード ドライバー フレームワーク (UMDF) ライブラリのファイル名の名前付け規則について学習します。

## <a name="kmdf"></a>KMDF


KMDF ライブラリの各バージョンには、メジャー バージョン番号とマイナー バージョン番号が割り当てられます。 ライブラリのファイル名には、メジャー バージョン番号が含まれています。 ファイル名の形式です。

**Wdf**&lt;*MajorVersionNumber*&gt;**000. sys**

メジャー バージョン番号は、2 つの文字を使用します。 たとえば、ライブラリのバージョン 1.0 のファイル名は*Wdf01000.sys*します。 バージョン 1.9 や 1.11 がという名前でも*Wdf01000.sys*、ライブラリ ファイルの新しいマイナー バージョンは、ファイルの以前のバージョンを上書きします。

システム上にある framework のバージョンよりも新しい KMDF ライブラリのバージョンを使用して、ドライバーをビルドした場合は、後者更新しなければなりません。 フレームワーク ライブラリの更新方法の詳細については、次を参照してください。[再頒布可能フレームワーク コンポーネント](installation-components-for-kmdf-drivers.md)します。

(フレームワーク co-インストーラーのファイル名が、両方のメジャーおよびマイナー バージョン番号が含まれることに注意してください。 共同インストーラーのファイル名の詳細については、次を参照してください[KMDF 共同インストーラーを使用して](installing-the-framework-s-co-installer.md)。)。

ドライバーをビルドする MSBuild ユーティリティは、ドライバーを MSBuild ユーティリティを使用しているライブラリのバージョン番号を含むスタブ ファイルにリンクします。 オペレーティング システムでは、ドライバーが読み込まれたら、フレームワークのローダーは、ドライバーは、システム上にある framework ライブラリのバージョンで実行される場合を判断するドライバーのスタブのバージョン情報を確認します。

ドライバーを呼び出すことができます、ドライバーを実行しているライブラリのバージョンを調べるに[ **WdfDriverIsVersionAvailable** ](https://msdn.microsoft.com/library/windows/hardware/ff547190)または[ **WdfDriverRetrieveVersionString**](https://msdn.microsoft.com/library/windows/hardware/ff547211).

KMDF ライブラリのリリース履歴については、次を参照してください。 [KMDF バージョン履歴](kmdf-version-history.md)します。

## <a name="umdf"></a>UMDF


KMDF と同様、UMDF ライブラリのメジャー バージョン番号は、2 つの文字を使用します。 ただし、メジャー バージョン番号は、UMDF バージョン 2.0 以降、UMDF ライブラリ ファイル名にのみ表示されます。

UMDF バージョン 2.0 では、UMDF ライブラリのファイル名は*Wudfx02000.dll*します。

UMDF バージョン 1。*x*、UMDF ライブラリのファイル名は*Wudfx.dll*します。

KMDF ライブラリのリリース履歴については、次を参照してください。 [UMDF バージョン履歴](umdf-version-history.md)します。


 





